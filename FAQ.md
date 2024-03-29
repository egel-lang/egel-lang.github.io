---
layout: default
title: Egel Language FAQ
---
<html markdown="1">
<head>
<link rel="stylesheet" href="css/main.css">
</head>
<body markdown="1">
## FAQ about the Egel Language

This is a FAQ where I preemptively try to answer questions I think people will
have and document some design decisions.

## No type system? Are you serious?

Yes, and no. Or, no and yes. There isn't a type system for various reasons:

+ Egel is about showcasing the _usefulness_ of an operational model, a 
  particular manner of calculation. It has concurrency and exceptions, it is
  aimed at mobile code, and it shows how reference counting can be exploited.
  Types are mostly in the way of that goal.
+ C++ is verbose. Even this small interpreter took a lot of work. A type system
  would have increased that burden, it isn't what I am interested in, and I
  am not sure the additional work would pay off since I only wish to support
  trivial scripting tasks.
+ Type systems are a nice to have. Surprisingly, the workhorse of functional
  programming after sixty years still is Lisp. Its usage outnumbers other
  functional languages by several orders. I am not sure what to conclude from that
  but at least it shows that in practice people don't care much.
+ Types get in the way. Some mathematics is more easily described, matrix operations,
  in an untyped language. I want to script data-center calculations. It seemed
  a reasonable choice.
+ I wouldn't know what type system to implement. As a language needs to
  support more features its type system also becomes more baroque to meet
  new requirements. Academics constantly publish novel type system
  fixing yet another triviality, it's hard to get right and easy to get wrong.
+ After I got used to the idea I actually started wondering what would open
  up with an untyped language. Lisp research has lead to some baffling new 
  constructs, surprising usage of a simple operational semantics. I got interested
  what would, or could, happen if I relaxed all constraints I met.

## Eager rewriting? Surely modern math would suggest a lazy system?

+ No. Not for serious tasks in my opinion. In lazy systems, every once so often
  someone codes a small data processing application which when run on a large data 
  set suddenly starts to consume all memory and becomes unresponsive. 
  I consider this a show stopper. 
  Algorithms must have predictable behavior once implemented and deployed code
  shouldn't be able to suddenly explode on data.
+ Programmers have no idea how lazy evaluation behaves. They simply cannot
  keep track of it. Predictable behavior is better.
+ I do not intend to be very pure with this language. Which, see above,
  eager rewriting serves better.

## What is this combinator rewriting you talk about?

+ Combinator rewriting is an old approach to implementing (lazy) functional
  languages. It fell out of grace as it was recognized as being a slow
  manner of evaluation. But I still like the idea and revived it with
  a twist in order to implement mobile code. The basic idea is to have
  migrating combinator definitions. My translation scheme may explode 
  into too many of them, but hey, it's experimental!

+ After some questions I decided to add a separate page on the operational
  semantics. You can read about it [here](SEMANTICS.html).
  
## Do you support tail calls?

+ I support an experimental trivial eager rewrite system which should
  make tail calls unnecessary. It's expensive and you better hope I got 
  it right though.
  
## No cyclic structures?

+ Yep. To keep programmers sane I actually like the idea that all runtime
  structures are trees; moreover, those are easily serializable and
  collectable. Granted, you lose some sort of expressiveness with regard
  to, for example, Haskell but the benefits might pay off. You gain
  that your memory content won't be a mess, easily.
  
+ Another possible benefit is that rewriting acyclic graphs puts the 
  operational model in the middle of stack machines (like postscript)
  or generalized graph rewriters (like Haskell). This model should
  allow fast compacting garbage collection, I am not sure whether I'll
  implement that though. But it is an unique quality deserving it's own
  exploration. At minimum, Egel is another proof that you don't lose
  a lot of expressiveness switching to acyclic graphs.

## I am implementing cool product X. Should I include Egel for scripting?

+ No. Egel is experimental, probably full of bugs, and you will likely regret
  not having assignment. I recommend Lua, a small Lisp, or Python for your
  needs.
  
## Combinators are represented as C++ objects? Isn't this too expensive?

+ Combinators are runtime constants which are instantiated only once. The
  runtime passes pointers to them along.

## Why do you reference count?

+ Egel implements a term rewriting language which implies it should
  work on acyclic graphs. I wanted to see whether I could get away with
  using native C++ smart pointers only. There are drawbacks to that
  approach, I agree.
+ Reference counting is predictable. I don't like that in most garbage
  collecting schemes, for example, file handles are closed only after
  the collector makes a full sweep. In Egel, file handles are closed
  immediately after an object goes out of scope. That's the way it should
  be.
+ Reference counting is local and memories grow larger.
  Which means it might start to pay off
  on larger objects and on concurrent evaluation.
+ Again, you better hope I got every invariant right, though.

## Your bytecode doesn't support standard arithmetic?

+ Wrong, I agree. It stems from trying to work in vanilla C++ where due to technical
  reasons it's more easy to have a register language on pointers only.
  You do pay a hefty price for this, but my aim is to mostly support something like
  matrix operations in the long run. So, I don't care much. I hope Egel
  gives you acceptable speed.

## What about concurrency? Where's the stack?

+ Egel at the moment has provisional support for concurrency through a 'par'
  construct implemented with C++ threads. That is usually implemented on
  operating system primitives and for coarse grained parallelism. On my laptop
  it supports rougly 20k threads, though the Egel semantics would allow for
  a scheme (a thread is a term is a pointer) which could support much more.
+ I wanted a robust trivial scheme. I know it goes against conventional wisdom
  and I know my solution is slow but functional languages shouldn't run out of
  stack space, period. Out of memory, yes, out of stack space, no. So I went the
  robust road and implemented thunks, heap allocated stack frames.
