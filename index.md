---
layout: default
title: Egel Language
---
<html markdown="1">
<head>
<link rel="stylesheet" href="css/main.css">
</head>
<body markdown="1">
## The Egel Language

Egel is an untyped concurrent functional scripting language based on eager combinator rewriting with
a concise but remarkably powerful syntax.

Possible uses are:

+ Small 'mathy' domain specific languages
+ Experiments with untyped rewriting

Egel roughly falls in the same category as SASL/KRC and conceptually predates Miranda, ML, or Haskell; it combines a large number of ideas and is an esoteric language exploring dynamic functional programming through relaxing a maximal number of constraints while showcasing a novel means of calculation. Egel is also a useful language for software engineering in the small and easily combines with C/C++.

Egel's long-term goal is mobile code, transparently shoot any combinator anywhere.

## Language features

+ Symbolic evaluation
+ Namespaces
+ Exceptions
+ Concurrency

## Example

```egel
namespace Fibonacci (
    using System
  
    def fib =
        [ 0 -> 1
        | 1 -> 1
        | N -> fib (N - 2) + fib (N - 1) ]
)

using Fibonacci

def main = fib 5
```

## The Egel interpreter

The Egel interpreter is implemented in C++ and designed to swiftly go 
from reading the sources to evaluation, though these goals are somewhat
at odds with each other. Egel is primarily about exploiting a trivialized 
operational model, a program (state) can be represented as a directed
acyclic graph _solely_ and program evaluation corresponds to trampolining
the combinator at the root of that graph.

Combinators and evaluation graphs are implemented with standard reference counted
objects and the implementation is written with utter disregard
for performance.

A REPL, batch mode, and command mode evaluation are supported.

The interpreter is in an alpha state, everything is still subject to possible change.

## Links

The sources are on [github](https://github.com/egel-lang/),
author's thoughts on [blogger](https://egel-language.blogspot.nl/),
or in the [FAQ](https://egel-lang.github.io/FAQ.html).
There is a provisional [Website](https://egel.dev).
Also, [Twitter](https://twitter.com/egel_language/).
Read the fine [manual](https://egel-lang.github.io/egel.1.html).
The [operational semantics](https://github.com/egel-lang/egel-tex/blob/master/semantics/semantics.pdf) 
are discussed in a small technical note. 
For a list of builtin combinators look [here](https://github.com/egel-lang/egel-gen/blob/main/combs.md).
Or read the following short [introduction](http://egel.readthedocs.io).

The interpreter and associated documentation is distributed under 
the [MIT](https://github.com/egel-lang/egel/blob/master/LICENSE.md) License, 
© 2017 Marco Devillers.

## Thanks

I would like to thank Linus Torvalds for Linux, the GNU team for their
command line tools and compiler chain, Bram Molenaar for
VIM, GNOME for their desktop, and Red Hat for providing me with a 
great operating system for the last twenty years.

And of course, [CFarm](https://cfarm.tetaneutral.net/) for their gracious support in
supplying access to the compile farm.

</body>
</html>


