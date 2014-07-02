---
layout: post
title: "Pre-Phase 2 - Coach's Corner"
date: 2014-02-16 14:06:02 -0800
comments: true
categories: 
---


**12:00pm - Arrive**

A couple of coach's came in today to give a Sinatra intro class. Sinatra is not a framework, but rather a domain-specific language for building websites, web services, and web ap- plications in Ruby.  

It's recommend that we implement MVC since we will probably be using it until something better comes along.  

`M`: Model - only one that talks to the database via Active Record  
`V`: View - changes the data to HTML  
`C`: Controller - it delegates to others, it does NOT care about the the data itself  

![MVC](http://24.media.tumblr.com/c58e571c5ef307b5eb9905a01d6e5fc8/tumblr_n147l3s77F1t30egqo1_r2_1280.jpg)

Your browser sends a GET request and it's parsed similar to how an address is by the post office.

The Controller finds `WHO`.

![address](http://31.media.tumblr.com/a6f9bbb0818a569f6a4349213ad45a30/tumblr_n147gqY2ec1t30egqo1_1280.jpg)

##SINATRA

Practice with the MVC design pattern. `app.rb` is our Controller.  Views are in the view folder, controllers in the controller folder. It's almost too simple. ;)

![file structure](http://i.minus.com/i8wVvvWs5PreW.png)


###Routes

Routes are matched in the order they are defined. The first route that matches the request gets fired off.

Route patterns may include named parameters, accessible via the params hash:

```ruby
get '/hello/:name' do
  # matches "GET /hello/foo" and "GET /hello/bar"
  # params[:name] is 'foo' or 'bar'
  "Hello #{params[:name]}!"
end

# is the same as...

get '/hello/:name' do |n|
  # n stores params[:name]
  "Hello #{n}!"
end
```

When an `.erb` file has `<%    %>` it just means the stuff inside is Ruby code, in this case it's just logic and it will NOT be displayed.

The `.erb` equivalent of `puts` is `<%=   %>`

```ruby
<h1>DBC Coaches</h1>

<a href="/coaches/new">Create new coach</a>

<ul>
<% @coaches.each do |coach| %>
  <li><%= coach %></li>
<% end %>
</ul>
```

In the case of this example, if we want to add a new coach we'd go to `localhost:4567/coaches/new`, and our controller calls `new.erb` (as can be seen from the code below)

```ruby
require 'sinatra'
require './models/coach'

get '/' do
  @coaches = Coach.all

  erb :index
end

get '/coaches/new' do
  erb :new
end

post '/coaches' do
  puts params

  Coach.create(params)

  redirect '/'
end
```

`new.erb` is seen below

```ruby
<form action="/coaches" method="post">
  <input type="text" name="coach_name" placeholder="Enter coach name">
  <input type="submit">
</form>
```

So we arrive at index.erb via the first Get, then from there if we click on `Create New` we head to `new.erb` - Thumbs up!

Overall a great intro session. Thanks, coaches!


**10:25pm - Depart**

>Computer science... differs from physics in that it is not actually a science. It does not study natural objects. Neither is it, as you might think, mathematics; although it does use mathematical reasoning pretty extensively. Rather, computer science is like engineering; it is all about getting something to do something, rather than just dealing with abstractions.  
-Richard Feynman
