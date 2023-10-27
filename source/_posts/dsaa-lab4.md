---
title: Data Structure and Algorithm Analysis Lab4 Writeup
date: 2023-10-26 14:00:00
tags: 
 - Queue
 - Stack
categories:
 - Algorithm
---

This is the first post of my blog and I've postponed building the website for years since I feel like getting one. We all need a website to write something, in order to improve our skills.

> Improve (x)  Show off (√)
>
> The truth is:
>
> All dalao have their own blog and to show that I'm one of them, I must have mine. ~~I post this writeup to let you know that I AK this lab.~~

I didn't expect that I got all solved that fast... Anyway, this lab will not be that easy. If you got stuck somewhere, perhaps I can help a little in this writeup. Lets get started.

## 1. Brackets Matching

Classic stack problem

### Description

Given a bunch of brackets e.g. `[(){}]`, decide whether it's matched.

### Solution

At first, we shall convert the brackets into numbers that we can easily recognize, say, in my thought, left brackets will be assigned **even** numbers and right brackets will be assigned **odd** numbers, and matched pair of brackets will be put together. For example:

- `[` : 0
- `]` : 1 
- `(` : 2
- `)` : 3
- `{` : 4
- `}` : 5

Then, `push` into stack if it's even and `pop` out if it's odd, after which compare if their numbers are adjacent. If not, return `No`.

After operating all bracktets, check whether the stack is empty. If so, return `YES` and otherwise `NO`.

## 2. Cinema

Classic queue problem

### Description

A pair of students with same `id` is waiting in two lines to buy ticket. If a student successfully buy the ticket, his/her partner will leave the line immediately. Output the time each team waits.

### Solution

Enqueue the inputs into two queues, and apply two arrays `times` and `bought` to store the waiting time and whether he/she has bought the tickets.

Iterate from $1$ to $n$, dequeue the "bought" ones in two queues and then dequeue one student in both queues, mark them as "bought" and store the $i$ as the waiting time.

## 3. Playroom

More like a evaluation.

### Description

Given a string of matched brackets. The value of `()` is $1$ and value of  `(<brackets>)` is the double value of `<brackets>`. 

### Solution

This problem may be a little tricky, but once you understand how the evaluation of arithmetic expression works, you'll start to think it easy. I will tell the steps first.

Step:

1. iterate the brackets, use a variable `value` to store the current value
2. if it's `(`, the push the `value` and reset it to zero
3. if it's `)`, pop out and plus double `value` if it's not zero, otherwise one, to get the new `value`

Here's how this works:

I will take `( () ( () ) )` for example. To make it clear, I add space between them.

Firstly, I shall introduce a idea, level, which indicates that when brackets are enclosed by the same outer bracket, they are in the same level.

If we encounter a left bracet, we need to store the previous value in stack and reset since the `value` is only for now. And if we encounter a right bracket, which means it's enclosed, we should double the `value` if the bracket enclose something and we should set it to one if the bracket is empty. So, the current value (at the same level) will be `pop()` plus `value > 0 ? 2 * value : 1`.

I will show the value and the stack of the example

**Step 0:** value = 0; stack = 0

**Step 1:** value = 0; stack = 0  0

**Step 2:** value = 1; stack = 0

**Step 3:** value = 0; stack = 0  1

**Step 4:** value = 0; stack = 0  1  0

**Step 5:** value = 1; stack = 0  1

**Step 6:** value = 3; stack = 0

**Step 7:** value = 6; stack = NULL

## 4. Exciting Spider

Classic pop sequence

### Description

Given a sequence of numbers, decide the sequence of pop out with the smallest lexicographical order.

### Solution

The idea uses a bit of greedy algorithm. We can maintain an array to store the minimum values of the rest numbers, say,  Min[i] = min(Min[i + 1], a[i]). So, Min[i] represents the minmum value from a[i] to a[n].

We iterate each item of the sequence. If the current item a[i] < Min[i+1], which means it's the smallest  then pop it right now. Otherwise, we do nothing because we need to pop the big number as late as possible. At the end, pop the rest in stack. Through this, we can ensure that items in stack are decreasing sequence.

## 5. Magic Sequences

Classic sliding window problem

### Description

Given a sequence of numbers and a number m, find the maximum values of all subsequences with length m.

If you don't know what `Deque` is, check [here](https://www.programiz.com/dsa/deque).

### Solution

The algorithm reminds me of a funny saying:

> If your teammate is younger and better than you, you should retire.

If we brute force, the comlexity will be $(n-m-1)m = O(nm)$, which is not acceptable. So I shall introduce a algorithm named Sliding Window Algorithm. It's natrually a kind of queue with special identity.

We uses deque here for convenience. The deque maintain the following identities:

- Front element is the biggest number of current interval.
- Back element is the possible biggest number when moving forward.

The reason why algorithm is called "sliding window" is probably that the we maintain the deque in the interval with constant length, which is similar to moving a window in the slot.

When updating the deque, we do two operations: **a)** if current number is bigger than back element, pop back; **b)** push the current number at the back.

Thus, the steps are obvious:

1. initialize the deque with the first interval.
2. for the rest intervals, update the deque first
3. pop the front elements that don't belong to the current inverval
4. store the answer with the front element

I recommand you store the index of elements in deque rather than the elements themselves.

## 6. Fencing Hall

Another sliding window problem

### Description

Given a sequence of numbers and a number k, find the length of the longest consecutive subsequence whose absolute difference is not greater than k.

*Absolute difference*: the maximum difference of two numbers.

### Solution

We shall uses two deques here because it's the minimum and maximum values of the subsequence that determine the absolube difference of it. So one deque maintains the minimum values while the other maintains the maximum values just as previous problem does.

Iterate the right index of subsequence, and the steps are

1. update both deque
2. obtain the absolute difference throught the deques (min and max values)
3. while the current absolute difference exceeds, move the left index
4. compare the length, update the answer if it's greater

That's all you need to do.

## Epilogue

I will post my codes when the lab ends. After all, I earn my living on them. (
