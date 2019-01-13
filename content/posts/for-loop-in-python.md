---
title: "For Loop in Python"
date: 2019-01-14T00:52:11+08:00
draft: true
categories:
  - random
---

This article is about `for/else` in Python, and how to use it to break/continue looping.

In Python, doing something with `for` loops looks like:
```python
fruits = ["apple", "banana", "pear", "kiwi"]
for fruit in fruits:
    print("I like %s\n" % fruit)
```
The output is:
```shell
I like apple

I like banana

I like pear

I like kiwi
```

Easy, right?

Sometimes things get complicated.
For example, I can use `if/else` statements to specify the fruit I don't like:
```python
fruits = ["apple", "banana", "pear", "kiwi"]
not_my_type = ["pear"]

for fruit in fruits:
    if fruit not in not_my_type:
        print("I like %s\n" % fruit)
    else:
        print("I don't like %s\n" % fruit)
```
The output is easy to imagine:
```shell
I like apple

I like banana

I don't like pear

I like kiwi

```

What if I want to do something after the loop completes normally?
Use `else` clause.
```python
fruits = ["apple", "banana", "pear", "kiwi"]
not_my_type = ["pear"]

for fruit in fruits:
    if fruit not in not_my_type:
        print("I like %s\n" % fruit)
    else:
        print("I don't like %s\n" % fruit)
else:
    print("Loop over the fruits successfully!")
```
The output is:
```
I like apple

I like banana

I don't like pear

I like kiwi

Loop over the fruits successfully!
```

## When should I use `for/else` clauses?

Its usage is not that intuitive, test your knowledge of `for/else` clause with
the following codes:
```python
fruits = ["apple", "banana", "pear", "kiwi"]
not_my_type = ["pear"]
while True:
    for fruit in fruits:
        if fruit not in not_my_type:
            print("I like %s\n" % fruit)
        else:
            print("I don't like %s\n" % fruit)
    else:
        continue
    print("Loop over the fruits successfully!")
    break
```
Imagine what the output should look like...

<br>
<br>
<br>

_It is an infinite loop!_

In the above codes, the `for` loop never encounters a `break` statement.
As the result, the `else` clause executes after the `for` loop completes.
`continue` then causes the `while` loop continues on with the next iteration
and skip the rest of the code inside the loop.

It is useful when you want to run a loop forever and only break the loop when a
condition is met. For example:
```python
fruits = ["apple", "banana", "pear", "kiwi"]
not_my_type = ["pear"]
while True:
    for fruit in fruits:
        if fruit not in not_my_type:
            print("I like %s\n" % fruit)
        else:
            print("I don't like %s\n" % fruit)
            break
    else:
        continue
    break
```
In the above codes, the loop broke in the iteration of `pear` and thus the
`else` clause is never executed. The program continues to the next line of code
in the `while` loop and terminate the `while` loop. The output is:
```
I like apple

I like banana

I don't like pear
```
If "pear" is removed from the list, then the loop will run forever.
```python
fruits = ["apple", "banana", "kiwi"]
not_my_type = ["pear"]
while True:
    for fruit in fruits:
        if fruit not in not_my_type:
            print("I like %s\n" % fruit)
        else:
            print("I don't like %s\n" % fruit)
            break
    else:
        continue
    break
```

To show the usage of `else` clause, here's an example from [Python Tips](http://book.pythontips.com/en/latest/index.html):

```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print( n, 'equals', x, '*', n/x)
            break
    else:
        # loop fell through without finding a factor
        print(n, 'is a prime number')
```
As an exercise, imagine what the output should look like...

<br>
<br>
<br>

```
2 is a prime number
3 is a prime number
4 equals 2 * 2.0
5 is a prime number
6 equals 2 * 3.0
7 is a prime number
8 equals 2 * 4.0
9 equals 3 * 3.0
```

Alright, that's enough procrastination for me today.