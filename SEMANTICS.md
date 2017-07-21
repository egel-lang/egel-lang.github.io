---
layout: default
title: Egel Language
---
<html markdown="1">
<head>
<link rel="stylesheet" href="css/main.css">
</head>
<body markdown="1">
# Operational Semantics of Eager Combinator Rewriting

The operational semantics of the eager combinator rewrite system I use is trivial to explain with two pictures, so here goes.

Say, you have a term language where you want to rewrite an expression consisting of combinators. In Egel's case, each 
combinator knows how to rewrite itself, therefore, corresponds to a procedure or some code.



You could use a stack and push stackframes for F, G, and H. However, I wanted to experiment with another model, rewriting. 
Note that since we're rewriting eagerly we're rewriting the outermost expression first.

The operational semantics Egel uses is extremely simplistic: start with the node which is to be rewritten first, store 
the result where necessary, and continue with the next node to rewrite.



That's it. Note that the resulting graph is still a tree and is simply the starting tree turned upside down. Also, the 
resulting tree is still a directed acyclic graph. That's what enables me to implement Egel's interpreter with native C++ 
reference counted pointers.

This is, of course, a slow manner and restrictive manner of evalutation. For one, stack based evaluators are simply faster 
because pushing data to, or popping from, a stack is less computationally expensive than allocating, and deallocating, 
heap nodes. Second, it's a term rewrite system so you can't allow for assignment since that would usually allow you to 
create cyclic structures.

The main task of my interpreter's byte code generation is to maintain all invariants.

The benefits of this model are twofold. For one, you don't run out of stack space which is really important in a functional 
language as I have experienced, unfortunately. Second, it is still a tree rewrite system so you don't need to care about 
tail call optimization.

I simply like this model of evaluation, there isn't much more to it.

Notes: Yes, these are thunks or heap allocated stack frames. No, this isn't done with CPS since CPS is a transformation, 
not an evaluation strategy/model.

More: Egel also supports exceptions which is a natural extension of this model.
</body>
</html>