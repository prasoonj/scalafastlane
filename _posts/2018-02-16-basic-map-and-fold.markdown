---
layout: post
title:  "#3. Map and Fold"
date:   2018-02-16 06:18:05 +0530
categories: Basic
description: Working with collections using map and fold.
tags:
  - scala
  - map
  - fold
---

## Running down a collection of objects

Before we start with map, let's take a very quick detour and see how we can define functions (or methods inside a class which we'll see in a later post):

# Defining functions

``` scala
scala> def doSomething(x: Int): Double = pow(x, 5)
doSomething: (x: Int)Double
```

Well, I kinda lied to you there. You need to `import math._` before you can use the `pow()` method from the `math` package. The `._` instructs the compiler to get everything that's publicly exposed available in the `math` package.

Let's run through that one line function and the function `type signature` that follows it (the scala interpreter generates it for us). Here are the important points:
  1. `def` is how you tell the compiler that it is the start of a function definition.
  2. `doSomething(x: Int)` is the function name along with the list of arguments it takes and their types. The type of `x` is `Int` here.
  3. The last part of the definition is the return type. You don't always need to provide the return type but, it is a good practice (The compiler will tell you when you need to and you forgot but, don't forget. It helps in writing clean code that NEVER breaks!) In this case, the return type is `Double`.
  4. The things after the `=` sign constitute the body of the function. Yes, you guessed it, if the body is more than just one line, you can use the `{ }` to keep them in a code block.
  5. Notice that there is no `return` statement. The function would just return the result of the last line. Be careful that this should match the return type declared in your function definition.

# Maps are more than just for cartographers!

Think of the `mapping` operation as this: Run down a collection, taking one element at a time, and pass the elements as an argument to the mapping function.

``` scala
scala> (1 to 4) map doSomething
res1: scala.collection.immutable.IndexedSeq[Double] = Vector(1.0, 32.0, 243.0, 1024.0)
```
You would remember from yesterday that `(1 to 4)` is a collection. Well, if you forgot, just put it in the RePL and see what it is!

``` scala
scala> (1 to 4)
res4: scala.collection.immutable.Range.Inclusive = Range 1 to 4
```
Neat!

# Let's jump to fold now!

`fold` is interesting! To demonstrate `fold` let's be nice and give a name to a collection:

```scala
scala> val list = List(1, 2, 3, 4)
list: List[Int] = List(1, 2, 3, 4)
```
By now, you should be comfortable with understanding the type that the RePL prints for us.

``` scala
scala> list.fold(0)(_+_)
res11: Int = 10
```
Here's what this weird looking fellow is doing:
  1. `fold` is taking 2 `parameter lists`! The first one is the number `0`, the second is the function `+`. You might find the `_+_` weird but, this is an `infix` notation for the function `+` which takes 2 arguments. We don't care to name the arguments here so we just used a `_` -> anything goes!
  2. The first argument list - `(0)` - is called the `accumulator`. (See it yet?)
  3. What `fold` is doing is, it is taking one element of the collection at a time -> passing that element and the `accumulator` to the function given in its second argument list. This function's return value then acts as the `accumulator` for the next iteration!

We "looped" through the whole list and added the elements!

# Caution (or Joy?)
`fold` will not go through the list in any particular order. It is essentially an async operation. If you are doing something with the list that requires a particular order to be preserved you can use `foldLeft` or `foldRight`!

This post is already quite long! But hey, we wrote just ***4 lines of code!*** That's the joy of Scala, it makes your code very concise and therefore easy to debug, if something goes wrong!

# Exercises
  1. Try creating functions that are more than one lines of code!
  2. Can you think of (and write!) some function that might give different results for `fold`, `foldLeft` and `foldRight`?
  3. Change the return type of your functions to induce an error and read the exception.
  4.

Check out this cool resource from [Twitter][twitter-collections] for more on collections and what can be done with them!

[twitter-collections]: https://twitter.github.io/scala_school/collections.html
