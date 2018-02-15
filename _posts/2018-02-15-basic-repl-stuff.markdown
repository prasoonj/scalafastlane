---
layout: post
title:  "#1. Explore the RePL"
date:   2018-02-15 08:56:05 +0530
categories: Basic
description: This post does some very basic stuff with the Scala RePL.
tags:
  - scala
  - repl
---

``` sh
$ scala
scala> val x = "hello"
x: String = hello
```
The `x` above is a `val`, meaning, if you try to assign any other value to `x`, you would get an error. These are Scala’s immutable. We have assigned a String value to this val which is what the Scala interpreter prints out for you.

`x: String //This is how we define objects to be of a certain type.`

## Exercises:
1. See what happens if you try to re-assign a value to this val.
2. What happens if you don’t use the keyword ‘val’?
3. Carry out other type assignments - Int, etc.


Check out the [Scala Documentation][scala-docs] for more on the RePL!

[scala-docs]: https://docs.scala-lang.org/overviews/repl/overview.html
