---
layout: post
title: "Phase 2: Week 2: Saturday"
date: 2014-03-02 01:40:15 -0800
comments: true
categories: 
---

**11:45am - Arrive**

Work on Group project

and also portfolio challenge 7

our challenge:

Modify the shell code to implement the following functionality:

* Clicking on the 'Click Me' button submits an AJAX request to the '/colors' route
* return a JSON object the server with a random color and cell number
* change the background color of the cell number returned to the color - WITHOUT MODIFYING THE HTML


We use jQuery to put an event handler on the button, which has an ID '#get_color' on a click. Then we use AJAX to handle the action - by going to our controller and going to the correct route 

and on success, a cell object is passed back and we act on all list items <li> and then with the .eq() method we constructs a new jQuery object from the element within that set, then we change the css of the background to a random color that's passed to us from the return value given to us from the controller.

```javascript
$(document).ready(function(){

  $("#get_color").on("click", function() {
    $.ajax({
    	url: '/color',
    	type: 'post',
    	success: function(cell) {
    		$('li').eq(cell.cell - 1).css("background", cell.color)
    	}
    })
  })

});
```

what about the object that AJAX is returning?

We turn it into a JSON object!!

```ruby
post '/color' do
  content_type :JSON
    {cell: rand(1..9), color: "#" + "%06x" % (rand * 0xffffff)}.to_json
end
```

**1:00am - Depart**

>Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live.  
- M. Golding