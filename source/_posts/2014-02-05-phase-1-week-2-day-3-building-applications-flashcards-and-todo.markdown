---
layout: post
title: "Phase 1: Week 2: Day 3 - Building Applications (Flashcards &amp; ToDo)"
date: 2014-02-05 22:52:00 -0800
comments: true
categories: 
---

**7:30am - Arrive**

Todo list!  Today one of the challenges was... build a todo list!

We want to be able to interact with the user via the terminal... passing in commands to read and write to an external file.  

```ruby
$ ruby todo.rb add Bake a delicious blueberry-glazed cheesecake
$ ruby todo.rb list
$ ruby todo.rb delete <task_id>
$ ruby todo.rb complete <task_id>

```
  
We had to build the program using the MVC (Model-View-Controller) design method.

The general consensus is that in Ruby the lines are semi-fuzzy between the Model and the Controller.  Apparently this fuzziness clears up dramaticaly in Rails, but since we're not yet using Rails, my partner and I had a discussion and mini-whiteboard session to see if we preferred one way over the other.  Ultimately we decided to have our Model hold not only the data but also the methods for manipulating the data, where our Controller essentially acted as the interpreter for what the View was saying.

One of the early problems we encountered was how to have our program add to the external todo list (txt file) without overwriting what was already in it.  The solution was to use 'a+' with File.open


```ruby
def add_task(task_to_add)
  @your_todo << task_to_add
  File.open('todo_practice.csv', 'a+') { |file| file.write("\n#{task_to_add}")   }
end
```
###Remember: coding in a procedural style defeats the purpose of object orientation

**10:40pm - Depart**

>The question of whether Machines Can Think... is about as relevant as the question of whether Submarines Can Swim.  
- Edsger W. Dijkstra