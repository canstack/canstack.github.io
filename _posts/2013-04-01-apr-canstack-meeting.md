---
layout: post
title: Wrap up of March 2013 CanStack Meeting
---

On Thursday, March 28th, 2013, nine people called in from across Canada to talk about what's happening with regards to OpenStack in Canada.

## Attendees

* Anita Kuno (Haliburton, ON)
* Curtis Collicutt (Edmonton)
* Barton Satchwill (Edmonton)
* Matthew Delaney (Edmonton)
* Alex Valiushko (Edmonton)
* David Ackerman (Edmonton)
* John Shillingtong (Edmonton)
* Jason van Gaal (Ottawa)
* Jordan Dohms (Edmonton)

## Poorly timed

Unfortunately, I made a mistake in setting up the date for this meeting--I set it on the Thursday of a Friday long weekend. But, we had a poll and decided not to change the time. So this meeting was a bit shorter as we all wanted to get on with our long weekend. Lesson learned! :)

## What we talked about

### Configuration management

Configuration management and OpenStack go hand-in-hand. I imagine each meeting will have a bit of discussion regarding configuration management.

We talked a bit about the usual suspects--chef and puppet--but we also discussed [Salt](http://saltstack.com/), which is a configuration and orchestration system written in Python, and because OpenStack is also mostly written in Python, it might make sense to use Salt stack in specific cases, especially if developers are already working with Python.

### Learning how to contribute code to OpenStack

We talked about how on the Friday previous to the #canstack meeting [Anita](https://twitter.com/anteaya) spent 4.5 hours with a group of us from Cybera going over the procedure and setup of a development environment to contribute to OpenStack. Surprisingly, even with that much time we weren't quite able to submit a patch, mostly because we ran into a swift bug.

We're going to continue this process in the next couple of weeks, and hopefully we'll see some Cybera staff having contributed patches to OpenStack.

### Updating OpenStack releases

One of the bigger topics in discussion was updating between OpenStack releases. 

Basically, no one in the room had ever really upgraded between releases. In most cases the upgrade wasn't really an upgrade so much as a complete reinstall, otherwise known as a "forklift upgrade." So we didn't have any good answers to that issue, and it's something we want to explore in future meeting.

Here are a few links that Anita provided that might help in learning about upgrading from one OpenStack release to another.

* [https://github.com/openstack-dev/grenade](https://github.com/openstack-dev/grenade)
* [http://docs.openstack.org/essex/openstack-compute/install/yum/content/ch_migrating-from-diablo.html](http://docs.openstack.org/essex/openstack-compute/install/yum/content/ch_migrating-from-diablo.html)
*  [http://docs.openstack.org/trunk/openstack-ops/content/maintenance.html#upgrades](http://docs.openstack.org/trunk/openstack-ops/content/maintenance.html#upgrades)

Also, we were all curious as to exactly how Rackspace is staying within a couple weeks of trunk.

At some point OpenStack will have to support upgrades.

### Next meeting

The next meeting will be just after the [Portand OpenStack summit](http://www.openstack.org/summit/portland-2013/), so I'm sure it will be a lively one filled with new information about OpenStack, especially the Grizzly release. 
