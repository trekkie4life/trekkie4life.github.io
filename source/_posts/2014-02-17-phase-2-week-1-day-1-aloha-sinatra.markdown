---
layout: post
title: "Phase 2: Week 1: Day 1 - Aloha Sinatra"
date: 2014-02-17 23:01:39 -0800
comments: true
categories: 
---


**8:00am - Arrive**

New Cohort arrives - it's interesting being on the otherside of the activities for the morning. No less fun, and the buzz level had a nice spike for the day.  I wish the Phase 1ers an excellent 3 weeks, it's a blast!

The new teachers seem good (you get a pair of teachers for every phase), and the overview of Phase 2 has one theme in common... It will be much more difficult than Phase 1.

Making the jump from 'programmer' to 'web programmer/developer'.  Yeah, my jaw just dropped.

`$ shotgun config.ru` starts our application with shotgun, and shotgun means we don't have to stop and restart the local server to check for changes to our web app.

##[Anagrams](http://en.wikipedia.org/wiki/Anagram)  

One of the challenges we had today was to make an anagram solver web application - our first one!

##Migrating & Seeding the DB


```ruby /db/migrate/
class CreateWords < ActiveRecord::Migration
  def change
    create_table(:words) do |t|
      t.string :text, null: false, length: 200
      t.string :sorted, null: false, length: 200
    end
  end
end
```

Seeding the database will do exactly that, by using the file `words` that has the list of words, each word on it's own line - and then putting a word in the text column, then putting the letters of that word rearranged alphabetically into the `sorted` column. Why are adding a `sorted` column? Because it's the easiest way to see if something is an anagram of another word. If a row's `sorted` column mathes another, those two words are anagrams!

```ruby /db/seeds.rb
ALL_WORDS = File.open('db/fixtures/words', 'r')

ALL_WORDS.each_line do |dict_word|
  real_word = dict_word.chomp
  real_word_sorted = real_word.downcase
  Word.create(text: real_word,
              sorted: real_word_sorted.split('').sort.join(''))
end
```
Remember, the model is what interacts with the database

##Model

```ruby /app/models/word.rb
class Word < ActiveRecord::Base
  # Remember to create a migration!

  def anagrams
    # only need to search sorted words of the same length
# where Word[:sorted] == self.sorted

    anagrams = Word.where(sorted: self.sorted)
    actual_ana = []
    anagrams.each do |word|
      if word.text != self.text
        actual_ana << word.text
      end
    end

    actual_ana

  end
end
```
And our controller takes in commands and passes them to both the database and the view

##Controller

```ruby /app/controllers/index.rb
get '/:word' do
  @word = params[:word]
  @my_word = Word.new(text: @word, sorted: @word.split('').sort.join('')) #something like this
  erb :index
end
```


##View

```erb /app/views/index.erb
<div class="container">
  <p>Show a list of anagrams for "<%= @word %>"</p>
  <% anagrams_array = @my_word.anagrams %>
  <% anagrams_array.each do |ana_word| %>
   <p><%= ana_word %></p>
   <% end %>
</div>
```

**10:35pm - Depart**

>In order to make an apple pie from scratch, you must first create the universe.  
-Carl Sagan

