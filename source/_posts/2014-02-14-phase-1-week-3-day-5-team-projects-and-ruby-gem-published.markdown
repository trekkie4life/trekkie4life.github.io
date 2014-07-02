---
layout: post
title: "Phase 1: Week 3: Day 5 - Team Projects and Ruby Gem Published"
date: 2014-02-14 20:04:23 -0800
comments: true
categories: 
---

8:30am - Arrive

Quick check-in to refresh our brains and make sure everyone is up to speed and to plan our attack for the morning and day.

![White board session](http://i.minus.com/imADChWNwphdy.jpg)

No one pushed to master, we made new branches based on the feature, when we had a feature working, we pushed to GitHub and then submitted a Pull Request. Someone else on the team would review it then merge it. We had a really good workflow going.

So, our project? Make a "cool faker" gem to generate fake data for testing - eerily similar to "Faker" but instead of random names, we will use famous movie and tv show characters to populate the data.  What are we calling it? **Cool Faker** what else?!

Other than using Faker, we didn't know how it got or made the data, so we dove into the source code.  It was cool to see how much of it we could follow. Also, we saw that the Faker gem is self contained, all you have to do is download it because the gem comes bundled with all the people/company/etc data it uses.

We followed their example and then had to find a way to gather all the movie/tv characters we wanted without manually typing them in... because we are programming after all, let's use our brains and make the computer do it.

##API use to gather data

We looked at using IMDB's API (Application Programming Interface), but the data you get from it is not clean at all, and since we were on a schedule, our first job was to look for clean data.  Luckily TheMovieDatabase (TMDB) had exactly what we needed and someone even made a Ruby gem that used their API.

After playing around with it, we got the a massive amount of data per movie, but the data was very well organized. Unfortunately there was no way using their API to return *just* character names. The information we got inluded everything, literally everything about the requested movie.  We tried several methods to parse the character names from the data object the API returned, and then wisely decided to just check what kind of object that data was, turns out it's a ``` PatchedOpenStruct ``` (a data structure similar to a Hash), from there some quick Googling and we learned a little bit about it and how to remove the nugget of character name data we wanted.  Easier than it sounds because the data was clean/well organized, but still an enjoyable little problem that makes you feel good when playing with an API for the first time.

```ruby
names:
  friends: ["Rachel Green", "Monica Geller", "Phoebe Buffay", "Joey Francis Tribbiani", "Chandler Bing", "Ross Geller"]
  entourage: ["Eric Murphy", "Vincent Chase", "Johnny 'Drama' Chase", "Turtle", "Ari Gold", "Lloyd"]
  batman: ["Batman", "Bruce Wayne", "Joker", "Two-Face", "Riddler", "Poison Ivy", "Rachel Dawes", "Harvey Dent", "Lt. James Gordon", "Alfred", "Scarecrow", "Lucius Fox", "Bruce Wayne", "Joker's henchman", "Engel", "Mayor of Gotham", "Lau", "Wuertz", "Salvatore Maroni", "Barbara Gordon", "Chechen", "Stephen", "Loeb"]
  startrek: ["Captain Jean-Luc Picard", #...
  
quotes: ["Traditionalists are pessimists about the future", #...
```

On the other side, Jamie and I were getting our gem file structure down by breaking down Faker's and understanding how each file used another.

Quentin was did the vast majority of tests, I paired up with him for a bit on it to get my feet wet with RSpec. The syntax is great because it almost reads like normal english.

We decided in our whiteboarding and discussions that our MVP would be a gem that worked by plucking random character names. In order to test it, we used a tourny bracket (think, March Madness) application that used Cool Faker to populate the teams and then we modified the application to pick a random winner per matchup.  IT WORKED!!  High-fives went all around.

Our final version can throw up quotes from various sources and come up with team-names (or company names, whatever you [the user] desire).  For the names, you can even specify if you only want characters from a specific movie.

```ruby
require_relative "cool_faker"

module CoolFaker
  class Character < Base

    @data = self.parse(dir + '/cool_faker/data.yml')

    def self.name # random character from random movie
      @data['names'][@data['names'].keys.sample].sample
    end

    def self.name_from(movie)  # only characters from a specified movie/tv show
      @data['names'][movie].sample
    end

  end
end
```

If you want to see the source code, head over to [GitHub](https://github.com/Qt-dev/cool-faker)

If you care to download it yourself, all you need is Ruby installed and a connection to the interwebs.  Because it's officially published on [RubyGems](https://rubygems.org/gems/cool_faker)!! Woo hoo!

```ruby
$ gem install cool_faker
```

High fives and hugs to everyone on team Más Awesomos: Quentin Devauchelle, Jamie McKenzie, Nicholas Cu, and myself!



Presentations of Phase 2 one-day group projects from the Sea Lions, followed by Phase 1 two-day group projects from the Banana Slugs (that's us!), then some alums came in and showed their Phase 3 group projects. It was great fun and cool to see what we types of things we would be learning about and how some people implemented those technologies. I was impressed with everyone's stuff!

Post-presentations, it's group kareoke time at DBC to celebrate the ending of a phase. A couple people in each cohort are repeating the phase because they want to solidify their knowledge before moving on. It's what works best for them, it's never an easy decision, and it's definitely not failure by any means.  So it takes 12 weeks to become a junior developer, not 9. Is anyone seriously going to shake their head in shame at that? I don't think so. Good luck to all phases and cohorts moving forward!

10:15pm - Depart

>Education is what remains after one has forgotten what one has learned in school.  
- Albert Einstein