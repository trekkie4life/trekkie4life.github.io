---
layout: post
title: "Phase 1: Week 2: Day 1 - Advanced Ruby"
date: 2014-02-03 22:30:31 -0800
comments: true
categories: 
---
##"Something old, something new"
  
**8:00am - Arrive**

 we had 9 challenges today.  I def had a favorite...

####"revisiting Fibonacci"
Instead of merely checking to see if a number is a Fibonacci number, we take an input, say 27, which then returns the 27th Fibonacci number.  Then we do some benchmarking to see whether having the program run iteratively or recursively was quicker! First intro to benchmarking - sweeeeet.

Here's our iterative code

```ruby
def fib_iterative(n)
  fibonacci = [0,1]
  return 0 if n == 0
  return 1 if n == 1

  (n - 1).times do |current_fib_num|
    fibonacci << fibonacci[-2] + fibonacci[-1]
  end
  return fibonacci.last
end

```


Here's our recursive code

```ruby
def fibonacci_recursive(n, prev_fib = 0, current_fib = 1)
  return prev_fib if n == 0
  fibonacci = prev_fib + current_fib

  fibonacci_recursive(n-1, prev_fib = current_fib, current_fib = fibonacci)
end
```

So, which one is faster? What do ***you*** think?  Benchmark it and see if you're right!

**11:07pm - Depart**

>The best way to predict the future is to invent it.  
- Alan Kay