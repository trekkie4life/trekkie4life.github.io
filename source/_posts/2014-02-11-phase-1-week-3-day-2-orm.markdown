---
layout: post
title: "Phase 1: Week 3: Day 2 - ORM"
date: 2014-02-11 07:51:04 -0800
comments: true
categories: 
---

**7:40am - Arrive** 

Get out of your comfort zone. It's important in a situation where you want to grow, learn and evolve as a human being, regardless of age. That holds true for programming as well. 

![Where the magic happens, it's true, give it a try](http://i.imgur.com/hu32GdW.jpg)


**The Law of Demeter** - a set of coding rules (strong suggestion, emphasis on strong) that results in the creation of loosely coupled objects. A unit/object (class or method) should have only limited knowledge about other units, those others being only units "closely" related to the current unit/object.  
  
Basically, try to make your classes single responsibility and your methods as well. That doesn't mean only one method to a class, but rather you want to be sure your class is highly cohesive... that everything in it is related to its central purpose.

##Object Relational Mapper (ORM)

Build our own ORM that mimics some common features of ActiveRecord. Why not just learn to use RSpec right off the bat? Because we should understand that RSpec is just Ruby, written in a certain way to have its own dsl (domain specific language). RSpec is not magic, we ***CAN*** and ***SHOULD*** know what's going on under the hood when we take a peak. It's important as n00bs to develop proper habits now rather than having to unlearn bad ones and re-learn good ones.

- - - 
If we run some code in Ruby...

```ruby
Database::Model.execute("PRAGMA table_info(students)")
```
... that returns meta-data on a database table...

```ruby
[{"cid"=>0, "name"=>"id", "type"=>"INTEGER", "notnull"=>1, "dflt_value"=>nil, "pk"=>1}, 
 {"cid"=>1, "name"=>"cohort_id", "type"=>"integer", "notnull"=>0, "dflt_value"=>nil, "pk"=>0},
 {"cid"=>2, "name"=>"first_name", "type"=>"varchar(255)", "notnull"=>0, "dflt_value"=>nil, "pk"=>0},
 {"cid"=>3, "name"=>"last_name", "type"=>"varchar(255)", "notnull"=>0, "dflt_value"=>nil, "pk"=>0},
.
.
.
```
... which is an array of hashes where each hash corresponds to a field in the database, and we want only the values of each hash's "name" key, we'd want to iterate over the array of hashes using #map like so...

```ruby
@attribute_names = pragma.map { |col_hash| col_hash["name"].to_sym }
```

###Remember: TEST BEHAVIOR, NOT IMPLEMENTATION



**10:45pm - Depart**
  
>You don't understand anything until you learn it more than one way.  
- Marvin Minsky