---
layout: post
title: "Phase 3: Week 1: Day 1 - Intro to Rails"
date: 2014-03-10 23:44:41 -0700
comments: true
categories: 
---

**8:00am - Arrive**

I did some reviewing over the weekend, but got out of the bubble by going to visit some friends in the city. It was so nice to get a breath of fresh air and share some of my experience with people close to me and rooting me on.

---

A day of welcoming the new cohort and all that involves. I love it - this communal feeling of opening up our space to doughy eyed future coworkers and friends and paying it forward in welcoming them to their new home for the duration of DBC. And as I mentioned before, the

The video Ivan an Mathilde made was great - cheesy and geeky and wrapped up in some Banana Slug (our cohort) and DBC inside jokes. Everyone was dying of laughter. I'm proud of them for pulling that off so well.  It's official, we're in Phase 3 now. ::jaw drops::

We got a breakdown of what our final three weeks will look like. At one point, Shadi (one of our instructors, who happened to also be one of our great Phase 1 instructors) said, "ONLY 8 business days until you pitch final projects." And then it hit me. these next three weeks will fly by, just as the other six did.

After lunch we got our first intro lecture to Rails, after that, it was time to get our hands dirty and see what was going on.

Our number one rule in Phase 3 in regards to Ruby on Rails...

Do NOT use rails scaffold & rails generation. The only exception is Rails generate migration. We are learning to write code, don't let Rails write it for you.

Makes perfect sense.

Right off the bat, you can't help but realize they had a very clear method in getting us to use Sinatra with a stripped down Rails skeleton/file structure in it, to get us used to it. It'd be difficult to jump from Ruby straight into Rails without that intermediate step of Sinatra in Phase 2.

Setting up routes is Rails is easy - once you have your migrations and models set up, you want to work on your views, before that, hit up `config/routes.rb`

Priority is based on order of creation, so if one depends on another, just put it first, as seen below


```ruby config/routes.rb
root :to => 'welcome#index'  #remember to delete public/index.html

resources :products
```

`resources :products` That simple line of code will maps HTTP verbs to controller actions automatically! Sweeeeeeet!

Use `rake routes` in the Terminal to see a list of your HTTP verbs and which controller actions they map to.

If you had to the products controller, you'll see your actions/methods...

```ruby app/controllers/products_controller.rb
def index
 @products = Product.all
end

def show
    @product = Product.find(params[:id])
  end

  def new
    @product = Product.new
  end
  
  __END__

and also create, edit, update, destroy

```

then there's a view folder you make for the corresponding controller `app/views/products/` and the files contained within correspond to index, edit, show, new, etc. The files are formatted `*.html.erb`

and `app/assests` contains the folders that have your image, JavaScript, and CSS files. How convenient.

It's only the beginning, and there's an ocean of information left to learn, but it's pretty cool stuff!


**11:15pm - Depart**

>Tell me and I forget. Show me and I remember. Involve me and I understand.  
- Chinese Proverb