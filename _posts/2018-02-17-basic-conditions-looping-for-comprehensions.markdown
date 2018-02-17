---
layout: post
title:  "#4. Conditions and looping vs comprehension"
date:   2018-02-17 07:18:05 +0530
categories: Basic
description: Conditions and more looping versus comprehension.
tags:
  - scala
  - iteration
---

We've already seen some looping in the earlier posts. Today, let's talk about 3 concepts together that cement one important idea about a functional language that we've seen a glimpse of but, which we didn't bother to define properly - ***side effects***.

We said that Scala has expressions meaning, constructs that, after doing their stuff, return a certain value. Compare that with statements like `if statements` in other languages - they produce what are called ***side effects***. Programming is all about __composing__ smaller pieces together to form bigger ones. With that in mind, if a `statement` that does not return anything is used, we can never be sure how including it as a compose-able piece will affect the overall behaviour of our code. Avoiding such statements hat produce ***side effects*** is one of the major push that functional programming languages like Scala drive for. But, you do need these ***side effects***, if you just compose and do nothing, your program is useless! When we code in a FP language, we try to limit such side effects to controlled parts of our code and try to achieve "pureness" everywhere else.

With that introduction, let's see what the `if` can do for us in Scala that it cannot in other languages like Java. Well, it can return something!

``` scala
scala> :paste
// Entering paste mode (ctrl-D to finish)

def howIsTheMorning(day: String): String = if(day == "Sunday"){
  "Beautiful Morning!"
} else {
  "Meh!"
}

// Exiting paste mode, now interpreting.

howIsTheMorning: (day: String)String

scala> howIsTheMorning("Sunday")
res12: String = Beautiful Morning!

scala> howIsTheMorning("Monday")
res13: String = Meh!

scala> howIsTheMorning("Saturday")
res14: String = Meh!
```

Notice how you can use the Scala RePL to enter the paste mode when you need to write functions that span more than one line!
The important thing to note here is that your `if` and `else` blocks are not just doing stuff like printing values or calling databases or whatever, they are returning values that can be used to ***compose*** bigger blocks!
There's certainly one problem here - ***Saturday*** morning are beautiful too! Let's fix that while making it more robust!

``` scala
scala> val days: List[String] = List("Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday")
days: List[String] = List(Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday)
scala> :paste
// Entering paste mode (ctrl-D to finish)

def howIsEachDayOfTheWeek(week: List[String]): List[String] = for {
  day <- week
  if (day == "Sunday") || (day == "Saturday")
} yield (s"$day is Beautiful!")

// Exiting paste mode, now interpreting.

howIsEachDayOfTheWeek: (week: List[String])List[String]

scala> howIsEachDayOfTheWeek(days)
res19: List[String] = List(Sunday is Beautiful!, Saturday is Beautiful!)

```
Here, we've added, what are called ***guards***. The `if` condition that __guards__ what gets filtered out and becomes available for the `yield`. We've learned quite a bit of terminology today, let's add just one more to it before we finish - ***for comprehension***.
A good way to remember when a `for` construct results in a ***comprehension*** (as opposed to a ***loop***) is to see what the `for` does -- ***if `for` results in a side-effect it is a loop, if it results in another collection, it is a comprehension***.

__Phew!__ This was a long one! Let's do some quick exercises so we don't forget what we learned!

# Exercises
  1. Change the `howIsEachDayOfTheWeek` function to print the better days of the week instead of yielding them. Hint: The function's return type would be `Unit` in that case.
  2. Play around with ***guards***. Add more of them in the `for` expression.
