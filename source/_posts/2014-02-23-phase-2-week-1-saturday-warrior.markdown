---
layout: post
title: "Phase 2: Week 1 - Weekend Warrior"
date: 2014-02-23 10:30:26 -0800
comments: true
categories: 
---

**11:30am - Arrive**

Working on portfolio challenge 2 and 3 today.

Challenge 2:

build ActiveRecord Models, Migrations, Validations, and Relations to model the following user stories:

* A User has many skills and a Skill can be assigned to many users.
* A User has a proficiency rating for each of their skills.
* Multiple skills can not be saved with the same name.


Let's start, shall we?

For the users table

```ruby /db/migrate/create_users.rb
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :name
      t.string :email
      t.timestamps
    end
  end
end
```

For the skills table
```ruby /db/migrate/create_skills.rb
class CreateSkills < ActiveRecord::Migration
  def change
    create_table :skills do |t|
      t.string :name
      t.string :context
      t.timestamps
    end
  end
end
```

For the join table - user_skills
```ruby /db/migrate/create_user_skills.rb
class UserSkills < ActiveRecord::Migration
  def change
    create_table :user_skills do |t|
      t.belongs_to :user # note the "belongs_to" to make the association!
      t.belongs_to :skill
      t.integer    :level, default: 0
    end
  end
end
```

Now how do those line up with the models??

Even though the database has an association between tables, we have to make the connection in our models as well so Active Record knows how to handle everything.

```ruby app/models/skill.rb
class Skill < ActiveRecord::Base
  validates :name, uniqueness: true

  has_many :user_skills # so a skill has many user skills AND ...
  has_many :users, through: :user_skills # a skill has many users THROUGH the table user_skills

  def user_with_proficiency(rating)
    self.user_skills.find_by_level(rating).user
  end
end
```

Let's take a look at our User model to see the connection
```ruby app/models/user.rb
class User < ActiveRecord::Base
  validates :name, :email, presence: true, uniqueness: true

  has_many :user_skills
  has_many :skills, through: :user_skills
```
Well look at that. Similar associations made in the users table to connect to the skills table via user_skills table.

```ruby app/models/user_skill.rb
class UserSkill < ActiveRecord::Base
  belongs_to :user
  belongs_to :skill
end
```

Challenge 3 was a whole different ball game, because using Sinatra, we had to create a user signin/signup and authenticate signed in users before displaying information.  For password encryption it was recommended we go with [BCrypt](http://en.wikipedia.org/wiki/Bcrypt).

Since HTTP is a stateless protocol (because each command is executed independently, without any knowledge of the commands that came before it. This is the main reason that it is difficult to implement Web sites that react intelligently to user input), we need a way to make sure the user experience is unbroken throughout their visit to the website. How to do that? 

Sessions! Sessions are kind of like a hall pass that you give the user/client (some of you may have heard the term, "cookie" before, a session is basically a cookie). That hall pass lasts as long as you want it to, in our situation, we want it to last as long as a user is logged in. When a user logs out, that session is cleared.  Under the hood it's pretty cool.


```ruby
def logged_in?
  !!session[:id]
end
```

we use a `get` request for the login.erb page and then collect our user info

```ruby app/views/login.erb
<div class="container">
  <h1>Awesome Authentication Authorization App - Login</h1>

  <div class="login_screen">
    <form action="/users/login" method="post">
      <input type="text" name="email" placeholder="enter email">

      <input type="password" name="password" placeholder="enter password">
      <input class="input-rounded-button" type="submit" value="login">
   </form>
  </div>
</div>
```

You'll notice in the view, that the form method is a `post` 

```ruby 
<div class="container">
  <h1>Awesome Authentication Authorization App - Login</h1>

  <div class="login_screen">
    <form action="/users/login" method="post"> # right here, the action and the method!
      <input type="text" name="email" placeholder="enter email">

      <input type="password" name="password" placeholder="enter password">
      <input class="input-rounded-button" type="submit" value="login">
   </form>
  </div>
</div>
```

And in the `post` route is our controller and the logic used to login.

```ruby app/controllers/index.rb
post '/users/login/?' do
  @user = User.find_by_email(params[:email])
  if @user.password == params[:password]
    session[:id] = @user.id
    redirect "/users/#{session[:id]}"
  else
    redirect '/'
  end
end
```

the `#password ==` is actually a method in BCrypt that decrypts the hashed password and then compares it to the stuff on the right of the redefined `==` method.

It took A LONG time for us to figure out what was going on with implementing BCrypt.

So long in fact, that I had to call it quits at 1:40am and then finish it tomorrow. Sometimes your brain needs to reboot.

**1:40am - Depart**

>Programs must be written for people to read, and only incidentally for machines to execute.  
- H. Abelson and G. Sussman