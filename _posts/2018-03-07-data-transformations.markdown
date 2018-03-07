---
layout: post
title:  "#6. Data Transformation as a Design Principle"
date:   2018-03-07 19:18:05 +0530
categories: Basic
description: Understanding data transformations in Scala.
tags:
  - scala
  - data transformations
  - functional programming
---

If I were asked to name the most important idea of Functional Programming, I would certainly say it is Data Transformation! I'm no expert in Category Theory but, I think it derives quite naturally from there - using functions to combine/convert one category to the other using algebra defined on them (I would really love some inputs here!)

Category Theory aside, if you look at any imperative language that's trying to mimic a functional way, the thing they start with are ways to do data transformations. We've already seen `for` comprehensions and, `map` and `fold` in earlier posts. In this post, let's try to see if we can find some ways to spot if we are missing the mark and writing Scala in the Java way (anti-patterns)!

1. Use of `var`: If your code is using `var`, chances are that you are not using the full power of data transformations.
2. Shared state: This usually is a result of the first point. If you have a `var` or `val` declared at a global level in your code and there are functions that are manipulating this shared state, there is a problem that can be solved by transforming the data and passing it around in functions.
3. Functions with zero parameters: Yes, again in the same vein, this anti-pattern hints to the possible use of transforming data.

The above is not an exhaustive list of course but, those are points that are easy to spot and correct.

A neat trick to understand is that in functional programming, you don't need to pass data around back and forth between different functions - that's what the functions are for! Create small functions that work on a single piece of data and `map` them over a collection to get a different collection!

# Exercises
  1. Check out the [post on `map` and `fold`](url:https://prasoonj.github.io/scalafastlane/2018/02/16/basic-map-and-fold/) and see if you feel more confident about that topic!
  2. `map` is basically `for` under the surface! Read up the [previous post](url:https://prasoonj.github.io/scalafastlane/2018/02/17/basic-conditions-looping-for-comprehensions/) on that topic and work out the exercises again to see if you are able to do them better!
