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

To get a taste of the language, an example is shown below.

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
at odds with each other. Egel is primarily about exploiting a trivialized 
operational model, a program (state) can be represented as a directed
acyclic graph _solely_ and program evaluation corresponds to trampolining
the combinator at the root of that graph.

The interpreter is written to explore how far you can push
an implementation of a term rewrite system based on directed acyclic graphs in idiomatic C++.
Combinators and the evaluation graphs are implemented with standard reference counted
objects and the implementation is written with utter disregard
for performance.

A REPL, batch mode, and command mode evaluation are supported.

The interpreter is in an alpha state, everything is still subject to possible change.

## Links

The sources are on [github](https://github.com/egel-lang/),
author's thoughts on [blogger](https://egel-language.blogspot.nl/),
or in the [FAQ](https://egel-lang.github.io/FAQ.html).
Also, [Twitter](https://twitter.com/egel_language/).
Read the fine [manual](https://egel-lang.github.io/egel.1.html).
The [operational semantics](https://github.com/egel-lang/egel-tex/blob/master/semantics/semantics.pdf) 
are discussed in a small technical note. 

The interpreter and associated documentation is distributed under 
the [MIT](https://github.com/egel-lang/egel/blob/master/LICENSE.md) License, 
© 2017 Marco Devillers.

## Thanks

I would like to thank Linus Torvalds for Linux, the GNU team for their
command line tools and compiler chain, Bram Molenaar for
VIM, GNOME for their desktop, and Redhat for providing me with a 
great operating system for the last twenty years.

And of course, [TIO](https://tio.run/) for hosting the interpreter online 
and [FSF](https://cfarm.tetaneutral.net/) for their gracious support in
supplying access to the compile farm.

</body>
</html>


