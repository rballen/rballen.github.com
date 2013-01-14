---
layout: post
title: "Using Vagrant and Puppet to Build a Virtual Dev Box"
description: ""
category: workflow
tags: [vagrant, virtualbox, vm, puppet ]
---


## Vagrant Installation

1. install [virtualbox] (https://www.virtualbox.org/wiki/Downloads), virtualbox guest additions, dkms, ruby1.9.3
1. download and install latest [vagrant] (http://downloads.vagrantup.com/) version
1. read the [getting-started] (http://vagrantup.com/v1/docs/getting-started/index.html) guide for details
1. add /opt/vagrant/bin to $PATH on Linux
1. sudo apt-get install puppet-common
1. sudo apt-get install nfs-common nfs-kernel-server


## Base Box
I'm building my own base box on Mint 14 using ubuntu-12.04.1-alternate-i386. This box will be the base template for all future vm's I need. There are some prebuilt boxes running different distros and software stacks at [vagrantbox.es] (http://vagrantbox.es) and 

{% highlight bash %}


## vagrant commands
vagrant box add webdevbox ~/Projects/vagrant/vagrant-ubuntu-precise-32/package.box
vagrant box list 
vagrant init webdevbox
vagrant up webdevbox
vagrant ssh webdevbox
wget -qO- 127.0.0.1

vagrant reload


mkdir test-ubuntu-precise-64
$ cd test-ubuntu-precise-64
$ vagrant init ubuntu-precise-64
$ vagrant up

# suspend vm and save state
vagrant suspend --> vagrant resume

# shutdown vm
vagrant halt --> vagrant up

# completely destroy vm
vagrant destroy
ope
mkdir webdevbox
vagrant webdevbox



## Building Base Box
1. fork https://github.com/cal/vagrant-ubuntu-precise-64.git and update per the README.md file
2. ./build.sh

# other devs can later clone your base by
vagrant box add my_box /path/to/the/package.box
vagrant init my_box
vagrant up


    Debian/Ubuntu


## Install Ruby, Ruby Gems and Vagrant
sudo apt-get install rubygems
sudo apt-get install ruby-dev
sudo apt-get install build-essential
sudo gem install vagrant
# Add the ruby gems path to your path
PATH=$PATH:/var/lib/gems/1.8/bin
# Download and install VirtualBox
echo 'echo "deb http://download.virtualbox.org/virtualbox/debian maverick contrib" >> /etc/apt/sources.list' | sudo sh
wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -O- | sudo apt-key add -
sudo apt-get update
sudo apt-get install virtualbox-4.0
sudo apt-get install dkms

You should now be able to type vagrant in your terminal and see the list of tasks that yo

$ vagrant
Tasks:
  vagrant box                        # Commands to manage system boxes
  vagrant destroy                    # Destroy the environment, deleting the created virtual machines
  vagrant halt                       # Halt the running VMs in the environment
  vagrant help [TASK]                # Describe available tasks or one specific task
  vagrant init [box_name] [box_url]  # Initializes the current folder for Vagrant usage
  vagrant package                    # Package a Vagrant environment for distribution
  vagrant provision                  # Rerun the provisioning scripts on a running VM
  vagrant reload                     # Reload the environment, halting it then restarting it.
  vagrant resume                     # Resume a suspended Vagrant environment.
  vagrant ssh                        # SSH into the currently running Vagrant environment.
  vagrant ssh_config                 # outputs .ssh/config valid syntax for connecting to this environment via ssh
  vagrant status                     # Shows the status of the current Vagrant environment.
  vagrant suspend                    # Suspend a running Vagrant environment.
  vagrant up                         # Creates the Vagrant environment
  vagrant version                    # Prints the Vagrant version informatio

{% endhighlight %}
