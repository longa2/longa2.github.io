---
layout: essay
type: essay
title: "I Need Help!"
# All dates must be YYYY-MM-DD format!
date: 2025-09-11
published: true
labels:
  - Software Engineering
  - Stack Overflow
  - Questions
---

<img width="200px" class="rounded float-start pe-4" src="../img/i-need-help-quote.jpg">

*"Never underestimate the power of stupid people in large groups." ~ George Carlin*

## Any Questions?

Questions have always been a long-standing way of searching for answers to the problems around us in day-to-day life. So what happens when you ask one? Do you get an answer as expected? In some cases, sure you can. But, in other cases, there are questions unanswered - or better yet - there already is an answer and no one is bothered to answer it for you.

## The Wrong Way

When someone asks a question, they are seeking a solution. Ususally, it is so. But sometimes, people ask not to seek a solution to a problem, but rather in redundancy. Take for example this user:

"In the example below, childOfNumbers is correctly inferred to be Child<number>. However, my issue is childOfStrings is inferred to be Base<string>. Is it possible to have a parent return the subclasses type such that childOfStrings is inferred to being Child<string>?"

Code
```
abstract class Base<T> {
    public items: T[] = []
    constructor(items: T[] =[]) {
        this.items = items;
    }
    abstract createInstance<U>(args: U[]): Base<U>;
    map<U>(fn: (value: T, index: number) => U): Base<U> {
        return this.createInstance(this.items.map((v, i) => fn(v,i)))
    }
}

class Child<T> extends Base<T> {
    override createInstance<U>(args: U[]): Base<U> {
        return new Child(args)
    }
}

const childOfNumbers = new Child<number>([1,2,3]);
const childOfStrings = childOfNumbers.map((v,i) => v.toString())
```
[Source](https://stackoverflow.com/questions/79762418/return-subclass-type-from-parent-function)
