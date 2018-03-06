---
layout: post
title:  "#5. Data modelling with Algebraic Data Types"
date:   2018-03-06 07:18:05 +0530
categories: Basic
description: Using ADTs to construct complex data.
tags:
  - scala
  - data modelling
  - ADT
---

Algebraic Data Types always seems like a complicated topic to those who are new to the functional world. So much so that, they avoid using it altogether! The perils of that approach is that the design of the code becomes largely OOPy making it hard to get the benefits of functional programming. In this post we'll see how simple they really are and how to best use them. Let's begin!

# Sum Types (`case class`)

The "Sum Types" ADTs are used when we need to club things of different "shapes" together. In Scala we use case classes to do this. A good example is modelling the users of a website:

``` scala
sealed trait Users
case class AnonymousUser(sessionId: String) extends Users
case class LoggedInUser(userId: String, username: String) extends Users
```
(For now, think of `trait` as another name for an interface. We'll talk about it in detail in a later post.)
In the example above, wherever we want to talk about `Users` in our code, we would be forced to talk about both the types of users - `AnonymousUser` and `LoggedInUser`. These are called "sum types" because of the way they ***combine*** together to produce new things - How many types of users are there? 2!

Another cool benefit of using `case class` is that you get a constructor for free!

``` scala
val john = LoggedInUser("43", "awesomejohn")
val randomVisitor = AnonymousUser("asdfjiberishadsf")
```

# Product Types

The product types can be thought of as a traditional class from the OOP world. When we put a few types together, in one clutch, we get a product type. For example, in the example above, `LoggedInUser` is a product type that holds 2 Strings together. When you read it like this it becomes clearer:
"`LoggedInUser` is made up of a `userId: String` **and** a `username: String`"

# Why do we care?

Well, the proof of the pudding is in data modelling. Product types should feel quite natural if you are coming from the OOP world. The sum types may take a bit of time to adjust to. A good way to think about the sum types is that you are just tagging **absolutely different** things together so that they can be handled via similar logic. A function that takes `Users` would be able to take any of the 2 `case classes` we defined even though the 2 look (and indeed are!) very different.

In that sense, the `trait Users` is not just an `interface` in the traditional sense (adding functionality), it is in fact, a way to tag the 2 different types so that things like **Pattern Matching** become simpler (and possible). A golden rule of thumb in functional programming is to ***say what things are***. That enables us to avoid things like poking inside an object to find a field `isAnonymous` to handle a particular code path.

# Exercises
  1. Think of 5 different scenarios where totally different objects (based on their structures) need to be tagged together as `case classes` with the same tag. (Sum type)
  2. Think of product types that can be "built up" from other sum types.
