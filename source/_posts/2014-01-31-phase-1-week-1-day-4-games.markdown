---
layout: post
title: "Phase 1: Week 1: Day 4 - Games"
date: 2014-01-31 02:00:49 -0800
comments: true
categories: 
---

![communication](https://github-camo.global.ssl.fastly.net/263edda0ba67654c5e68725c981d6701c0f4b8eb/68747470733a2f2f736f6372617465732e646576626f6f7463616d702e636f6d2f6173736574732f747265655f636f6d69632e6a7067)

How can you not love the above picture - it's correct on so many levels!

**8:00am - Arrive**

Diving into games! Scary and fun at the same time.

First up: Pig Latin

take an input string

IF the string starts with a vowel, return the word (unchanged)
ELSE set the consonants at the of the word and add the suffix "ay"
PRINT the pig-latin-ified word
The best way in my mind would be to use RegEx, and that's exactly what happened.

For the first example.


```ruby
if normal_word =~ /\A[aeiyou]/
p normal_word
```

=~ \A  means the search MUST start at the beginning of the string.

[aeiyou] the square brackets mean that a positive match will occur if the first letter (in this case) is one of the characters in the brackets - like “a” or “e” or “i” or “y” or “o” or “u” is the first letter, then *BING* we have a match

```ruby
  else
    p normal_word.gsub!(/(^[^aeiyou]*)(.+)/, ”\2-\1ay”)
  end
```
You’ll notice 2 pairs of paranthesis.

```ruby
/(^[^aeiyou]*)(.+)/
```

the first hat ^ acts the same as \A

inside the [ ] the ^ acts as “NOT”

\* after the right bracket ] means to end that search there

the second pair of brackets assigns the result of that search to a second group.

the period means to match any character, the + means “one or more”

\#gsub!(this is what we are searching for, replace it with this)

will destructively match and replace the match. There’s a special syntax when you use those captured groups

```ruby
“\2-\1ay”
```

When the group is inside double quotes, we have to have \ preceding the group number. \2 refers to group two, \1 refers to group one.

 

So here, we’d have group two followed by a dash, then group one, followed by “ay” with no white-spaces separating them.

DBC Yoga - especially good

AHA Moments!

Linked Lists:

the pointer points to the entire object, not just the value
object within an object within an object - on and on until the end of the list

![Linked Lists](http://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/CPT-LinkedLists-deletingnode.svg/380px-CPT-LinkedLists-deletingnode.svg.png)

####Assignment Operators

```ruby
||= 
```

tests left argument for truthiness, if nil or false will overwrite it with right argument.  In the example below, if a is nil or false, it is assigned the value 3  

```ruby
a||=3

a|| a=3
```
**11:35pm - Depart**
>Smart data structures and dumb code works a lot better than the other way around.  
- Eric S. Raymond