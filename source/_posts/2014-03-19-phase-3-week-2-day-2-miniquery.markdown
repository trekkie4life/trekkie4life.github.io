---
layout: post
title: "Phase 3: Week 2: Day 2 - miniQuery"
date: 2014-03-19 08:47:30 -0700
comments: true
categories: 
---

**8:30am - Arrive**

So what's the deal about miniQuery? It's using vanilla JavaScript to build certain functions of jQuery - the purpose? So we become enlightened and unafraid of jQuery under the hood and come to the realization that we can understand it and create it... to empower us and give us faith in our ability.

In addition to that, one cool thing we learned about today in JavaScript - hidden methods - the common indicator is to add an underscore in front of a method name.

In the code below if we call

`SweetSelector.sweetness` the only thing that gets returned is `_sweetSelector()` but we can't actually see what `_sweetSelector()` is doing. Pretty cooool!

```javascript
var SweetSelector = (function(string){
//getelementsbyclassname

  var _sweetSelector = function(string){
    var splitString = string.split("")
    if(splitString[0] === '.'){
      splitString.splice(0,1)
      var className = splitString.join("")
      return document.getElementsByClassName(className)
    }
  //getelementbyid
  //getelementsbytag
  }

  return{
    sweetness: function() {
      _sweetSelector();
    }
  }
}())

```

We had trouble when modifying an HTML display property, our miniQuery could set the display property to none, but when we showed it, the default/initial display property vanished into thin air. This really bothered us, but since we were on a time crunch we moved on -- ONLY AFTER we took a dive in the jQuery source code to see how they did it.

The way they took care of that was to have a single method showHide with logic inside that hid a class/id/target but holds the display property in a variable and then sets `display: none` if it's `show` then it checks to see if there was an initial display value, if so it sets `display` to that, if not, then it gets the default display property of other elements of that type on the page.

My take away? Well played, Steven and Shadi, it's not magic and we can create it and understand it.



**12:15am - Depart**

>If you're not failing every now and again, it's a sign you're not doing anything very innovative.  
- W. Allen