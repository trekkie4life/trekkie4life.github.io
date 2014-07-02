---
layout: post
title: "Phase 3: Week 1: Day 3 - TDD w Rails"
date: 2014-03-12 23:01:54 -0700
comments: true
categories: 
---

**8:00am - Arrive**

Today, paired with Matthew again ::high-five:: to TDD with feature testing! We were given a 40% complete version of a "to do" app. With this app, you can add several Todo lists (say, "Home", "Work", etc). You can edit the list name, and each list has its own tasks.

Our job was to add functionality to the tasks (tasks can be added, marked as completed, or unmarked, edited, and be deleted) - and to do it with a TDD frame of mind.

We tested via Capybara - because we are really getting an emphasis on it now, and the reason was revealed to us... it's because testing via Capybara is time intensive to run, an we will gain a new found love of controller tests and also unit/model tests, which are pretty inexpensive to run from a time stand point.

Capybara syntax is kind of funky but it reads pretty close to english. Hey, click on this, fill in that, expect this result or thing to be on the page.

```ruby spec/features/tasks_spec.rb
describe "User can create a task" do

    context "with valid body" do
      it "task link will be appended to the page" do
        visit todo_path(todo)
        fill_in "Body", :with => "clean house"
        click_on "Create Task"
        expect(page).to have_content "clean house"
      end
    end
```

Afterward we threw down some mild styling just to add a dash of spice to the web app.

And in the evening we concentrated on RSpec.

I'm feeling a lot more confident on my testing 'skillz'.


**12:15am - Depart**


>More than the act of testing, the act of designing tests is one of the best bug preventers known. The thinking that must be done to create a useful test can discover and eliminate bugs before they are coded - indeed, test-design thinking can discover and eliminate bugs at every stage in the creation of software, from conception to specification, to design, coding and the rest.  
- B. Bezier

