---
layout: post
title: "Solutions for processing background jobs from a Rails app : A comparison"
date: 2012-06-28 23:02
comments: true
categories: [programming, asynchronous, scaling, queueing, async, resque, sidekiq, delayed_job, rails]
published: false
---

When you are writing a web application, you want the app to be
responsive to the user as well as highly available to multiple
users. Both these requirements mean that your app ought not to get tied
up with a long running task. But large applications invariably have
tasks that take a while to run. For e.g. when you fork a huge repository
on Github, if the Github Rails app waited for the forking to end, it
would be unable to serve any other requests until it was done. This
leads to lower availability hence fewer concurrent requests can be
served. How do you get around this problem? By using background worker
threads that do the processing for you.

Now, the questions arises, how do you safely delegate tasks to these
background workers with the assurance that the task will eventually get
done? This is where background processing solutions matter. Most
background processing solutions involve the use of a persistent queue,
where you can add jobs. Then you can fire up workers who consume jobs
from the queue and perform it in the background. Now, all that your
application needs to do is to 'enqueue' a job and get back to doing
whatever it is that needs to be done. The app can rest assured that some
worker thread will eventually pick up the job and application.

Here are some of the solutions that are available and easy to integrate
into your Rails app.

### Resque

### Sidekiq

### Delayed Job
