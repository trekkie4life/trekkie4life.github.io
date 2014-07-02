---
layout: post
title: "Phase 2: Week 3: Day 3 - O-Auth"
date: 2014-03-05 00:10:35 -0800
comments: true
categories: 
---

**8:30am - Arrive**

A lecture on the intricacies of O-Auth flow. Yeah, it's complicated, but as long as I have a high-level understanding I can build on it.

As Quentin (my pairing partner for the day ::high-five:: is always fun to work with) get started, we get everything set up, but then whenever we try loading the sinatra server, we keep getting a 401 error.  401?! Ok, let's take a look. Everything seems well on our side, and on Twitter's side online when we log into our developer account. Hmmm, what is it? Maybe it's how our key and secret are stored in the yaml file? Edit format, save, start server - load page...~~success~~ error, still 401. Some more round about debugging before - take a guess - and it's at about this point that Sherif's voice is starting to enter.... "look at the simple thing first."

A couple other boots in our cohort took a look and it was beyond simple - fundamental infact - the callback URL we had for the app on Twitter was empty. ::massive facepalm::
![](http://4.bp.blogspot.com/-m2slla6Qc4o/Uk2nq4In5GI/AAAAAAAAE0w/BVWz6YNrgj4/s1600/picard-facepalm-o.gif)

At this point we were ready to roll.

12:30pm - Lunch & Yoga

The "access token" and "access token secret" will have to change depending on what user is currently authenticated. This key pair answers the question, "On whose behalf is this application acting?"

Twitter needs to answer both of these questions to make sure that the application is valid and that the application can *only* do what it has permission to do on behalf of an authenticated user.

The core OAuth flow goes like this:

1. Application generates URL to "Sign In with Twitter".
2. Application renders page with "Sign In with Twitter" link
3. User clicks "Sign In with Twitter"
4. User is redirected to Twitter and authorizes the application
5. User is redirected back to the application's callback URL
6. Application verifies the redirection from Twitter is valid
7. If valid, Application takes appropriate action

We first tweeted from the command line, in true geek fashion.

Next was adding a small user interface so any Twitter could log in and tweet from their own account.

Success!!



**11:00pm - Depart**

>Learning how to learn is life's most important skill.  
- T. Buzan


