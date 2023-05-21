---
title: "How I make random decisions that do not matter"
date: 2023-05-18T19:43:05+02:00
tags: [Mathematics, fun]
---

If the decision is binary then a simple coinflip will do. Otherwise, one would need to pull out a random number generator. I typically make these unimportant decisions quickly using my phone's clock and [modular arithmatic](https://en.wikipedia.org/wiki/Modular_arithmetic) (my favourite operator). The idea is to take the minute ($m$) on your phone clock as the input to $f(m, n) = m \mod n$, where $n$ is the number of unique choices you have.

Let's pretend you are in Germany and were given 5 different pieces of cake that look equally amazing, but you only want to have one. You look at your phone and see it is `15:39`. Therefore:

$$39 \mod 5 \equiv 4$$

so you take the rightmost cake since we number them from left to right $0, 1, 2, 3, 4$.

For simple decisions you typically have less than 60 options so the minute should be good enough, seconds are not used because they change too quickly.
