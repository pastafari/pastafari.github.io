---
layout: post
title: "Our experience with Vagrant and Puppet"
date: 2012-06-03 18:14
comments: true
categories: [Programming, Thoughtworks, Vagrant, Puppet]
---
On my current project, after a bit of prodding by [Sunit](http://twitter.com/sunitparekh) we decided to experiment with using a virtual
machine setup managed through [Vagrant](http://vagrantup.com) and [Virtual Box](http://virtualbox.org) for our development
environment. 

In this post I will try and outline the pros and cons and
lessons learnt over the past week while pairing with
[Ginette](http://twitter.com/vginette) and setting up our own VM
managed with Vagrant. 

## Why Vagrant?

Our project uses Rails with Postgres and Nginx/Passenger. We also use RVM to manage Ruby versions.

The reasons to use Vagrant were primarily these:

* Use **_one VM per project_** without cluttering your main machine with the sundry dependencies (MySQL, Postgres, Redis,
Apache, Nginx, Passenger, et al) that projects invariably have.
* Have a **_5 minute setup_** for any new developer who joins our team to
  get up and running. This should be as easy as running a single
  command: `vagrant up`. No installation, no troubleshooting. It
  should *"just work"* &#8482;
* Have a **_consistent_** environment across all developers machines.
* Have a simple command line based workflow: `vagrant up`, `vagrant ssh`,
  `vagrant halt`
* Create **_reusable_** configuration scripts using Puppet that could be used on Test/Staging and Production environments as well. **_(Ambitious)_**

## TL;DR version

#### Advantages

* `vagrant up` _"just works"_ &#8482; ! Excellent for hiding details and
  letting people focus on GTD. This also improves productivity by
  avoiding "it doesn't work on my machine" delays! Because everything
  _"just works"_ &#8482; on the VM.
* Setting up a  [Vagrant base box](http://vagrantup.com/v1/docs/base_boxes.html)
  is not hard. If you setup a minimal base box with a operating system
  (sans GUI) and SSH, you can reuse it on every project and do the provisioning through Puppet/Chef.
* We recommend using a [pre-existing base box](http://vagrantbox.es), installing dependencies
  with a package manager (apt-get, etc.) and then hosting it somewhere
  on your local network for fellow devs to use as a pre-packaged VM.
  This is a quick and easy way to get setup.

#### Disadvantages

* Our biggest roadblocks were with getting Puppet to do our bidding. We
  tried to reuse existing Puppet modules for installing dependencies.
  We managed to get RVM and Postgres installed through Puppet.
  But we just couldn't seem to get Nginx/Passenger to work. 
* Puppet modules tended to be either poorly documented / not
  maintained or just did not work! Maybe we were doing something
  wrong, but it was really hard to tell!
* Base boxes for your choice of operating system might not be readily
  available! (This is not a major disadvantage as it is quite easy to
  create your own base box, but it is time consuming)
  
## Background

We started by watching a short but informative
[presentation](http://crohr.me/presentations/vagrant-puppet/) by Cyril
Rohr about using Vagrant with Puppet. It was enough to convince us to
pursue the magical `vagrant up`!

## How to setup Vagrant

Just follow these simple
[getting started](http://vagrantup.com/v1/docs/getting-started/index.html)
instructions on the Vagrant site. You can try it out using the
`lucid32` base box that the creators of Vagrant have provided. If the
setup was easy enough, you should already be convinced that Vagrant is
a useful tool ;-)

## Customizing the VM for your project

Setting up Vagrant was easy. The more complicated part was
setting up a Virtual machine for use on the project.

There were two strategies that we thought of:

1. Create a fully loaded base box with all the dependencies pre-installed. This base box can be hosted on a URL that can be
  shared with the team and added to the Vagrantfile as well. The first
  time someone does a `vagrant up`, the base box will be downloaded to
  their machine and stored locally.
2. Create or reuse a minimal base box with only the OS and SSH
  installed. Provision the dependencies for your project through
  Puppet/Chef. Ideally reuse existing Puppet modules/Chef recipes.
  

Option 1 is relatively easier and faster for these reasons.

* There are quite a few base boxes that people have already created and
shared on the [Vagrant Boxes site](http://vagrantbox.es). 
* It is straightforward to use a package manager (apt-get, et .al) to
  install whatever you need on the base box
* Once your installation is done, you can _**freeze**_ it on the VM
  and no one else needs to do it. So less troubleshooting, etc. is likely.

Option 2 was more interesting because we wanted to experiment with
Puppet! So thats what we went with. Here is our experiences:

* Puppet uses the concept of Resource Abstraction Layer to abstract
  away OS level details for resources like: Files, Packages, Services,
  Users, Executables and so on.
* Puppet provides a language to specify configuration and one can
  maintain a "manifest" file with per-project requirements.
* Puppet modules are a way to reuse other people's code to avoid the
  nitty-gritty of setting things up. There is a PuppetLabs module
  repository as well as a number of modules available on Github. 
  However, we were not too happy with the documentation and support
  for most modules that we used.
* We ended up using Puppet modules for RVM and Postgresql
  installation. In order to tell Puppet to install RVM, all we needed
  to do was: `include 'rvm'` in our Puppet manifest. The same was true
  for Postgresql. 
* In conclusion, we realized that Puppet modules are nothing but
  collections of OS specific installation instructions for various
  packages and services. It is not too difficult to write your own
  module that delegates to the OS you are using. And that is probably
  a better way to go than rely on some obscure module that might not
  be properly tested/maintained.
  
## Bottomline/Conclusion

Using Vagrant to manage VM's is a great idea. 

However, until I become a Puppet/Chef expert or I there is one on the team, I would go for a fully-loaded base
box option it is less time consuming.

Happy coding.
