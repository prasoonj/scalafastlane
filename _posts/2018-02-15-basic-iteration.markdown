---
layout: post
title:  "#2. A Basic Iteration"
date:   2018-02-15 12:18:05 +0530
categories: Basic
description: Simple for comprehensions with Scala.
tags:
  - scala
  - iteration
---

# A Basic Iteration:

``` sh
scala> for (x <- (1 to 10)) yield { x * x }
res3: scala.collection.immutable.IndexedSeq[Int] = Vector(1, 4, 9, 16, 25, 36, 49, 64, 81, 100)

```

The part `(x <- (1 to 10))` is called the generator. We are using a Range here `(1 to 10)` but, this could be any type that has `IterableLike` as a trait (think of traits as an interface for now, we’ll come back to it.)

The function (inside the curly braces `{ }` ) is a function that is passed after the `yield` keyword. This function is responsible for taking each element of the generator and “doing something with it”. In this case we are just calculating squares of the numbers passed.

Few important points about the result of the operation:
1. Since we did not assign the expression (everything in Scala is an expression - we don’t have statements here, you’ll know why later) to any variable (`var` or `val`), the interpreter assigns the result to a `val` (yes, by default things are `val` not `var`) called `res3`.
2. Following the same convention as before, you can check the type of res3 which is `scala.collection.immutable.IndexedSeq[Int]`.
3. We started with a Range (1 to 10), the for comprehension yielded another Sequence for us - a Vector. Each element of this vector is equal to the square of each element of the Range. Simple!

## Exercises:
1. Try assigning this expression to a val/var and compare the results.
2. Use a String object as a generator and see what happens.
3. Here’s how you can print things - `println(“Hello Scala”)`. Try printing the values instead of returning a Vector.
4. Try the foreach construct like this:` (1 to 10) foreach { x => x * x }` Experiment with this slightly different syntax and try to see which one would be used where.
5. Use foreach for exercises 1 to 3.

Check out the [Scala Documentation][scala-docs] for more on the RePL!

[scala-docs]: https://docs.scala-lang.org/overviews/repl/overview.html
