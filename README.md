# Intro to Deploying

## Learning Goals

- Understand what "deploying" means
- Understand the responsibilities of a web server
- Evaluate platforms for deploying Rails applications

## Introduction

So far during this phase, we've been working on developing applications and
running them locally on our own computers. If we want other folks to be able to
interact with our applications, that means we need to deploy them to another
computer that's configured to allow requests over the internet, from anywhere in
the world!

This process essentially involves:

- taking our application's code
- uploading it to a server that's configured to run our code and allow HTTP
  requests
- running our code on that server

As a web developer, it's essential to familiarize yourself with the development
process for a few reasons:

- It's increasingly expected that developers participate in the deployment
  process. While many companies employ specialized DevOps (Developer Operations)
  engineers, it is not uncommon for engineers on other teams to have a hand in
  deploying and troubleshooting issues in production.
- Deploying your site early in the development process can be helpful for
  catching bugs that you may not encounter running your code locally,
  particularly when it comes to project dependencies and working with
  third-party services.
- Understanding how your app will perform in different environments (development
  and production) can help you optimize your code's performance.

In this lesson, we'll explore the deploying process and identify the needs of a
web server for hosting a Rails application.

## Defining a Web Server

All web servers share the same common goal: they must be able to handle HTTP
requests, and send back a response. The simplest kind of websites are known as
[**static** websites][static web page], which typically means sites that store
all their content in pre-built HTML files which are saved to the file system and
sent back when a client makes a request for that specific file:

![static server diagram](https://curriculum-content.s3.amazonaws.com/phase-4/phase-4-intro-to-deploying/static-server.png)

[static web page]: https://en.wikipedia.org/wiki/Static_web_page

Static websites are still quite common on the web; but there's also a large portion
of the web that is [**dynamic**][dynamic web page], which means that the content
returned from an HTTP request isn't derived from just a HTML file, but instead is
processed by some code running on the server before being sent back to the client.
All Rails applications are **dynamic**, since every request needs to be processed
by Rails in order to determine the correct response.

[dynamic web page]: https://en.wikipedia.org/wiki/Dynamic_web_page

![dynamic server diagram](https://curriculum-content.s3.amazonaws.com/phase-4/phase-4-intro-to-deploying/dynamic-server.png)

Since hosting a server for dynamic websites is a bit more complicated, let's
discuss some things a dynamic server needs in order to do its job.

## Application Environment

Take a moment to think about all the things that are required to run a
Rails application. When you're working on a lab, what setup is needed so
that you can type `rails s` in the terminal, and view your website in the
browser?

For starters, there's your _environment setup_: you could be running on OSX, or
WLS, or Linux; you'll need to have a recent version of Ruby installed; you'll
need Git for version control; and a few other system dependencies.

There are also all of your _application dependencies_: the code specific to
your Rails app that needs to run. That includes the Rails gem itself as well
as all the other gems in your Gemfile.

You'll also need some kind of _database_ to persist all your data. It's helpful
to think of the database in isolation from the rest of your application, as a
kind of resource that's available to your Rails app; ideally, even if your Rails
app goes down for some reason, your database shouldn't go down with it!

> A note on databases: for the labs in this phase, we've been using SQLite as a
> lightweight database. It's great for quick development, but it doesn't scale
> well to larger applications. We'll be using Postgres for our database moving
> forward. More on that later!

Since all of these elements are required in order to run our application,
whatever system we choose to deploy our code on will need to be able to handle a
similar environment setup. Let's explore some options.

## Deploying Options

When it comes to deciding on which platform to use to host our deployed
applications, there are a number of options, each of which comes with some
tradeoffs. For Rails in particular, a few popular choices are:

- [Heroku][heroku]
- [Amazon Web Services (AWS)][aws]
- [Digital Ocean][digital ocean]

[heroku]: https://www.heroku.com/about
[aws]: https://aws.amazon.com/
[digital ocean]: https://www.digitalocean.com/

One thing these services all have in common: they all have the ability to easily
configure an environment to run our Rails applications in. These services own
the hardware (the physical servers and networking infrastructure) that your code
will run on, but they also have configurable [**containers**][containers] with
resources dedicated to run your code.

[containers]: https://en.wikipedia.org/wiki/OS-level_virtualization

There are a lot of considerations when it comes to choosing a platform for
deploying your application, such as:

- **Cost**: How much will this platform charge me? How much do I get for free?
  Flat rate per month? Calculated based on usage?
- **Ease of use**: How much work does it take to deploy my application the first
  time? How easy is it to deploy new versions?
- **Scalability**: As my application gets more users, how easy is it to handle
  increased traffic?
- **Performance**: Does my application need to handle a lot of traffic? Be optimized
  for video processing? Store a lot of files? Handle large database tables?

For now, since we're deploying our very first Rails projects, we're going to
prioritize **cost** and **ease of use** to decide on a platform, and use Heroku
for deploying in the coming lessons.

[Heroku][heroku] is first and foremost a Platform as a Service (PaaS), which
means they manage the hardware your code runs on as well as the software
environment, with an aim of making it as simple as possible to take the code
from your machine and run it on theirs. Heroku also has a free tier for
developers to try out the service at no cost.

[AWS's Elastic Beanstalk][elastic beanstalk] and
[Digital Ocean's App Platform][app platform] are both Platform as a Service
options as well, so you're welcome to try them out for future projects if you're
interested in exploring other options.

[elastic beanstalk]: https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/ruby-rails-tutorial.html
[app platform]: https://docs.digitalocean.com/products/app-platform/languages-frameworks/ruby-on-rails/

The downside to PaaS options is that they tend to cost more in the long run as
your application scales up, since you're not only paying for the hardware your
code runs on, you're also paying for the platform maintenance and security. They
also tend to make it more challenging to fine-tune the environment in a way that
is optimal for _your_ specific application, rather than _all_ applications
running on their service.

The upside is that compared to handling that configuration ourselves, using Heroku
will make it much easier to get our app up and running in a production environment
on a server.

## Conclusion

The end goal of developing web applications is to share them with the world, and
deploying is the crucial last step in this process! As a developer, it's
important to equip yourself with the knowledge of what it takes to deploy a
website so you can evaluate the available options and choose the right one for
your project.

In the coming lessons, we'll go through that deployment process with a couple of
applications of varying complexity so you can build the confidence to deploy your
own projects independently.
