---
layout: default
title: Operational Semantics
---
<html markdown="1">
<head>
<link rel="stylesheet" href="css/main.css">
</head>
<body markdown="1">
# Operational Semantics of Eager Combinator Rewriting

The operational semantics of the eager combinator rewrite system I use is trivial to explain with two pictures, so here goes.

## Term evaluation
Say, you have a term language where you want to rewrite an expression consisting of combinators. In Egel's case, each 
combinator knows how to rewrite itself, therefore, corresponds to a procedure or some code.

![A term](tree1.png)

You could use a stack and push stackframes for F, G, and H. However, I wanted to experiment with another model, rewriting. 
Note that since we're rewriting eagerly we're rewriting the outermost expression first.

The operational semantics Egel uses is extremely simplistic: *Start* with the node which is to be rewritten first, *store* 
the result where necessary -the dotted line-, and *continue* with the next node to rewrite -the straight line-.

![Term traversal](tree2.png)

That's it. Note that the resulting graph is still a tree and is simply the starting tree turned upside down. Also, the 
resulting tree is still a directed acyclic graph. That's what enables me to implement Egel's interpreter with native C++ 
reference counted pointers.

## Drawbacks

This is, of course, a slow and restrictive manner of evalutation.
+ For one, stack based evaluators are simply faster because pushing data to, or popping from, a stack is less 
  computationally expensive than allocating, and deallocating, heap nodes.
+ Also, it's a term rewrite system so you can't allow for assignment since that would usually allow you to 
  create cyclic structures.

## Invariants

The main task of my interpreter's byte code generator is to maintain all invariants. That is: A) The 'stack'/'spine' forms a DAG and B) the results calculated are DAGs too.

## Advantages

The benefits of this model are twofold: 
+ First, you don't run out of stack space which is really important in a functional language as I have experienced, 
  unfortunately. It's a slow but extremely robust mode of operation; too often have I experienced with functional 
  programming that you test your code on small input, to have it explode on larger input. What's the point of functional
  programming if you're going to run out of stack space when using recursion?
+ Second, it is still a tree rewrite system so I don't need to care about tail call optimization. That is, say for "fac 5"
  the thunk is rewritten to the thunks corresponding to "5 * fac 4"; i.e, in classical terms, the stack frame is dropped and
  replaced. That is, classical factorial still takes O(n) space but a tail recursive one should take O(1).
  And, no, that doesn't generalize to most other languages, it's just an advantage of term rewriting.

I simply like this model of evaluation, there isn't much more to it.

**Notes:** Yes, these are thunks or heap allocated stack frames. No, this isn't done with CPS since CPS is a transformation, 
not an evaluation strategy/model.

**More:** Egel also supports exceptions which is a natural extension of this model.
</body>
</html>
