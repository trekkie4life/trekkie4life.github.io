---
layout: post
title: "DBC - Hackathon"
date: 2014-02-08 11:53:39 -0800
comments: true
categories: 
---
First off, let me say, this was a priceless experience. If you have the choice to do some challenges or go to a DBC Hackathon as a boot... GO TO THE HACKATHON! You will be able to participate and contribute and you'll be exposed to so many things. I just finished Phase 1 - Week 2, and I was still able to make a substantial amount of meaningful input. I loved it.  

**8:45am - Arrive**

After app pitches, we pick which one interests us and converge.  Our team? 5 people: 2 DBC alums and 3 (that includes myself) Phase 1 students.

####Our goal?

I should preface this by saying the Phase 1 students have no JavaScript experience, vanilla or otherwise.

Use JS to build a 9 x 9 board of cells. Randomly generate  (horizontal/vertical)unions between the cells.

Make a Dynamic Connectivity algorithm to see if there is a path that will connect two points, A and B on the board.  We were kind of stuck on the algorithm until a fellow Banana Slug, Quentin (my brother from another mother), came by and gave a great explanation on it.

Animate the algorithm, so we can see it make a path as it goes through various possiblities until it finally reaches the destination cell OR runs out of possible options.

![Recursion](http://i.minus.com/ihuIdgNySiXPd.JPG)

####Execution

Javascript - closures!! You can wrap a group of functions together such that the variables in the "wrapper" can be used by functions contained in the wrapper but not by those outside of it. In other words ... Whenever you see the function keyword within another function, the inner function has access to variables in the outer function. It's all about the scope!!


```javascript
var Board = (function() {
  var board = [];
  var saveState = [];

  return {
    makeSomeCells: function () {
      for (var i = 0; i < 81; i++) {
        var cell = new Cell(i);
        board.push(cell);
      }
    },

    connectCells: function () {
      for (var i = 0; i < 81; i++) {
        board[i].findNeighbors();
        board[i].makeConnections(board);
      }
    },
```
  
Two things went wrong:  
  
1) Animation debacle! Unfortunately tried as we might, we couldn't get it working in time by the end of the Hackathon. The animation was the fresh coat of paint on the whole project.  At least we do know through thorough testing that our algorithm works as it should.

2) Because the unions are randomly generated, there isn't always a path from A to B.

####**10:00pm - "Pencils down"**

Our team takes a huddle to discuss how we're going to present, points to concentrate on, things we took away, etc.

####**10:20pm - Judging**

There were some amazing apps, only two teams had Phase 1 boots, and one of them won!  It wasn't us, but I was still really proud of everyone in my cohort that participated!