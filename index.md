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

Egel roughly falls in the same category as SASL/KRC and conceptually predates Miranda, ML, or Haskell.

The programming style is similar to functional programming though the operational semantics is
slightly novel.

## Language features

+ Symbolic evaluation
+ Namespaces
+ Exceptions
+ Concurrency

## Example

To get a taste for the language, an example is shown below.

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

Want to know more? Then read the following short [introduction](http://egel.readthedocs.io).
Or [Try it online!](https://tio.run/##hVTbbtpAEH33V4ych9qlIVzUFyIqtWmFKkVEIi9YBCEHj8mq9q5lL2po02@nsxevl4a2lsA7Zy5ndi7GHRbH40VwAQvRoJQp3IgMAZ/TsiqQBP49Pbxp4Jbl2A@U3T3iBJ6krCZXV7Xx2ZJLX9S7IGBlJWoJYVVjsScQd6HDmCBRhEGwbxjfwf2hkVha4ZY10h6/3gVBhjk8irTOGvYDYQrvDYRlJQ8krmAJCVx@gAGsjYbxBoljGgA9Rv3p7uPiszLSmMUHkAwUxnJIeQYRAdMpLGOIEn1KYpBPyGHonLwHiwZtWBNo3dJvhaBcLX2BEhaUZV6LUgrKMequcgnDmJL1U6Jc9V3KtILoYdkdNbpUKSX0I7s1hV0YwqpmXG6xKNyV9bU0DGEfQo2@wMZD30LY5qsRnZXzb8vlUstFkRWw2ihmm9Mq0um0ITV/ZAtCijWZXrdsD5zYgIuqLY4r1Z7LP1hNNx2zDUlkulxRot8x9DrNebR3Yv23eMkrn@Qf1lHSO8PdO8usUXtPjs/Sa87cTt1cTdnYDpmZqIHrVWskaoi04Si2h3F86tKy7KsslfifTqqBpCZO7Vy5Jqqye@2DyPSmQwjKi1RKIjZNPJldFZZG1w8LNzDvQusSKERPr@fZjldtJgoGcbet5vACWrHxFHbFu9Ve2@8B5WCr8Vgw/g1rW4nIegxVGftOHJ2KYxKNd5kyTrdxOzz7MqdvggtqyOwtrH5Ier8F2uXUZPTaZOjXwq3ZzFvVHXKsU8kEn9AeXfv7OrNb9VNxvdPh9P/o1/H4Gw "Egel – Try It Online")
For a list of builtin combinators look [here](https://github.com/egel-lang/egel-gen/blob/main/combs.md).

## The Egel interpreter

The Egel interpreter is implemented in C++ and designed to swiftly go 
from reading the sources to evaluation, though these goals are somewhat
at odds which each other.

The interpreter is mostly written to explore how far you can push
an implementation of a term rewrite system based on directed acyclic graphs in idiomatic C++.
Combinators and the evaluation graphs are implemented with standard reference counted
objects and most of the implementation is written with utter disregard
for performance. That has drawbacks but it also gives a highly robust system which
can be seamlessly integrated into other C/C++ programs. Lastly, the 
interpreter employs bytecode in a small instruction set for maximal
portability.

The interpreter seems to have something between a naive Lisp and
Python performance though that can vary widly. To some extent, the interpreter
is a C++ Standard Library performance checker and on the FSF compile
farm the 'million.eg' (summation of a list of the first million natural 
numbers) microbenchmark results in anything between 1 min 22 secs on sparc64 
to 6 secs on Apple Silicon.

A REPL, batch mode, and command mode evaluation are supported.

The interpreter is in an beta state, ready for shipping. The language
is fixed and seems to run without problems but libraries are
either undeveloped or subject to change.

## Roadmap and mobile code

Egel is developed as a hobby project to explore some ideas the author
has. The intention is to grow the language to support different math
libraries and then move towards making the code mobile.

## License and links

The interpreter is distributed under 
the [MIT](https://github.com/egel-lang/egel/blob/master/LICENSE.md) License, 
(c) 2017 M.C.A. (Marco) Devillers.
The sources are on [github](https://github.com/egel-lang/),
author's thoughts on [blogger](https://egel-language.blogspot.nl/),
or in the [FAQ](https://egel-lang.github.io/FAQ.html).

## Thanks

I would like to thank Linus Torvalds for Linux, the GNU team for their
command line tools and compiler chain, Bram Molenaar for
VIM, GNOME for their desktop, and Redhat for providing me with a 
great operating system for the last twenty years.

And of course, [TIO](https://tio.run/) for hosting the interpreter online 
and [FSF](https://cfarm.tetaneutral.net/) for support with access to the 
compile farm.
</body>
</html>


