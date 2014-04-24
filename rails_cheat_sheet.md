# Rails Cheat Sheet #
This is a cheat sheet to help me with rails dev.  A lot of things in rails are worth memorizing since you don't have things like intellisense and there are SOOOO many things that are completely convention based.  So this is what I came up with while working through the [Rails Tutorial](http://ruby.railstutorial.org/), and on to my own apps.  This also assumes you have all the prereqs installed.  

## Creating a new app ##

**rails new #{app_name} --skip-test-unit** => Creates the rails project without using the built in framework.



## Gemfile ##
To update gems run the following command:

**bundle install --without production** => installs the gems.  --without production will be remembered after he first time.

**bundle update** => updates the gems

Here are some useful gems to use (or at least that I have used).


**Testing gems**

1. **rspec-rails** => Testing gem using rspec (group :development, :test)
2. **selenium-webdriver** => Browser automation. 
3. **capybara** => Simulate a user’s interaction with a web application
4. **factory\_girl_rails** => Used to create models easily in tests.  Especially in bulk

**CSS & Rails GEMS**

1. **bcrypt-ruby** => Used to transform the password to make the password hash.
2. **bootstrap-sass** => Bootstrap framework in sass form.
3. **bootstrap-will_paginate** => Used to get a quick data pager.  


**Other Gems**

1. **faker** => Used to get fake data for samples (see sample_data.rake) 


## Generating Models & Migrations ##
*Use SINGULAR for model names such as User, Micropost, Relationship.*  
*timestamps creates two magic columns called created\_at and updated\_at*

Migration files consist of a **change** method that creates, updates, or removes columns and tables

**rails generate model User name:string email:string** => Creates a model and a migration file with 

**bundle exec rake db:migrate** => Runs the data migrations.

**bundle exec rake db:rollback** => Rolls back the data migrations.

**bundle exec rake test:prepare** => Sets up the test DB

**bundle exec rspec spec/** => Runs the tests in the specified directory/file (spec/)

**Model record definitions** <br />
class User < ActiveRecord::Base
end

**Data types**
:binary
:boolean
:date
:datetime
:decimal
:float
:integer
:primary_key
:references
:string
:text
:time
:timestamp

**scope :name, where("")** allows you to call Model.scope with that where clause.  

## Controller Class Definitions ##
*Use PLURAL for controller names such as StaticPagesController(file name: static\_pages\_controller)*


class UsersController < ApplicationController

end

## Model Records (ActiveRecord::Base)

**validates(:field_name, {})** => Validates the field with the options passed in.  

## Querying with Models ##

- **with_scope** => in your model class when you define a method add the following to allow additional operations on your find.  Example:

    def self.find\_incomplete(options = {}) <br>
        with\_scope :find => options do <br> 
    find\_all\_by\_complete(false, :order => 'created_at DESC'); <br>
      end 
    end
- **find(:all).collect(&:name).collect(&:downcase)** => returns an array of the attribute.  Chainable.

## Sample data ##

1. Create a rake file like \lib\task\sample_data.rake
2. Use a gem like Faker if you need generic data
3. **bundle exec rake db:reset** => Resets the DB
4. **bundle exec rake db:populate** => Populates the database 
5. **bundle exec rake test:prepare** => Performs all the migrations on the test database