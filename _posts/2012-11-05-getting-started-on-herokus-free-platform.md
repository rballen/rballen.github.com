---
layout: post
title: "Getting Started on Heroku's Free Platform"
description: "heroku"
category: workflow
tags: [heroku, free]
---
Getting started on Heroku (cedar) [heroku](http://heroku.com) using mongodb. My current distro is Linux Mint 14 Cinnamon.

{% highlight bash %}

wget -qO- https://toolbelt.heroku.com/install-ubuntu.sh | sh

heroku addons:add mongolab:starter


$ heroku login
Enter your Heroku credentials.
Email: bert@example.com
Password:
Could not find an existing public key.
Would you like to generate one? [Yn]
Generating new SSH public key.
Uploading ssh public key /home/ra/.ssh/id_rsa.pub

$ cd ~/myapp
$ heroku create
Creating stark-fog-398... done, stack is cedar
http://stark-fog-398.herokuapp.com/ | git@heroku.com:stark-fog-398.git
Git remote heroku added


$ heroku create
Created sushi.herokuapp.com | git@heroku.com:sushi.git

$ git push heroku master
-----> Heroku receiving push
-----> Rails app detected
-----> Compiled slug size is 8.0MB
-----> Launching... done, v1
http://sushi.herokuapp.com deployed to Heroku

$ heroku ps
=== web: `bundle exec rails server -p $PORT`
web.1: up for 6s
=== worker: `bundle exec rake resque:work QUEUE=*`
worker.1: up for 5s

$ heroku logs --tail
2011-05-31 04:04:48 heroku[router]   GET / dyno=web.1
2011-05-31 04:04:48 app[web.1]       66.75.123.123 - -

{% endhighlight %}


...tbc
