---
layout: post
title: "Phase 2: Week 2: Day 1 - JavaScript"
date: 2014-02-25 13:24:24 -0800
comments: true
categories: 
---

**8:00 - Arrive**

A morning lecture on the wonders of jQuery ... and how we are to avoid at all costs crazy long chains of doing things in our code. We want to be thoughtful of the people who will read/edit our code in the future. So what do we do? Clean it up, then wrap it in a descriptive callback method!

jQuery is a JavaScript library that's supposed to simplify client side scripting of HTML. In English (well closer to English) that means it's easy to grab elements in the DOM, create animations and capture events (mouse clicks, keyboard actions, etc) and map those to different actions.  The [jQuery documentation](http://api.jquery.com/) is very very thorough, and worth looking at if you want to learn more.

The syntax is kind of funky - it almost looks like chaining methods in Ruby... but on steroids.  

```javascript
$(document).ready(function() { //when the page is done loading do the function
  $("div").fadeOut(1000);  //this captures all div tags & has them fade out, 1000 is time in milliseconds
});
```

The above action could generically be written out as

```javascript
$(document).ready(function() {
  // jQuery "magic"
});
```
So if you wanted to chnage the background color of a class `.lead`, you'd type

```javascript
$(".lead").css("background-color", "orange");
```
Take a nice long look at what is in `" "`.

Wait, colors are too boring for you? Let's replace some boring images that are already in there

```javascript
$("img").attr("src", "http://imgur.com/superamazingimage.jpg")


// if there are a ton of images and you only want to replace the first one

$("img:first")...
```

Ok, bear with me, what if we wanted to select elements from the navbar and use the `.on() ` method to bind an event handler on these elements?

```javascript
$(".nav").on("mouseenter", function(){
  $(this).css("background-color", "#FF0000");
});

$(".nav").on("mouseleave", function(){
  $(this).css("background-color", "#FFFFFF");
});
```

And that's a micro-intro to jQuery. PSA: if you are actually a VIP in the insane chaining club for jQuery. Take a step back, remove your sunglasses, rip up that VIP card, and step into the light. Everything will be ok.



##JavaScript (JS)

you don't always need jQuery though, Steven (one of our instructors and a fellow Longhorn) would argue that you don't ever need it.  And if you don't believe him, you can head on over to [youmightnotneedjquery.com](http://youmightnotneedjquery.com).

Our intro to JS is done in with OO in mind, using Ruby as a basis and taking our knowledge and logic from Ruby and applying it to JS.

What makes a Class a class?  

* Initializer function
* Attributes
* Methods

JavaScript has something akin to "Open" Classes, we open a class and bolt behavior onto it.

```javascript
function Talker(word) {  // like a class - it's a Constructor Function
  this.word = word; // instance method equivalent
}

Talker.prototype.sayHello = function() { // an Anonymous prototype
  console.log("Hello " + this.word); // behavior
}

var en_espana = new Talker("mundo"); // instance of Talker
en_espana.sayHello();
var en_la_france = new Talker("le monde"); // instance of Talker
en_la_france.sayHello()
```

Well, that makes some kind of sense now doesn't it!? 

##What about initialize methods in a class, Ruby has those, what about JS?

If we look at tthis line, it is JS equivalent of an initialize method.  An instance of Talker is born with knowledge of #word.

```javascript
this.word = word;
```

Set Attributes

Define methods on the thing's prototype - this exactly what we did with `Talker.prototype.sayHello ...`


Two ways to define an object in JS, with the object constructor or the literal syntax

```javascript
var anObject = new Object();  // constructor
var anotherObject = {}  // literal

console.log(typeof(anObject));
console.log(typeof(anotherObject));
```

##Name spacing

Take a look at these 2 methods, `.sin()`

```javascript
Trig.sin()

Morality.sin()
```
Even without knowing anything about what they do, you can probably surmise that they do *very* different things. **Name spacing** allows us and the computer to organize things accordingly.  Yeah, it's important.


**10:45pm - Depart**

>The sole justification of teaching, of the school itself, is that the student comes out of it able to do something he could not do before. I say do and not know, because knowledge that doesn't lead to doing something new or doing something better is not knowledge at all.  
- J. Barzun