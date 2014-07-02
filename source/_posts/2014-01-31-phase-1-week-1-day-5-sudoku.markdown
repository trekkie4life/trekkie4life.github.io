---
layout: post
title: "Phase 1: Week 1: Day 5 - Sudoku"
date: 2014-01-31 23:30:49 -0800
comments: true
categories: 
---
**8:00am - Arrive**

AM - check-in with new small groups (3 from our cohort, 3 from the cohort ahead of us). We each get 2 min to talk about anything and not be interrupted. The goal of this exercise is open up, take what’s on your mind and in your heart and talk about it. It may or may not be related to the happenings of DBC.

After pairing up with my coding partner for the day, we dive into how to solve soduku. First step - let’s solve a puzzle on paper and see how we each (as humans) solve it.

How do you choose where to start?
Did you adopt the same notation/board markings while playing Sudoku? Why? If not, why did you choose differently?
Why do we do a certain action?
Are we avoiding any strategies because they’re too tedious or require us to remember too much?

From there we build the logic of how our sudoku solving algorithm (without guessing) will work. We use a high level approach in our Pseudocode and avoid language specific syntax.

Once we find an empty cell, to form a set of possible values for that cell we check what values are already in that row, then in the column, then in the 3x3 sub-box the cell falls within.

IF the number of possible values is just one, we put that value into the grid
ELSE we move onto the next spot - so on and so forth

Yes, we’ll have to go over the board several times in order to fill in all the empty cells.

**12:30pm - lunch and yoga** - harder than Tues or Thurs, but more enjoyable at the same time - definitely allows me to keep my body and mind centered.

PM - finishing up the challenge

**11:00pm - Depart**

>Email is a wonderful thing for people whose role in life is to be on top of things. But not for me; my role is to be on the bottom of things. What I do takes long hours of studying and uninterruptible concentration.  
- Donald Knuth