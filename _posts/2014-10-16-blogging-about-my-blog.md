---
title: "Blogging About My Blog (The Who, Why, and the How)"
tags: [technology, life]
---

After a year and a half of telling myself that I was going to start a blog, I finally did it!

##Who I Am
I am a second year software engineering student at the University of Waterloo, and in this post, I will be discussing why I started this blog, why I chose Jekyll, and a bit about my design decisions and blog setup.

##Why I Am Blogging
In my several years of programming, I have repeatedly experienced the same dilemma: I would encounter a particularly difficult programming challenge, tackle it, and finally solve it after a lot of hacking and hard work. However, despite all the effort that I put into solving the problem, I would realize in perhaps a week's time, that I had completely forgotten how to solve it, and be sitting perplexed in face of the same problem. After a while of facing this dilemma, I realized that if I started a blog, then it would serve as a multi-purpose solution to both myself and others:

- a refresher for myself about problems that I have previously encountered and how to solve them
- a refresher on how to do cool things
- a resource for others to learn from based on my experiences
- an outlet for my perspective on things

##Why Jekyll
For my blogging platform, I decided to go with raw Jekyll with GitHub pages, rather than using a blogging framework such as WordPress or Octopress.

This was partially due to the fact that a lot of programmers that I admire, including Phil Haack, whose blog can be found at [haacked.com](http://haacked.com/), but my reason also has to do with the function and speed of Jekyll.

Jekyll is a blog aware, static site generator, which basically means that rather than using server-side software to load content from a database, Jekyll generates static HTML pages for my blog, thereby skipping the overhead of a server-sided CMS. This results in faster loading of pages.

When choosing Jekyll, there were two routes I could have taken: raw Jekyll or using a blogging framework such as Octopress. An advantage of Octopress is that there are a lot of plug-ins developed for it, and it is user-friendly to set up. However, I would need to manually generate the site with Jekyll, then push my changes to the server every time that I wanted to add a new post to my blog. This is where raw Jekyll shines; GitHub Pages works with raw Jekyll in that whenever I push my changes to GitHub, it will automatically run the content through Jekyll (more information can be found [here](https://help.github.com/articles/using-jekyll-with-pages/). This allows me to use GitHub itself as a content management system, editing and publish posts through the browser only, which is pretty neat, and the route I decided to take.


##Blog Setup
When building my blog, my workflow consisted of a Ubuntu virtual machine where I tested my builds locally, before pushing my changes onto GitHub, where it would be run through Jekyll and published to the web.

###My Development Environment
My Ubuntu virtual machine is where I did all my development and experimentation. In order to set it up as the development machine, I installed rbenv, libssl-dev, ruby-build plug-in, ruby, jekyll, nodejs, and git. I set it up with the following script:

```bash
#This script prepares a Debian-based Linux box (particularly Ubuntu) for setting up a simple Jekyll demo
RUBYVERSION=2.1.2 #Ruby Version to install (a list can be displayed with 'rbenv install -l')

# sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev #install git dependencies (usually pre-installed)
sudo apt-get install git

git clone https://github.com/sstephenson/rbenv.git ~/.rbenv #Check out rbenv into ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc #Add ~/.rbenv/bin to $PATH for access to the rbenv command-line utility. (For non-Ubuntu distros, replace .bashrc with .bash_profile)
echo 'eval "$(rbenv init -)"' >> ~/.bashrc #Add rbenv init to shell to enable shims and autocompletion

#Note that the shell has to be restarted for the changes to be effective.

git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build #install ruby-build as plug-in

sudo apt-get install libssl-dev #install dependency required to install Ruby

rbenv install $RUBYVERSION #install ruby
rbenv rehash #install shims for all ruby versions
rbenv global $RUBYVERSION #set $RUBYVERSION as version to use in all shells

sudo apt-get install nodejs #only necessary if linux box does not have javascript runtime

gem install jekyll #rubygems is included with most of the later ruby distributions
jekyll new myblog
cd myblog
jekyll serve

#a boilerplate jekyll blog should now be up on localhost:4000

#To set up a template:
#sudo gem install bundler
#bundle install
#jekyll serve
```

###My Production Environment
The production environment is basically GitHub Pages, and the repository that is hosted on GitHub. In order to add content or remove content, I simply need to go to [github.com/clemmy/clemmy.github.io](http://github.com/clemmy/clemmy.github.io/) and make changes through GitHub's in-browser editor.

##Closing
Whew, this was a very long post. I will be wrapping this up now, but I am quite pleased that I finally got this load off my shoulders. Until next time!

![Yay!](../images/in_post_images/yay.jpg)

<!--end-->
