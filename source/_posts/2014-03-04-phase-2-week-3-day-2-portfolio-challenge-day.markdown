---
layout: post
title: "Phase 2: Week 3: Day 2 - Portfolio Challenge Day"
date: 2014-03-04 14:25:49 -0800
comments: true
categories: 
---

**8:30am - Arrive**

catching up on sleep after a late night

Today is a catchup day on the portfolio challenges. I have 2 more to do and I'm done.

It's nice to have a day to be able to concentrate and take a deep breath to 

Portfolio Challenge 9 -

---

models do not have to be ActiveRecord backed. Think about the Die problem!

---
some quick truth bombs from a review lecture on the boundary between JS & jQuery:

* Models - better not have jQuery
* Controller - just has an "ajax helper" (maybe it returns JSON objects)
* View - jQuery, baby!

Models instantiated by a Controller - i.e. collection of trees (possibly an array of tree objects) lives in the Controller
render those in the View by using jQuery to manipulate the DOM

Ajax makes it difficult because of things like Binding (where do those go?). Do not have binding jumble up the HTML, that responsiblity should be held in the View.

---

Portfolio Challenge 10 - APIs

1st go to [instagram and signup](http://instagram.com/developer/) and register to get your client_ID and client_Secret.

Instagram is very VERY picky about the website you sign up with as all requests redirect there, so be sure to use your local machine if you are making and testing an app locally.

After you successfully sign up there, go [Download the ruby gem 'instagram'](https://github.com/Instagram/instagram-ruby-gem)

Their documentation is excellent.

`gem 'instagram'` to your Gemfile.

Add `require 'instagram'` to your environment.

Their example is hardcoded, but you can definitely make it cleaner and MVC it if you want (and you should want to do that).

You can use the API to search for photos/videos by the following:

* geo location
* hashtag
* user-name
* etc...

You can also have a user authorize the app to like/comment/unlike on things, but for this particular challenge, I found out how to gather the tags.  In my code the following line in the controller works the magic...
what that returns is actually an array of Objects from instagram.

```ruby
post '/tags/:tag' do
  @tag = params[:tag]
  p @tag
  Instagram.tag_recent_media("#{@tag}", options = {count: 24}).to_json
end
```

Using jQuery, we iterate over the array parsing out the photo data we want from an object and throw it on the DOM.

Since loading the images can take a while, I have an animated gif show until the ajax pings me that it's done at which point the Instagram images load.

Once everything was working like it should, I added some minor styling using vanilla CSS.

It's simple and clean and works well too! I'd like to convert it to a Foundation 5 layout.

Enter your hash tag below, let's go with puppies...
![](http://i.minus.com/i0huzXcA3PD3L.png)

PUPPIES!!!!
![](http://i.minus.com/imFzAFaGG9uP3.png)


**12:15am - Depart**

>It is not knowledge, but the act of learning, not possession, but the act of getting there which generates the greatest satisfaction.  
- F. Gauss