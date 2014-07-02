---
layout: post
title: "Phase 2: Week 1: Day 3 - More Sinatra and Active Record"
date: 2014-02-19 08:16:59 -0800
comments: true
categories: 
---


**7:05am - Arrive**

##REST
Relational State Transfer

HTTP Verbs (what makes the 'net go round) + Paths -> Action

| Actions        | HTTP Verb          |   Path  |
| ------------- |:-------------:| --------:|
| index      | GET | puppies/    |
| show      | GET      |   puppies/:id    |
| update | POST      |    puppies/:id    |
| create | POST      |    puppies/    |
| delete | DEL      |    puppies/:id    |
| edit (then points to update) | GET      |    puppies/:id/edit    |
| new (then point to create) | GET      |    puppies/new    |


(edit) GET displays form for updating -> POST is the HTTP verb used to consume that action

##Models
Don't forget to create models after creating DB

`$ rake generate:model NAME="[name in singular]"`

You can include join table in model file with

```ruby
has_many :XYZ
```

##HEROKU  

`$ heroku create`  
`$ heroku remote local-branch:[git-remote-branch.git]`

Remember: Heroku doesn't like nested directories - only the main directory app and its corresponding folders are in.

You can migrate and seed a database on Heroku from the Terminal (as long as you have a seed file in your application)!

`$ heroku run rake db:migrate`  
`$ heroku run rake db:seed`



**10:45pm - Depart**

>The opposite of a correct statement is a false statement. But the opposite of a profound truth may well be another profound truth.  
- Niels Bohr