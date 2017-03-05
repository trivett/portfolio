---
layout: post
title: Seed your Rails database with FFaker and Factory Girl
date: 2016-05-09 19:44:15.000000000 -05:00
type: post
published: true
status: publish
categories:
- Blog
tags:
- rails
- web development
- seeding
- tutorial
- databases

excerpt: "Make a production-like development environment in a few minutes."
---

When developing a Ruby on Rails application, it helps to simulate a real production environment. When testing out the layout of a page for instance, you need to see how your views render objects from the database in the browser. Without stuff in the database to render, you can't effectively test that functionality.

You can get quite far by manually inputing fake data through the Rails console, or using the front-end input forms on your site. This works, but there are a few drawbacks to this approach. First, if you ever have to reset your development database (it happens!) or work on another machine, you have to repeat the process to get something on the screen. Also, if you are working with a team, each developer has to input their own data. It's also impractical to manually input enough data to simulate the amount of data the production environment has to handle. Having to think of realistic fake information to put into a form can be a major time suck.

Fortunately, Rails ships with a built-in feature called _seeds_, where you can code in development and test data. With third-part gems [Factory Girl](https://github.com/thoughtbot/factory_girl) and [FFaker](https://github.com/ffaker/ffaker), you don't have to waste time typing content to get a realistic-looking development database.


## Setting up


To demonstrate, let's make a simple app called `messenger` where users can post messages, a bit like Twitter. Feel free to skip this step if you already have a suitable app to work with.

Start by initializing a new project from the command line:

```
$ rails new -d postgresql messenger
```

>We specify PostgreSQL as the database management system rather than the Rails default of SQLite. In case you aren't familiar with it, Postgres is a powerful free and open source database management system that is very popular with Rails developers. Heroku, a popular service for easily deploying web apps to the web, provides a Postgres database by default. You can use SQLite in development and Postgres in production, but keeping parity between your development and production environments helps avoid subtle, hard-to-find bugs. If it's your first time encountering Postgres, GoRails has a great [guide](https://gorails.com/setup/osx/10.10-yosemite#database) for getting started.


Once that runs, we can set up the underlying database for the app with rake:

```
$ rake db:migrate
```

This app will have two models: User and Message. Messages will belong to users, just like in a normal microblog network. We'll use the handy Rails generators to create those models and the migration files that we need to turn them into tables in the database by running the following in your terminal:

```
$ rails g model user screenname:string email:string

$ rails g model message:string body:string user:references
```

The first command gives us the `User` model and table with screenname and email as columns. If you leave off the `:string` data type, you will get the same result, as string is default. The second creates the `Message` table with body as the sole attribute. It also sets up the `belongs_to` relationship between `User` and `Message`. The `Message` model in `app/models/message.rb` already has the `belongs_to :user` code written for you. The next step is to specify the `has_many` relationship in the `User` model like so:

**app/models/user.rb**

{% highlight ruby %}

class User < ActiveRecord::Base
  has_many :messages
end
{% endhighlight %}

Now, since we created new database migrations, we have to execute them so our changes are reflected in the database:

```
$ rake db:migrate
```

You should see output along these lines:

```
$ rake db:migrate
== 20160509232809 CreateUsers: migrating ======================================
-- create_table(:users)
   -> 0.0321s
== 20160509232809 CreateUsers: migrated (0.0322s) =============================

== 20160509232816 CreateMessages: migrating ===================================
-- create_table(:messages)
   -> 0.0214s
== 20160509232816 CreateMessages: migrated (0.0215s) ==========================
```

Let's test out the setup of these models in the Rails console to make sure the relationship is right. First open the console with `$ rails console` or `$ rails c` for short. Your prompt will change to a `>` and you can enter data directly.

```
> u = User.create(screenname: "motherofdragons16", email: "dtargaryen@hotmail.com")

> m = u.messages.create(body: "burnin it up today!")
```

If this works, it proves that we can create users, and that those users have a collection of messages. We are ready to continue.

## Factory Girl and FFaker

Typing in a large number of messages for multiple users through the console can be tedious, and it wastes your precious time and creativity that should be spent coding. We are going to introduce Factory Girl and FFaker to the app to take this off of your plate.

Factory Girl might be familiar to you if you have experience testing Rails applications. This popular gem stamps out data according to a pattern for testing, kind of like how a factory cranks out hundreds of similar objects. The interface for creating instances of a class is easy to get the hang of, as you will see. Factory Girl is most often used in automated tests, but it can be called upon to manufacture data in development as well.

FFaker is another fantastic gem that comes with a massive multilingual library of realistic-looking random data such as addresses, names, screen names, companies, product names, currencies, sports, Social Security numbers, and so on. It even has ready-made pretentious catch phrases for corporations! FFaker is a natural companion to Factory Girl for filling your development or test databases, and it saves you a lot of time typing nonsense or looking up and pasting in filler text like lorem ipsum.

First, we need to declare this dependency in the `Gemfile`. Be sure to place this in the development and test groups. We don't want to fill teh production app with fake users and messages.


**Gemfile**

```
group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug'
  gem 'factory_girl_rails'
  gem 'ffaker'
end
```

As always, to use these gems, we have to install with bundler:

```
$ bundle install
```

Now we have access to `factory_girl_rails` and `ffaker` throughout the application. Without any further configuration, we can see the value of FFaker in real time in the console. Let's demonstrate with the `Company` module of the library. You can peruse the [complete FFaker reference](https://github.com/ffaker/ffaker/blob/master/REFERENCE.md) on GitHub for more ideas that might fit your app better.

```
$ rails c
> FFaker::Company.name
=> "Keebler and Sons"
> FFaker::Company.position
=> "General Secretary"
> FFaker::Company.catch_phrase
=> "Switchable clear-thinking firmware"
```

In this context, both `FFaker` and `FFaker::Company` are modules, and `.name` is a method within `FFaker::Company`. It returns a string of a somewhat believable random company name from the library. As with all open source software, you can see the [source code](https://github.com/ffaker/ffaker/blob/master/lib/ffaker/company.rb) of the gem to see how it works.

Now let's use some fake data from FFaker in conjunction with Factory Girl. The first step is to define a ruby file to act as your "factory." The default location for factories is in `test/factories`. Here is some example code for creating a factory, in this case, a factory to create users in our example app.


**test/factories/user.rb**

```
FactoryGirl.define do
  factory :user do
    screenname { FFaker::Internet.user_name }
    email { FFaker::Internet.email }
  end
end
```

This factory corresponds well to the `User` Active Record model. The screenname and email attributes will be filled with a random string from the [FFaker::Internet module](https://github.com/ffaker/ffaker/blob/master/REFERENCE.md#ffakerinternet).

Factory Girl gives you an intutive interface for cranking data out of the user factory you just built. Again, we can try it out in the console:

```
$ rails c
> FactoryGirl.create(:user)
### This makes one new user
> FactoryGirl.create_list(:user, 10)
### This makes 10 new users with one line of code!
```

These are just two methods that FactoryGirl comes with. You can find a more complete catalog of its capabilities on the project's [GitHub repo](https://github.com/thoughtbot/factory_girl/blob/master/GETTING_STARTED.md) or in the [official documentation](http://www.rubydoc.info/gems/factory_girl_rails).

You now have a tireless printing press for making users.

## Seeding your database

Rails comes with a built-in way to fill a database with stuff called _seeds_. You can find this file in `db/seeds.rb`. Essentially, anything that you run from the Rails console to create or manipulate Active Record models can be written here and be reused whenever necessary. You can seed a database with the `rake db:seed` command. In case you need to set up on a new machine or if you mess up your local database and reset it with `rake db:reset`, your whole database will be wiped out and re-seeded with `seeds.rb.`

Without Factory Girl and FFaker, you would have to manually write a `.create` statement for every object that you want to create in `seeds.rb`. Furthermore, if you seed twice with hard-coded content, you then have duplicates. This is the real strength of Factory Girl and FFaker. You can seed as much as you like in no time with little chance of duplicated data.

With those two gems, you can use a loop to make as many unique objects you want. Try this in `seeds.rb`:

**db/seeds.rb**

```
FactoryGirl.create_list(:user, 20)

User.all.each do |user|
  10.times do
    user.messages.create(body: FFaker::HipsterIpsum.phrase)
  end
end

```

The first line creates ten users with the user factory you defined earlier. The following code loops over all of the users and creates ten messages to belong to each one. The messages are nonsense generated from the [FFaker HipsterIpsum](https://github.com/ffaker/ffaker/blob/master/REFERENCE.md#ffakerhipsteripsum) module. Run `rake db:seed` and boom!

With six lines of code you have hundreds of rows in your database, all real-seeming and unique. If you want more data, you can just run `rake db:seed` again or increase the number of users or messages you create for each.

Now if you ever lose your database in development or take on a new collaborator, nobody has to type out pointless fake data to work with. You can even use this approach to test how your app handles foreign language input and the load of a huge amount of data to see how that affects performance.
