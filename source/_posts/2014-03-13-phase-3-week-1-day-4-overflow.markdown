---
layout: post
title: "Phase 3: Week 1: Day 4 - Overflow"
date: 2014-03-13 14:03:25 -0700
comments: true
categories: 
---
**8:30am - Arrive**

Seattle Style - the hidden menace, no parentheses.

```ruby 
def add operandA, operandB
  operandA + operandB
end
```

Is it only style or is it function? Well, it makes the edge cases (where you actually have to use parentheses) harder to find and fix in your code. But to each their own.

---

Testing RSpec, Rails doesn't actually render the body, so the body is just an empty string. To check if something is actually in the body that you're testing for, use `render_views` right below the first `describe` statement in your controller tests.

Remember, in Capybara, an actual browser window is opened, so you don't run into this problem.

```ruby
describe "this is the first describe" do
  render_views
  # more fun testing code here!
end
```

---

\#change

once upon a time change did not exist, there was only up & down

Rails got smarter, would figure out what the inverse operation was.

Migrations change structure. If you need to change structure (raw data) AND edit the code, you...

1) migration (structural change)

2) SQL operations - populate new column you added

DO NOT UNDER ANY CIRCUM - USE YOUR ACTIVE RECORD MODEL TO CHANGE YOUR DB

want data repopulation to not be bound to Rails, but solely to the database itself - it's also much faster bc Active Record has a lot of overhead on migrations.

What does that look like in code?

```ruby
add_column :tasks, :todo_id, :integer #the structural change

#ActiveRecord::Base connection.execute_sql "long string of SQL"
```

Group project - first one using Rails!! 

Quentin, Chermaine, Matthew, Hunter, and myself. I've never been in a group with either Matthew or Hunter, but they are both sharp and bring a lot, so I'm looking forward to the experience and learning from them too.

We have to make a [Stack Overflow](http:/www.stackoverflow.com/questions) clone. Although make it about something other programming. - We are deciding to make a "DBC Overflow" - where Phase 0 and potential applicants can ask questions about the experience and how to prepare.

After getting our Rails skeleton set up (no scaffolding allowed here, folks), we had our division of labor set up. Vertical slices and features split up among the team.

Hunter and I were to work on Questions/Answers from the database all the way up to their views.

Everyone committed early AND often.

Hunter and I methodically worked through several errors and bugs - getting everything set up with passing tests by the time we left.  Gotta tell you, that is one hell of a feeling of accomplishment. Tomorrow we tie everything together and iron out the kinks.

Also, no merge conflicts! Woo hoo!


**1:20am - Depart**

>Simplicity is the soul of efficiency.  
- A. Freeman