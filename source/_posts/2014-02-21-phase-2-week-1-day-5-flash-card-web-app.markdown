---
layout: post
title: "Phase 2: Week 1: Day 5 - Flash Card web-app"
date: 2014-02-21 21:19:06 -0800
comments: true
categories: 
---


**8:15am - Arrive**

Group projects - Flashcards Web App

12:30pm - Yoga, Lunch

Lightening talk - 5 minute "lectures" on a topic, we all have to do one once a week. Mine was today - my topic, Semantic Markup.

Present MVP

What did we learn?

since HTTP requests only all `GET` and `POST` it takes a little duct tape to get `DELETE` or `PATCH` to work.

Here's the duct tape in action...

```ruby 
<div class="bottom_buttons">
  <form name="delete" action="/notes/<%= @note.id %>/delete" method="post"> # the psuedo post method
    <input type="hidden" name="_method" value="delete">  # here the magic happens w/the REAL method value
    <input class="input-rounded-button" type="submit" value="Delete">
  </form>
</div>
```


notice how in the controller, how `delete` is used instead of `post` so it works with the value of the hidden method from the view!

```ruby app/controllers/index.rb
get '/notes/:id/delete' do
  @note = Note.find(params[:id])
  erb :confirm_delete
end

delete '/notes/:id/delete' do
	@note = Note.find(params[:id])
	@note.destroy
	redirect '/notes'
end
```

Got a few questions answered from Stephen and Quentin - hat tip to them for helping me make some good neural connections.

RSpec test for a note object to make sure it contains a non-nil title and body. 

```ruby
require 'spec_helper'

describe Note do
  it { should validate_presence_of :title }
  it { should validate_presence_of :body }
end
```

It does this by checking to make sure the Note model validates those.

```ruby app/models/note.rb
class Note < ActiveRecord::Base
  validates_presence_of :title, :body
end
```

Finished Portfolio Challenge 1 - woo hoo! In the morning I'll tackle number 2!

Finally going to get some serious sleep to prepare for a very busy weekend with DBC work.


**12:30am - Depart**

>At the source of every error which is blamed on the computer you will find at least two human errors, including the error of blaming it on the computer.  
- Anonymous