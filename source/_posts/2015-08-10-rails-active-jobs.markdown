---
layout: post
title: "Rails Active Jobs"
date: 2015-08-10 17:36:46 -0400
comments: true
categories: 
---

In some applications you may require a repitive job to be executed after a specific action or time period. Active Job allows us to schedule specific jobs that will execute automatically! Some of these tasks may be to send emails, clear a database, send a newsletter, generate a report, etc. 

Many large applications that handle images typically will run resource heavy jobs whenever server resources are available or in off hours. A common example is resizing images. Think about it. What if your app required 5 different sizes of the same image. You don't want to resize every single image uploaded as soon as it is uploaded! That can be crazy, especially during your sites peak hours. Instead you can schedule a job to run when your site traffic is low and your server resources are available.


<h3>Creating a Job:</h3>

``` ruby
rails g job SuperImportantJob
```
creates
``` ruby
class SuperimportantJob < ActiveJob::Base
  queue_as :default
  #queue is automatically set to :default
  def perform(user)
    # Do something later
    user.gather_all_user_external_data_evil
  end
end
```

<h3>Using a Job...</h3>

To actually use this job you need can call it in your controller, or model.... model is probably best.
Lets say you have a model for a User. Whenever a User is created we want to run a job that gets some data about them so we can sell better targeted ads.

Below is the User Model where you define a method you wish to run at a later time.

``` ruby
class User < ActiveRecord::Base
  validates_presence_of :email
  validates_presence_of :name
  validates_presence_of :facebook
  validates_presence_of :instagram
  validates_presence_of :twitter
  after_create :gather_all_user_external_data

  def gather_all_user_external_data
    #scrape their facebook and save it all!!!!!
    #scrape their twitter and save it all!!!!!!
    #scrape their instagram and save it all!!!!
    #save it to the DB so we can sell some targeted ads!
  end
end
```
Here is when we actually call the job to run. The SuperimportantJob is scheduled to run #gather_all_user_external_data after 24 hours. 

``` ruby
SuperimportantJob.enqueue_at(24.hours.from_now, user1)
```

<h3>Queue</h3>
The job queue. Active Job comes with a default queue which basically means that a job will run immediately unless you specify otherwise or add a queueing adapter to your backend. EX: 
``` ruby
SuperimportantJob.set(wait:2.weeks).perform_later(gather_all_user_external_data)
```
<h4>Adding a Queue Adapter</h4>
If you want more control over your queue you can use an external adapter. Some popular adapters are sidekiq, and resque. It is simple to set up your queue adapter. Simply add the below code to your application.rb file. Sidekiq seems to be a popular choice.
``` ruby
config.active_job.queue_adapter = :sidekiq
```


Currently I do not have any practical uses for Jobs however I do see the value of having these when an application actually has some users or when I have to do the same thing everyday. Since we basically follow the convention of DRY (do not repeat yourself) in coding, we can follow this convention when we are executing code thanks to Jobs and Queues. 



Sources: 
http://guides.rubyonrails.org/active_job_basics.html
https://blog.engineyard.com/2014/getting-started-with-active-job
https://github.com/RailsApps/rails-mailinglist-activejob