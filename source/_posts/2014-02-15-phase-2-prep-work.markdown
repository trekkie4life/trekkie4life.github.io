---
layout: post
title: "Phase 2 - Prep Work"
date: 2014-02-15 10:48:48 -0800
comments: true
categories: 
---
Chores around the house and some reading then it was time to head out to DBC

**1:45pm - Arrive**

##Git version control


```ruby
$ git rebase -i
```

`git rebase -i` allows you to:  

* rewrite commits
* remove commits
* combine commits
* reorder commits

The benefit is almost immediately obvious - you can write short/sweet commits locally to keep your work flow going smoothly, then use `git rebase -i` *before* pushing the commits anywhere to rewrite those commits into a unified and cohesive story that we can then share with our team, future self, and anyone else who comes along.

First: use `git log` to find the commit you want to change

Next: run `git rebase -i [the commit's hash]`

###a quick break for San Fran's Chinese New Year parade
Marching bands, drum lines and dragons  

##JavaScript intro
  
Programming in a new syntax - utilizing the skills/knowledge and applying it to a new language. The beauty of logic.
  
**For loop** syntax:  
`var i = 1;` is the counting variable and the starting value of that variable.  
`i < 11;` do the loop until this condition is met.  
`i++` the counter.  
  
```javascript  
for (var i = 1; i < 11; i++) {
  console.log(i);
}
```
Here's another example on printing strings from an array:

```javascript
var cities = ["NYC", "SF", "ATX", "Maui"];

for (var i = 0; i < cities.length; i++) {
  console.log(cities[i]);
}
```
**While loop** syntax

```
while (condition) {
  //do something
}

//an example of a while loop
count = 0;

var loop = function() {
  while (count < 3) {
    console.log("I'm looping");
    count += 1;
  }
};

loop();
```  

**Do / While loop** syntax  
```javascript
do {
  //do something
} while (loop condition);
```
  
**10:35pm- Depart**

>The only difference between science and screwing around is writing it down.  
- Adam Savage