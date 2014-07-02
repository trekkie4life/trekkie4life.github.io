---
layout: post
title: "Phase 2: Week 2: Day 3 - AJAX"
date: 2014-02-26 08:17:39 -0800
comments: true
categories: 
---

**7:55am - Arrive**

Paired with Matthew today, a good session - we had steady progress through our AJAX challenges and that made me feel good.



##Portfolio Challenge 5 - Validations

Using the ActiveRecord model to validate information meets certain criteria before saving it to the database.

Our mission:

Use ActiveRecord and Sinatra to allow anyone to create an event, so long as it passes validation rules.

Add validations to the Event model and show appropriate messages to the user when the validations fail.

Prevent Events from being saved when:

* The events date is empty, in the past, or is not valid. 
* The events title is already taken or empty.
* The event organizers name is empty.
* The event organizers email address is invalid.

So, let's take a look at the tests I made in the model

```ruby app/models/event.rb

class Event < ActiveRecord::Base

	validates :title, presence: true
	validates :title, uniqueness: true
	validates :organizer_name, presence: true
	validates :organizer_email, presence: true
	validates :organizer_email, format: { :with => /.+@.+\..+/i, :message => "is not valid" }
	validates :date, presence: true


# here we tell Active Record to check our OWN validation method/test

	validate  :valid_date? # calls the method below

  def valid_date?
   if date && Date.today > date   # why is it only 'date' and not ':date'??
     errors.add(:date, 'Must be a valid date, IN THE FUTURE!') 
   end
  end
end
```

Look again at line 7

```ruby
validates :organizer_email, format: { :with => /.+@.+\..+/i, :message => "is not valid" }
```
There we check to make sure the format of `organizer_email` matches our `:with`, and then provide a custom error message as well.

The cool thing with Active Record is that it wraps all our error messages into a hash (in an object) when we fail validation tests upon an attempt to write to the database.

What can we do with these errors?  WE TELL THE USER, so they can correct the information and re-submit it.

Ok, so how do we do all that?

We grab the params we used from the new_event form.

We will try to create a new Event in the database using those params.

If it works, it works! If not, we will have an @event object which now contains a hash of errors from the failed validation tests.

To get to the errors, take a careful look at line `4`. We get the full_messages which is an array of error message strings.

```ruby app/controllers/index.rb
post '/events/create' do
	@params = params
	@event = Event.create(@params)
	@errors = @event.errors.full_messages unless @event.valid?
	
	if @errors
		get '/events/new'
	else
		get '/events/#{@event.id}/show'
	end
end
```

If there are errors, we want to direct the user back to the create_event page so they can have another attempt... and we'll be helpful and show them what information we need them to fix.

Since we assigned our errors to an instance variable, we have access to those when we redirect back to the create_event page! Time to use some erb and iterate through the array of messages

```html app/views/event_new.erb
<% if @errors %>
<h3 class="error"> You have the following error(s): </h3>
<ul>
<% @errors.each do |error| %>
<li><h4 class="error"><%= error %></h4></li>
<% end %>
</ul>
<% end %>

<form action="/events/create" method="post">

```


**11:20pm - Depart**


>Some people, when confronted with a problem, think, “I know, I’ll use regular expressions.” Now they have two problems.  
— Jamie Zawinksi