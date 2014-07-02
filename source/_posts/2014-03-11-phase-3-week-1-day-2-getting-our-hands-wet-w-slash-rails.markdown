---
layout: post
title: "Phase 3: Week 1: Day 2 - Getting our hands wet w/Rails"
date: 2014-03-11 22:44:50 -0700
comments: true
categories: 
---

**8:00am - Arrive**

Paired with Matthew today, another great pairing session. I got a bit more confident with my testing skills, played with the test suite Capybara and got a bit more comfortable with RSpec and Shoulda matchers.

A little taste of each, but no main turkey meal out of any of them. I'm sure we'll get to it though!

Remake the Craigslist Jr app we did in phase 2, and do it before lunch - thanks to our knowledge and the power of Rails.

Did we succeed?  You know it! Even added some transitions on hover, whaaaaaa. hahaha, ok, so that's not difficult, but we were overly proud of it. It's the little victories that count.

After lunch - get ready to write some tests.

First up - use FactoryGirl to help with test data. Yes, we are using our CoolFaker gem!

```ruby spec/factories.rb
FactoryGirl.define do
  factory :category do
    name { CoolFaker::Team.name }
  end

  factory :post do
    title { CoolFaker::Team.name }
    email { Faker::Internet.email }
    key { SecureRandom.urlsafe_base64 }
    price { rand(50..1000000) }
    description { CoolFaker::Team.slogan }
    category
  end
end
```

Next up, utilize FactoryGirl in helping us do our controller tests.

```ruby spec/controllers/categories_controller_spec.rb
require 'spec_helper'

describe CategoriesController do
  let(:category) { FactoryGirl.create(:category) }
  let!(:post) { FactoryGirl.create(:post) }

  context '#index' do
    it "is successful" do
      get :index
      expect(response).to be_ok
    end

    it "assigns all categories to @categories" do
      get :index
      expect(assigns(:categories)).to eq(Category.all)
    end
  end
end
```

And then our unit/model tests using Shoulda matchers.

```ruby spec/models/post_spec.rb
require 'spec_helper'

describe Post do

  context "validations" do
    it { should validate_presence_of :title }
    it { should validate_presence_of :email }
    it { should validate_presence_of :price }
    it { should validate_presence_of :description }

  end

  context "associations" do
    it { should belong_to :category }
  end
end
```

Again, short and sweet. Testing is a small investment in time with a huge return - and it's definitely growing on me. I'm sure Steven and Shadi (our Phase 3 instructors) would shed a tear of joy if they read that.

**11:40pm - Depart**

>To teach is to learn twice.  
- J. Joubert

