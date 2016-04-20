---
title: "Reproducible Development Environments with Vagrant"
tags: [technology]
layout: post
date: 2014-11-16
---

Hey everyone! I can't believe it has been an entire month since my last post. I have been quite busy with midterms and job interviews. Hopefully I will be posting more frequently from now on though. In this post, I will be discussing why I started using Vagrant, and what it is.

##The Backstory

At [EngHack](https://www.facebook.com/events/866943706671962/) a couple of weeks ago, I decided to hack away at a web application that was composed of mainly Javascript. The plan was to simply develop on my Ubuntu box. Little did I expect that as I was managing some dependencies and installation, I would somehow destroy my virtual machine with almost irreversible changes. As a result, I spent a significant portion of my time trying to fix my environment, and wasting valuable time at a time-constrained event. The lesson I took here was to have some sort of backup mechanism where I could fall back to quickly in the event that I break something in my environment, and that is when I remembered [Vagrant](https://www.vagrantup.com/).

##What is Vagrant

I have actually heard about Vagrant from one of my close friends over the summer while we were sharing our co-op experiences to each other, but never found a reason to invest time into learning about it. However, its uses are now apparent, and it solves my problem as well as a couple of others; Vagrant is a wrapper around virtualization technologies that provides reproducible and configurable environments through commands as simple as:

~~~
$ vagrant init hashicorp/precise32
$ vagrant up
~~~

##My Setup

Since I was using Vagrant on my personal computer and there are no strict performance requirements except for my own convenience, I made certain choices in my setup which may be unfavourable in an industry environment, which I will explain below. Below are the steps I took to create a box customized for development with the MEAN stack.

###The Base Box

In Vagrant, the base box is a package which contains the bare minimum of software which allows Vagrant to function. These boxes are provider specific (i.e. differently packaged for VirtualBox, VMWare, etc.) In my setup, I choose a pre-made box that is uploaded on [Vagrant Cloud](https://vagrantcloud.com) since creating a base box from scratch is a lot of work. The base box I started with is [box-cutter/ubuntu1404-desktop](https://vagrantcloud.com/box-cutter/boxes/ubuntu1404-desktop). Personally, I chose the Desktop version of Ubuntu because it is convenient working with a GUI. Productivity is increased and since performance is not a concern on my personal computer, there are no downsides. However, when performance is important, it may be wise to use a server distribution instead, and work headlessly via SSH.

###Provisioning

Provisioning installs software and alters configurations in the virtual machine. In Vagrant, there are several approaches to take when provisioning:

- using a configuration management system such as Puppet, CFEngine, or Chef
- using a shell script

I opted for the latter option because I was simply using Vagrant on my personal computer as a safety net. For my purposes, I would barely be recreating the virtual machine; I would only need to re-provision when something goes horrendously wrong and I need to fall back. Therefore, I had no need for the power of a configuration management system, which has a learning curve attached to it. Configuration management systems would be more useful in scenarios where a consistent development environment system needed to be deployed to a bunch of different virtual machines, perhaps of varying operating systems; configuration management systems standardize dependencies and make it easier to manage dependencies over a large number of disposable boxes.

My mean.sh provisioning script contains the following:

{% highlight bash linenos %}
#Install git
sudo apt-get install -y git

#Install Node.js
git clone https://github.com/joyent/node.git
cd node
./configure
make
sudo make install

#Install MongoDB
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 #import public key used by package management system
echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list #create a list file for MongoDB
sudo apt-get update # update local package database
sudo apt-get install -y mongodb-org # install latest version

#Install Express.js
sudo npm install -g express
{% endhighlight %}

As you can see, it is very minimal. One thing to note is the '-y' flag used in ```apt-get install```
which assumes yes for all the yes/no prompts which will break the installation script.

###My Vagrantfile

The Vagrantfile basically contains the configuration for the entire box. My entire configuration can be found [here](https://gist.github.com/Clemmy/20119b71c17612f0df13). I will be highlighting the different parts of it below.


~~~
config.vm.box = "box-cutter/ubuntu1404-desktop"
~~~

This part specifies the base box.

~~~
config.vm.network "private_network", ip: "192.168.33.10"
~~~

This part creates a private network which allows the host to access the box through the specified IP address.

~~~
config.vm.provider "virtualbox" do |vb|
  vb.gui = true

  vb.customize ["modifyvm", :id, "--memory", "2048"]
  vb.customize ["modifyvm", :id, "--cpus", "2"]
end
~~~

This part tells VirtualBox to display the GUI and also modifies some of the default hardware settings. When I first built my virtual machine with Vagrant, it was terribly slow, so I allocated more RAM and processing power to it. The recommended amount of RAM to let the VM use is 1/4th the system RAM according to what I read online.

~~~
config.vm.provision "shell", path: "mean.sh"
~~~

This part specifies the path of the external shell script to be used for provisioning. The path is relative, so mean.sh should be placed in the same directory as Vagrantfile.

##Closing
And that's it! That is how I set up Vagrant to be able to recreate my development environments from a specific snapshot whenever I want to. Hopefully this solves dependency management problems for anyone who may be reading it. Happy developing!

<!--end-->
