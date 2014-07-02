---
layout: post
title: "Weekend Review"
date: 2014-02-09 20:12:55 -0800
comments: true
categories: 
---

Sunday morning errands to get some food for the first couple days

11:00am - Arrive

OOP (Object Oriented Programming)

Reading Practical Object Oriented Design for Ruby - affectionately referred to as "POODR" (pooh-der).

One problem we had was trying to keep the code DRY (Don't Repeat Yourself) in regards to our Fruit class and the classes that inherited from it. We wanted to have different fruits (Apples, Oranges, Pears) be initialized with different diameters. For awhile we couldn't figure out how to do that without repeating the code containing the diameter instance variable, until...

Solution: passing an argument into **super** so the Superclass receives it.  I didn't know super was capable of that. Ruby, you are so nifty and great.

Brain, grow more neurons to retain this nugget.

```ruby
# Initializes a new fruit with diameter +diameter+
class Fruit
  attr_reader :diameter
  def initialize(diameter)  # initialize takes an argument from super
    @diameter = diameter
  end
end

# Initializes a new Orange with diameter +diameter+ (of random size)
class Orange < Fruit
  def initialize
    super(1 + rand(4)) # super takes an argument - 
  end
end
```


9:30pm - Depart