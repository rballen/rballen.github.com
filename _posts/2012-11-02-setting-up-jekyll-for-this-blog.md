---
layout: post
title: "Setting up Jekyll for this Blog"
description: "jekyll, blogging"
category: linux
tags: [blog, jekyll, linux, helloworld]
---

This new blog is being hosted for free on github along with all my code snippets and personal projects. The blogging engine is [jekyll](http://jekyllbootstrap.com/usage/jekyll-quick-start.html) and it transforms my [markdownand] (http://daringfireball.net/projects/markdown/syntax) files into html. I love markdown. Here's how I setup it up locally on ubuntu 12.04 and Mint 14. This has to be the easiest way to blog yet. 

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


## create a repository named rballen.github.com on [github.com/rballen](https://github.com/rballen) 
cd ~/Projects/github
git clone https://github.com/plusjade/jekyll-bootstrap.git rballen.github.com
cd rballen.github.com
git remote set-url origin git@github.com:rballen/rballen.github.com.git
git push origin master


## to publish after making changes or adding posts
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
   This folder is for partial views like header.html, footer.html, blogroll.html

- **\_layouts**   
   This folder is for the main templates your content will be inserted into.
   You can have different layouts for different pages or page sections - default.html, post.html templates. This files calls a file like header.html from _includes folder e.g. {% include header.html %}


- **\_posts**  
   This folder contains my markdown files. To start a new post just type 
   {% highlight bash %}
   $ rake post title="Hello World"
   {% endhighlight %}
   The file format and url format will be `@YEAR-MONTH-DATE-title.md`. You set the posts' category and tags at the top of each post. Make sure you include a 'space' after each tag if you use more than one.
{% highlight bash %}
---
layout: post
title: "Build the latest FFmpeg codecs on Ubuntu/Mint 12.04"
description: "ffmpeg, h.264, codecs, ubuntu 12.04"
category: linux
tags: [linux, codecs, a/v editing]
---
{% endhighlight %}


- **\_site**  
  Jekyll will put the generated static site here.

- **assets**  
   This folder is not part of the standard jekyll structure.
   The assets folder represents _any generic_ folder you have in your root directory. I put all my static assets like css/ img/ font/ js/ foders in side assets/ and then call them like:   <link href="/assets/css/main.css" rel="stylesheet">
 
  

## customise theme
edit  '_config.yml' with personal settings
{% highlight bash %}

 title : rballen.me
 tagline: personal blog, memory dump and other randomness 
author :
  username : rballen
  name : robert b. allen
  email : robert.burch.allen@gmail.com
  github : rballen
  twitter :  _rballen
  flickr : robert_b_allen
  feedburner : feedname

 permalink: /:categories/:year/:month/:title 
 exclude: [".rvmrc", ".rbenv-version", "README.md", "Rakefile", "changelog.md"]
 auto: true
 pygments: true

production_url : http://rballen.github.com

markdown: rdiscount
  BASE_PATH : false
  ASSET_PATH : false

    archive_path: /archive.html
  categories_path : /categories.html
  tags_path : /tags.html

  comments :
    provider : false
    disqus :
      short_name : blogrballen
      analytics :
  provider : google 
  google : 
   tracking_id : 'UA-36739274-1'
     sharing :
    provider : false
{% endhighlight %}

## jekyll commands and themes
{% highlight bash %}


## try out these themes
rake theme:install git="https://github.com/jekyllbootstrap/theme-the-program.git"
rake theme:install git="https://github.com/dhulihan/hooligan.git"
rake theme:install git="https://github.com/jekyllbootstrap/theme-tom.git"
rake theme:install git="git://github.com/jekyllbootstrap/theme-mark-reid.git"
rake theme:install git="git://github.com/sodabrew/theme-dinky.git"
rake theme:install git="https://github.com/jekyllbootstrap/theme-the-minimum.git"
rake theme:install git="https://github.com/jekyllbootstrap/theme-twitter.git"
rake theme:install git="https://github.com/mattions/theme-twitter-2.0-cyborg"

## switch
rake theme:switch name="the-program"
rake theme:switch name="hooligan"
rake theme:switch name="tom"
rake theme:switch name="mark-reid.git"
rake theme:switch name="dinky"
rake theme:switch name="the-minimum"
rake theme:switch name="twitter"
rake theme:switch name="twitter-2.0-cyborg"

#update theme
Ever time there is a new version of twitter bootstrap just drop the new files in your assets folder.

# start jekyll for testing
jekyll --server     # start server and view at: http://localhost:4000/

# create a post
rake post title="Hello World"

# create a page
rake page name="about.md"

# create a nested pages
rake page name="pages/about.md"

# customize date
{{ post.date | date: "%b %Y" }}

# generate all tags for a post
{% for tag in post.tags %}
<span class="label label-inverse">{{ tag }}</span>
{% endfor %}

# get the single category per post
{{post.category }}

{% endhighlight %}


## plugins
* [mail] (https://github.com/masukomi/JekyllMail)
* [analytics] (http://www.google.com/analytics)
* [disqus] (http://disqus.com/)
* [feedburner] (http://feedburner.google.com/)
