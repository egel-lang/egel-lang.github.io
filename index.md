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

Egel is a very small toy language based on untyped eager combinator rewriting.

Possible uses are:

+ Small 'mathy' domain specific languages
+ Experiments with untyped rewriting
+ Mobile code

Egel roughly falls in the same category as Q and conceptually predates Miranda, ML, or Haskell.

The programming style is similar to functional programming though the operational semantics is
slightly novel.

## Language features

+ Symbolic evaluation
+ Namespaces
+ Exceptions
+ Concurrency

## Example code

```egel
namespace Fibonnaci (
  using System
  
  def fib =
    [ 0 -> 1
    | 1 -> 1
    | N -> fib (N-2) + fib (N-1) ]
)

using Fibonnaci

def main = fib 5
```

## The Egel interpreter

The Egel interpreter is implemented in C++ and designed to swiftly go 
from reading the sources to evaluation, though these goals are somewhat
at odds which each other.

The interpreter is mostly written to explore how far you can push
an implementation of a term rewrite system based on a directed acyclic graph in C++.
Combinators and the evaluation graphs are implemented with reference counted
objects and most of the implementation is written with utter disregard
for performance. That has drawbacks but it also gives a highly robust system which
can be seamlessly integrated into other C/C++ programs. Lastly, the 
interpreter employs bytecode in a small instruction set for maximal
portability.

The interpreter seems to have something between a naive Lisp and
Python performance. A REPL and batch mode evaluation is supported.

## Roadmap and mobile code

Egel is developed as a hobby project to explore some ideas the author
has. The intention is to grow the language to support different math
libraries and then move towards making the code mobile. The aim
is to become a small data-center language for distributed ad-hoc
computation; i.e., a light-weight solution for moving code to data
fast.

## Links

You can find the sources on [github](http://github.com/egel-lang/).
I blog about my progress on [blogger](http://egel-language.blogspot.nl/).
I started on a [FAQ](https://egel-lang.github.io/FAQ.html).
A short post on the [operational semantics](https://egel-lang.github.io/SEMANTICS.html).
## Thanks

I would like to thank Linus Torvalds for Linux, the GNU team for their
command line tools and compiler chain, Bram Molenaar for
VIM, GNOME for their desktop, and Redhat for providing me with a 
great operating system for the last twenty years.
</body>
</html>
