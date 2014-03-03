---
layout: post
title: Wrap up of Feb 2013 CanStack Meeting
---

On Thursday, February 28th, 2013, ten people called in from across Canada--and the world actually as we had one caller log in from Bangalore--to talk about what's happening with regards to OpenStack in Canada.

## Attendees

* Sandy Walsh (Halifax)
* Anita Kuno (Haliburton, ON)
* Jacob Godin (Halifax)
* Neil Jubinville (Edmonton)
* Wendy Simard (Edmonton)
* Curtis Collicutt (Edmonton)
* Matthew Delaney (Edmonton)
* David Ackerman (Edmonton)
* Luke Tymowski (Calgary)
* Kurin Murari (Bangalore, India)

## What we talked about

### Hardware

We talked a little about hardware, mostly Dell-based. Cybera predominantly uses the C6220 and it's previous generation. Others are using the Dell R410, 420 type systems. 

Luke mentioned that if you decide to use the C6620 make sure to have a spare chassis for testing when something goes wrong and you have to troubleshoot with Dell technicians.

### Rackspace automation

Sandy gave us a bit of an idea as to how Rackspace runs their infrastructure.

They have invested heavily in automation and testing. They run a week or two behind OpenStack's trunk *in production*, and can do so because of the automation. A lot of what they do is run out of [Jenkins](http://jenkins-ci.org/) and they prefer to make one or two changes at a time, but often, rather than many changes less often.

### Stacktach and Ceilometer

Sandy is also a developer on [Stacktach](https://github.com/rackspace/stacktach which is a monitoring/)metering system for OpenStack. Stacktach can help organizations to do billing and other analysis. For example Cybera is using Stacktack to [report Microsoft license usage in OpenStack](https://lists.launchpad.net/openstack/msg20884.html).

Sandy mentioned that Rackspace will be folding Stacktach into the newish [Ceilometer](https://wiki.openstack.org/wiki/Ceilometer) project.

### Puppet, Chef, JClouds, Ansible, Juju, Crowbar, etc

We also had a bit of a discussion about the various automation (ie. devops) systems out there, and cloud frameworks like [JClouds](http://www.jclouds.org/documentation/gettingstarted/what-is-jclouds/). 

I think the general agreement was use whatever you want, just start using it now!

### Over committing in OpenStack

Neil was also interested in have some kind of "hackday" regarding over committing in OpenStack. He wants to be able to see how far he can push OpenStack and the hardware it's running on so that once a cloud is launched they have a better idea of what it's capable of doing, rather than staying conservative with resource allocation. Because once you launch, it's hard to know.

I have done a bit of work around [over committing with KVM](http://serverascode.com/2013/02/20/overcommitting-with-kvm.html), so of course that interests me. :)

We'll see if we can fit in a hackday sometime in the future.

### What we decided about meetings

* We would like to have monthly meetings, though we will probably not have meetings in July, August, and December, so we'll have 7 more meetings this calendar year.
* At the next meeting we would like to talk about some of the new things that have changed in OpenStack since our last meeting in June of 2012 (which was a long time ago), and considering the rate of development in OpenStack, a lot has changed. There was a lot of interest in how OpenStack operators are using and troubleshooting Quantum, ie. software defined networking.
* Hopefully at the next meeting we'll also be able to bring in some of the people that are [writing an OpenStack operators manual in five days](http://www.openstack.org/blog/2013/02/bring-on-the-crazy-zero-to-book-in-five-days/)
* Everyone seemed to like the Bluejeans video/voice conference system, so that's a good sign for future meetings.

### Todo

* Anita suggested we set up an IRC channel. I'll be looking into this soon.
* Setup a poll with a possible monthly date, eg. the 3rd Thursday, or 2nd Tuesday kind of thing, and set the time and date for the March meeting.

As always, if you have suggestions, comments, criticisms or corrections, please let me know in the comments or by tweeting [@canstack](http://twitter.com/canstack) and I will make sure to update this post.

