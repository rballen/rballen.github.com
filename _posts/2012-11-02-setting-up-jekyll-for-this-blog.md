---
layout: post
title: "Setting up jekyll for this blog"
description: "jekyll, blogging"
category: linux
tags: [blog,jekyll,linux,helloworld]
---
{% include JB/setup %}

This latest blog incarnation is being hosted for free on github along with all my code and snippets. The blogging engine is [jekyll](http://jekyllbootstrap.com/usage/jekyll-quick-start.html) and here's how I setup it up on ubuntu 12.04 and Mint 14.

## installation 

{% highlight bash %}
sudo apt-get install -y ruby1.9.3 
# add the line below to  ~/.profile
export PATH=/home/ra/.gem/ruby/1.9.1:$PATH
sudo gem update
sudo gem install bundler
sudo apt-get install -y libjpeg-turbo-progs optipng 
sudo gem install jekyll rake
sudo apt-get install python-pygments

# create a repository named rballen.github.com on [github.com/rballen](https://github.com/rballen) 
cd ~/Projects/github
git clone https://github.com/plusjade/jekyll-bootstrap.git rballen.github.com
cd rballen.github.com
git remote set-url origin git@github.com:rballen/rballen.github.com.git
git push origin master

# to publish after making changes or adding posts
git add .
git commit -m "Add new content"
git push origin master

{% endhighlight %}

## jekyll layout

Jekyll expects your website directory to be laid out like so:

    .
    |-- _config.yml
    |-- _includes
    |-- _layouts
    |   |-- default.html
    |   |-- post.html
    |-- _posts
    |   |-- 20011-10-25-open-source-is-good.markdown
    |   |-- 20011-04-26-hello-world.markdown
    |-- _site
    |-- index.html
    |-- assets
        |-- css
            |-- style.css
        |-- javascripts


- **\_config.yml**  
   Stores configuration data.

- **\_includes**  
   This folder is for partial views.

- **\_layouts**   
   This folder is for the main templates your content will be inserted into.
   You can have different layouts for different pages or page sections.

- **\_posts**  
   This folder contains your dynamic content/posts.
   the naming format is required to be `@YEAR-MONTH-DATE-title.MARKUP@`.

- **\_site**  
   This is where the generated site will be placed once Jekyll is done transforming it. 

- **assets**  
   This folder is not part of the standard jekyll structure.
   The assets folder represents _any generic_ folder you happen to create in your root directory.
   Directories and files not properly formatted for jekyll will be left untouched for you to serve normally.

## customise theme
edit  '_config.yml' with personal settings

> title : rballen.me
> tagline: personal blog, memory dump and other randomness 
> author :
> name : rballen
> email : 
> github : rballen
> google analytics, disqus, twitter, feedburner

remove Supporting tagline from includes/themes/twitter/post.html
## jekyll commands and themes
{% highlight bash %}

# try out these themes
rake theme:install git="https://github.com/jekyllbootstrap/theme-the-program.git"
rake theme:install git="https://github.com/dhulihan/hooligan.git"
rake theme:install git="https://github.com/jekyllbootstrap/theme-tom.git"
rake theme:install git="git://github.com/jekyllbootstrap/theme-mark-reid.git"
rake theme:install git="git://github.com/sodabrew/theme-dinky.git"
rake theme:install git="https://github.com/jekyllbootstrap/theme-the-minimum.git"
rake theme:install git="https://github.com/jekyllbootstrap/theme-twitter.git"
rake theme:install git="https://github.com/mattions/theme-twitter-2.0-cyborg"
# switch
rake theme:switch name="the-program"
rake theme:switch name="hooligan"
rake theme:switch name="tom"
rake theme:switch name="mark-reid.git"
rake theme:switch name="dinky"
rake theme:switch name="the-minimum"
rake theme:switch name="twitter"
rake theme:switch name="twitter-2.0-cyborg"
# start jekyll for testing
jekyll --server     # start server and view at: http://localhost:4000/

# create a post
rake post title="Hello World"

# create a page
rake page name="about.md"
# create a nested pages
rake page name="pages/about.md"
{% endhighlight %}


## plugins
* [mail] (https://github.com/masukomi/JekyllMail)
* [analytics] (http://www.google.com/analytics)
* [disqus] (http://disqus.com/)
* [feedburner] (http://feedburner.google.com/)
