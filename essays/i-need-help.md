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

### Question

In the example below, childOfNumbers is correctly inferred to be Child<number>. However, my issue is childOfStrings is inferred to be Base<string>. Is it possible to have a parent return the subclasses type such that childOfStrings is inferred to being Child<string>?

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

The question posed above seems to be a fair question, no? However, why is it that no one responded to this post - let alone an answer to the problem? The reason is that the user did not show to be an individual who is willing to learn. Rather, the context provided by the user shows that they ran into a problem and wants to know the solution with no attempt in finding the answer themselves. Simply put, this is tantamount to laziness. As such, no reply was ever made despite the significant number of online users that had viewed it and could have easily provided an answer.

## The Right Way

Let's take a look at another user's question:

### How to sum up numbers across inventory?

CSV files on each host contain certain figures and I need to add them all up.

To that end, I find the matching files first, and invoke awk to parse the CSV content and output the per-host total.

Where I'm stuck is summing up the totals across all machines:

```
- hosts: all
  gather_facts: False
  tasks:
  - name: Find input
    find:
      path: /somepath
      pattern: 'logbatch*.txt'
      recurse: True
    register: found
  - set_fact:
      inputs: "{{ found.files | map(attribute = 'path') }}"
  - command: >-
      awk -F, '{ t += $NF } END { print t }' {{ inputs | join(' ') }}
    register: total
  - debug: var=total.stdout
  - debug:
      msg: >-
        {{ hostvars | json_query('[].total.stdout') }}
    run_once: True
```

The first debug outputs each machine's total, as expected.

I then expected to pipe the output of json_query into sum, but the json_query returns a None (which debug then outputs as empty string).
[Source](https://stackoverflow.com/questions/79762347/how-to-sum-up-numbers-across-inventory)

Despite being posted the same day as the previous post, this user has not just garnered more views due to a more interesting title, but more importantly, received a reply answer as well. This indicates that a more properly-phrased question gives way for more clarity in the problem and the 

## Conclusion

The juxtaposition is clear to see in the way both users phrased their questions. 
