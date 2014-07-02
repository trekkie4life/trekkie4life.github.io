---
layout: post
title: "Phase 1: Week 3: Day 3 - Intro to Active Record"
date: 2014-02-12 08:36:09 -0800
comments: true
categories: 
---

**8:15am - Arrive**

I was freakishly tired early last night, so slept in a bit this morning - it was exactly what I needed.

**Active Record** - Active Record is essentialy a layer of Ruby code that runs between your database and your logic code.  When you want to make changes to the database, you write some Ruby, then migrate - the migrations make the actual changes what database you're using, then you only have to change a couple of lines of code. Now *that* is slick.

```ruby
$ rake db:migrate
```

##The Database:  

Since Active Record interacts with the database, it's the M in MVC.

The syntax for ActiveRecord Migrations is as follows:

```ruby
class CreateStudents < ActiveRecord::Migration # each migration is a class
  def change
    create_table :students do |t| # create a table 'students' in the db with the below columns
      t.string :first_name
      t.string :last_name
      t.string :gender
      t.date   :birthday
      t.string :email
      t.string :phone
      t.timestamps # this automatically gives us created_at & updated_at columns
    end
  end
end
```
You may have noticed that there isn't an ``` id ``` column - that's because Active Record adds the unique primary key ``` id ``` to table *automatically*.

What's an even cooler thing that the migration class does? It is semi like git (version control), you can roll back and undo some changes.  How you might ask?

```ruby
$ rake db:rollback
```
REMEMBER: migrations don't happen automagically when you create a new model, you have to *MANUALLY* run them.

When we create a ``` Student ``` model, a file is created in ```app/models/student.rb```

```ruby
class Student < ActiveRecord::Base
.
.
.
```

##Adding validations

Why validate? Validations are hugely important in any web app, it's here that we check to ensure the data we want to put into the database is clean & correct.

**Remember - validations created in our model class(es) don't actually change the database!**

The ``` validates ``` method sets up all our validations, first we pass which field(s) we want to validate, then we pass it a hash with the validation properties.  There are a ton of pre-made validation helpers or we can even make our own.

```ruby
class Student < ActiveRecord::Base
  validate :minimum_legal_student_age
  validate :standard_phone_number
  validates :email, format: { with: /\A([^@\s]+)@((?:[-a-z0-9]+\.)+[a-z]{2,})\Z/i, message: "email format is incorrect"}
  validates :email, uniqueness: true # validates the email is unique in the database in the email column
  
  def standard_phone_number
    errors.add(:bad_phone, "must be at least 10 numerals") if self.phone.gsub(/[^0-9]/, "").length <= 10
  end
```  

``` validate ``` (NOT validate**s**) calls the method ``` standard_phone_number ``` to verify the phone # meets requirements, otherwise an error is given and the test fails.

##Associations

[Associations](http://guides.rubyonrails.org/association_basics.html) are how Active Record handles multiple tables

For more detailed information, hit up the [docs](http://guides.rubyonrails.org/migrations.html#supported-types)

**10:40pm - Depart**

>If you want to improve, be content to be thought foolish and stupid  
-Epictetus