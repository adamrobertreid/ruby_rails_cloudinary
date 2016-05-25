# ruby_rails_cloudinary

## Getting Started

We're going to create a simple photo app. You will be able to upload photos to a cloud and then pull the iamges
back through a super fast CDN. We will be using two gems in our app `'carrierwave'` & `'cloudinary'`.

* create simple ruby on rails app
* install `gem 'carrierwave'`, `gem 'cloudinary'`
* upload photo
* display photo through CDN to DOM

### Setup

Create a new rails app:
```bash
rails new photo -T -d postgresql
cd photo
```
Create the databases:
``` bash
rake db:create
```



## Routes First

Let's start with the routes for a user.

`config/routes.rb`

```ruby
Rails.application.routes.draw do
  root to: "users#index"
end
```
```bash
rake routes
```

## Users Controller Second

Let's go ahead and great a users controller
```bash
rails g controller users
```


## Cloudinary getting started guide

### 1. Create free cloudinary account

[Create Account](http://cloudinary.com/)


### 2. Installation

To install the Cloudinary Ruby GEM to gemfile:
```ruby
gem 'cloudinary'
```
Run bundle
```bash
bundle install
```

### 3. Configuration


### 4. Upload images

