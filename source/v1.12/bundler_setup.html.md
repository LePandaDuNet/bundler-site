---
title: Bundler setup
description: Configure the load path so all dependencies in your Gemfile can be required
---

## Bundler.setup

Configure the load path so all dependencies in
your Gemfile can be required

~~~ ruby
require 'rubygems'
require 'bundler/setup'
require 'nokogiri'
~~~

Only add gems from specified groups to the
load path. If you want the gems in the
default group, make sure to include it

~~~ ruby
require 'rubygems'
require 'bundler'
Bundler.setup(:default, :ci)
require 'nokogiri'
~~~

<a href="/groups.html" class="btn btn-primary">Learn More: Groups</a>

## Compatibility

Ruby 2.0 and RubyGems 2.0 both require Bundler 1.3 or later. If you have questions about compatibility between Bundler and your system, please check the compatibility list.

<a href="/compatibility.html" class="btn btn-primary">Learn More: Compatibility</a>

## Setting Up Your Application to Use Bundler

Bundler makes sure that Ruby can find all of the gems in the <code>Gemfile</code>
(and all of their dependencies). If your app is a Rails 3 app, your default application
already has the code necessary to invoke bundler. If it is a Rails 2.3 app, please see:
<a href="./rails23.html">Setting up Bundler in Rails 2.3</a>

For another kind of application (such as a Sinatra application), you will need to set up
bundler before trying to require any gems. At the top of the first file that your
application loads (for Sinatra, the file that calls <code>require 'sinatra'</code>), put
the following code:

~~~ ruby
require 'rubygems'
require 'bundler/setup'
~~~

This will automatically discover your <code>Gemfile</code>, and make all of the gems in
your <code>Gemfile</code> available to Ruby (in technical terms, it puts the gems "on the
load path"). You can think of it as an adding some extra powers to <code>require
'rubygems'</code>.

Now that your code is available to Ruby, you can require the gems that you need. For
instance, you can <code>require 'sinatra'</code>. If you have a lot of dependencies, you
might want to say "require all of the gems in my <code>Gemfile</code>". To do this, put
the following code immediately following <code>require 'bundler/setup'</code>:

~~~ ruby
Bundler.require(:default)
~~~

For our example Gemfile, this line is exactly equivalent to:

~~~ ruby
require 'rails'
require 'rack-cache'
require 'nokogiri'
~~~

For such a small <code>Gemfile</code>, we'd advise you to skip
<code>Bundler.require</code> and just require the gems by hand. For much
larger <code>Gemfile</code>s, using <code>Bundler.require</code> allows you to skip
repeating a large stack of requirements.
