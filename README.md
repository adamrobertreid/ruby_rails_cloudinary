# ruby_rails_cloudinary

## Getting Started

We're going to create a simple photo app. You will be able to upload photos to a cloud and then pull the iamges
back through a super fast CDN. We will be using two gems in our app `'carrierwave'` & `'cloudinary'`.

* create simple ruby on rails app
* install `gem 'carrierwave'`, `gem 'cloudinary'`
* upload photo
* display photo through CDN to DOM

## Basic Ruby on Rails new App Setup

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

## Users Controller 

Let's go ahead and great a users controller
```bash
rails g controller users
```

## Users model

```bash
rails generate model Users user:string
```
```bash
rake db:migrate
```
you schema will look like this
```ruby
  create_table "users", force: :cascade do |t|
    t.string   "user"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
```


# Cloudinary getting started guide

### 1. Create free cloudinary account

Sign-up for a free account.
[Create Account](http://cloudinary.com/)



### 2. Installation

To install the Cloudinary Ruby GEM to gemfile:
```ruby
gem 'carrierwave'
gem 'cloudinary'
```

Run bundle
```bash
bundle install
```
Start off by generating an uploader:
```bash
rails generate uploader Picture
```
this should give you a file in:
```bash
app/uploaders/picture_uploader.rb
```

add to /uploaders/picture_uploader.rb
```ruby
class PictureUploader < CarrierWave::Uploader::Base

include Cloudinary::CarrierWave

end
```

### 3. ActiveRecord

Add a string column to the model you want to mount the uploader by creating a migration:
(alternatively you could plan to already have `picture:string` to your table upon first creation)

```bash
rails g migration add_picture_to_users picture:string
rake db:migrate
```
Open your model file and mount the uploader:

```ruby
class User < ActiveRecord::Base
  mount_uploader :picture, PictureUploader
end
```


### 4. Upload images & Create users view

In our HTML form for Post editing, we add a File field for uploading the picture and also a hidden cache field for supporting page reloading and validation errors while not losing the uploaded picture.
```ruby
<%= form_for @user do |f| %>
<%= f.file_field :picture %>
<%= f.hidden_field(:picture_cache) %>
<%= f.submit "Submit" %>
<% end %>
```

This image tag works with cloudinary gem to handle getting your images from the cloud. We will use this in the next step.
```ruby
<%= cl_image_tag %>
```

in your views in '/app/views/users/index.html.erb' alternatively you could have a pictures views
and paste this in there.
```ruby
<section class="picture-layout">
  <header class="row bio-info">
    <section class="picture">
      <div class="col-sm-6 profile-1">
        <div class="picture-img">
          <%= cl_image_tag(@user.picture.url) %>
          
          <span style="vertical-align:middle">
            <%= form_for @user do |f| %>
            <%= f.file_field :picture %>
            <%= f.hidden_field(:picture_cache) %>
            <%= f.submit "Submit" %>
            <% end %>
          </span>
        </div>
      </div>
```
