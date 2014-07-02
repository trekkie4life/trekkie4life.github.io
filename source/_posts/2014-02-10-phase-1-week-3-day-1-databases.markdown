---
layout: post
title: "Phase 1: Week 3: Day 1 - Databases"
date: 2014-02-10 23:15:10 -0800
comments: true
categories: 
---

**8:00am - Arrive**

##"What excites you about programming?"
The ability to create and reach 39 (and growing) percent of the world's population.  

Below the vertical axis is percentage of world's population, horizontal axis is years.

![world internet usage graph](http://upload.wikimedia.org/wikipedia/commons/2/29/Internet_users_per_100_inhabitants_ITU.svg)
  
It's time to think about programming in this way:  
###I have a need. I want to express it. How do I do it in this/that language? 

##Database Schema and PostgreSQL

A self join is when a foreign key and the primary key it points to are in the same table.  In the pic below you'll notice we are showing that a user comment can be a reply to an earlier user comment.  We use a self join to make it a reality.  It's nice to find the beauty in simple things.  
  
![Always whiteboard your schema. Always. No exceptions.](http://i2.minus.com/iJUPUs3sj1qYx.jpg)  

Rule one of databases - always illustrate your tables and how they relate to one another. Don't try juggling that stuff in your head. If it's a few tables, it might be ok. If it's hundreds of tables, not such a good idea. Build good habits now.  

Soon it was time to implement some databases in PostgreSQL via Ruby.

Step 1 - remember to require postgres

```ruby
require 'pg'
```  

Step 2 - don't be afraid of using a hash as an input parameter  

```ruby
class Student

$db = PG.connect( dbname: 'students' ) # allows us to save time when accessing the db

  def initialize(args = {})
    @first_name = args[:first_name]
    @last_name = args[:last_name]
  end
```  
Step 3 - use binding variables to protect against [SQL injection](http://en.wikipedia.org/wiki/SQL_injection). In SQLite it's a '?' instead of '$1' or '$2' (and so on). $1 refers to the element at index 0, $2 refers to the element at index 1 (etc, etc) of the array the variable is bound to.

```ruby
  def save
    $db.exec("INSERT INTO students (first_name, last_name, created_at, updated_at)
        VALUES ( $1, $2, DATE('now'), DATE('now'))", [@first_name, @last_name])
  end
  
student = Student.new ({first_name: 'Armando', last_name: 'Reed'})  # notice the hash we pass in
student.save  
```
  
The second mission for today is to learn more about testing so when we tackle ActiveRecord and RSpec we won't think it's magic but that we'll understand what it's doing.  


**10:40pm - Depart**
  
>The good thing about reinventing the wheel is that you can get a round one.  
- Douglas Crockford