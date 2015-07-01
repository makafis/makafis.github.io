---
layout: post
title: "config.ru and setting your 404 page"
date: 2015-06-30 17:54:56 -0400
comments: true
categories: 
author: Vincent Alfieri
---


<h2>config.ru<sub>Not the Russian website</sub></h2>

This file is required when using any type of Rack or Rails app. 

Instead of writing a script to start an application you can use Shotgun or Rackup to automatically launch the stack you have inside of your config.ru file.  The content of this file will tell the Rack::Builder what middleware should be used and in what order. 

Contents:
You should require your environment.
Next you should list your middleware stack. The lowest level of the stack uses the RUN command.
All other stack controllers you wish to use are listed with the USE command.
``` ruby
use AnothernotsobigController
use AnotherController
run ApplicationController
```



You can also change the port you run your application on during test. 
``` ruby
shotgun --port=6666
```



<h2>Creating your own custom 404 page in Sinatra!!!!!</h2>
I always wanted a slick and clever 404 page. 

Its pretty simple to implement. 

Sooooo inside of your main ApplicationController
Just add the following code!

``` ruby
set :show_exceptions, false
not_found do
  status 404
  erb :'404'
end
```

A little explanation for line 1. Since we work in the Development environment the 404 page will never appear. To fix this you can either change environment in the environment.rb file or you can just change the :show_exceptions value to false. 

Now you must create a '404' erb file. This is simple HTML so you should already know how to do that. If not. Googles!

And now whenever someone goes to a page that does not exist you will get an awesome 404 page.
<img src="http://httpstatusrappers.com/images/404.png" />