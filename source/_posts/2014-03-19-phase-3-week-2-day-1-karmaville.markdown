---
layout: post
title: "Phase 3: Week 2: Day 1 - Karmaville"
date: 2014-03-19 08:47:15 -0700
comments: true
categories: 
---

**8:30am - Arrive**

The goal today was different but no less fun than normal - we were given a highly UNoptimized webapp and told to make it faster.

How?

Look for bottlenecks.  Look for the lowest hanging fruit, and then start fine tuning!

How do we get from a page taking 11sec to load down to under 200ms?

It was a really good foray into looking at code and what causes certain things to really slow down (I'm speaking to you, database queries), and also what small fixes you can implement to take care of that.

One of the best things you can do to speed up database queries in Rails/Active Record is to add a foreign-key Index!  In fact, it should be and often is considered a Rails best practice.

Why do you have to do it? Because Rails does NOT do it automatically for a foreign key.

```ruby your_migration_file.rb
class CreateKarmaPoints < ActiveRecord::Migration
  def change
    create_table :karma_points do |t|
      t.integer :user_id, :null => false
      t.integer :value,   :null => false
      t.string  :label,   :null => false

      t.timestamps
    end
    add_index :karma_points, :user_id  # this adds the foreign index!!
  end
end

```


On a completely non-sequitur note - I have never let my facial hair grow for this amount of time without shaving. I'd like to think of it as a "real" beard, something that makes men tremble in fear and stare in awe.  Instead, it more closely resembles a dying lawn with a few patches of grass clinging to life. I've also taken to stroking my (sad) beard when deep in thought. I never used to do that motion unless in jest, but apparently having facial hair and arms means you will form that habit. It's instinctual. You cant fight it.

**12:00am - Depart**

>On two occasions, I have been asked [by members of Parliament], "Pray, Mr. Babbage, if you put into the machine wrong figures, will the right answers come out?" I am not able to rightly apprehend the kind of confusion of ideas that could provoke such a question.  
- C. Babage