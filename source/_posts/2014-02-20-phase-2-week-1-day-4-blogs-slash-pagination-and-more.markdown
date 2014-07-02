---
layout: post
title: "Phase 3: Week 1: Day 4 - Blogs/Pagination &amp; more"
date: 2014-02-20 21:11:08 -0800
comments: true
categories: 
---


**7:30am - Arrive**

Recall that HTTP is statless, so "sessions" were invented.  A session keeps state during HTTP requests, and a session actually stores all data in a cookie.

In Sinatra, the session data in this cookie is 'signed' with a session secret, it's the default AND it's randomly generated every time you start Sinatra, though you can set it to a non-changing value.

A client makes an HTTP request to the server. The server responds to the client and drops a cookie on/in the client's browser. Once the cookie is dropped, every subsequent request from the client has the cookie.

Yes, there are exceptions that can be made and you can always manually clear cookies

A session in not a hash, but it is treated like a hash in syntax. `session[:color]`

In Sinatra, you must enable sessions with a simple...

```ruby
enable :sessions
```

12:30pm - Yoga and lunch

## Debugging

2 major types:

1) Binary Search, whose efficiency in narrowing down the problem is `n log n` 

2) Find "seams" between layers


##Portfolio Challenge 1


### I'd like to have more detailed blog posts, but phase 2 is crammed with work and it won't slow down anytime soon.

**1:00am - Depart**

>Chance favors the prepared mind.  
-Louis Pasteur