---
layout: post
title: Virtual computing lab OpenStack reference architecture
---
*Posted by [curtis](http://serverascode.com)*

*****


One of the projects that I work on at [Cybera](http://cybera.ca) is a [virtual computing lab](http://www.cybera.ca/projects/virtual-computing-lab). This project uses [Apache VCL](https://cwiki.apache.org/VCL/) backed by [OpenStack](http://openstack.org) to provide users the ability to use, and reserve, virtual machines to use for their classes. Typically this means making a reservation through VCL and being able to login to a remote Windows instance to access software they otherwise might only be able to use in a physical computing lab.

Technically OpenStack isn't 100% supported by Apache VCL right now, so we have some custom modifications in place that allow us to use OpenStack Essex as the virtual machine back-end, but I believe OpenStack support is on the road map.

## tl;dr

For a reference, here is what we are using to provide OpenStack to our Apache VCL system.

- OpenStack version: [Essex](http://www.openstack.org/software/essex/)
- OpenStack components used: nova-compute, nova-volume (ie. no swift)
- OpenStack networking: VLAN Manager
- Number of compute nodes: 7
- Number of cloud controllers: 1
- Servers: 2x [Dell C6220](http://www.dell.com/us/enterprise/p/poweredge-c6220/pd) chassis with 4 nodes in each 2U chassis, for a total of 8 "servers." Each node has 2x 10G SFP network ports, 2x 1G ports, and a 1G managment/IPMI port
- Storage: Each node has, for now, 6x 1TB SATA drives. 
- 1x Arista 10G switch
- 1x Cisco 1G management switch (for IPMI)
- Operating system: Ubuntu 12.04 / Precise
- Configuration management: [Ansible](http://ansible.cc)
- Baremetal deployment: PXE boot
- Datacenter host: [Blackbridge](http://www.blackbridge.com)

## Our architecture for the virtual computing lab

As noted above, we are running OpenStack Essex. This is because it was the latest release available when we started the project. We are running OpenStack off of Ubuntu 12.04 and using the standard OpenStack packages. I haven't run into any bugs yet, though because of an issue with our Windows images I set the DHCP timeout to 28800 instead of the default one minute, and we have configured OpenStack to use virtio on the bridges to get full use of our bonded 10G networking. Otherwise the virtual machines will be limited to 100M by default.

OpenStack is configured using the [Ansible](http://ansible.cc configuration managment) system. Currently our Apache VCL instance is configured with [Chef](http://wiki.opscode.com/display/chef/Home), though it was previously configured via Ansible.

I like Ansible because it is straightforward, only requires a couple of python packages to run (paramiko and jinja2 templates), and uses ssh to access the servers. I wrote a [blog post](http://www.cybera.ca/tech-radar/first-look-ansible) on Ansible a while back for Cybera so I won't get into it too much here. Eventually I will probably be forced to use Chef or Puppet, but for now I'm quite happy with Ansible. :)

As far as networking, each node has 2x 10G SFP ports connected to a single 24 port [Arista](http://www.aristanetworks.com/) switch. Also the IPMI interface is connected to an older, slower switch. The 10G nics are bonded in the OS and we have two virtual VLAN interfaces that have their raw device set as the bonded interface. In some of our other clouds we have two switches for high availability, but right now, for this project, we just have the one switch. Though with the two bonded connections we can easily add a new switch in the future. 

If you haven't heard of Arista before, now is a good time to look into what they are doing. Each switch runs on a [stock Linux kernel](http://en.wikipedia.org/wiki/Arista_Networks#Extensible_Operating_System), so you can run Linux applications on the switch if you want. Very interesting hardware and software. In the future I'll try to share more about how the switches are actually configured.

Our datacenter host is [Blackbridge](http://www.blackbridge.com/). They are located near [Lethbridge, Alberta, Canada](http://blackbridgenetworks.com/location.html), which is about 600Km from my workplace on the [UofA](http://ualberta.ca Campus). I've never actually seen the servers! Blackbridge has been great to work with, even going so far as to take some pictures of our rack so that I could put them up on the CanStack website.

## Stateless virtual machines, over-committing and solid state drives

As mentioned, right now the servers have 6x 1TB SATA drives. Our VCL project is interesting because the virtual machines are stateless. What I mean by that is if the virtual machine goes down for some reason--eg. hardware failure on a compute node--there will be no user data lost. Certainly if a user is accessing a virtual machine they will have to create a new reservation, but they don't store their data on the actual instance, so they can't lose data (assuming they save locally every once in a while)--all they have to do is make a new reservation and keep working.

The six SATA drives are configured in software-based RAID10. They are only really capable of about 400 IOPS. This is not very much, especially when working with IOPS hungry Windows instances. Each Windows instance uses about four or five IOPS even when "idle" so it doesn't take very many instances to eat up all the available IOPS.

In the next couple of months we are going to roll out solid state drives to each of the compute nodes. Given that VCL is stateless, I have been doing some [testing](http://www.cybera.ca/tech-radar/performance-testing-solid-state-drives) with striped/RAID0 configurations and when even the slowest of solid state drives can do 25k IOPS it doesn't take many to achieve tens of thousands of IOPS. 

In my experiments I've found we can benefit from at least 5k IOPS to support Windows bootstorms and such, so with 10x or 100x more IOPS we should see much improved Windows performance in VCL. Having more IOPS will also mean we can over-commit with KVM, because the reality is that over-committing is, in my opinion, mostly IOPS-bound. If we can over-commit we can run more virtual machines and provide access to more classes and students with a lower capital cost.

## Questions

I can't think of anything else important to mention, but if you have questions please feel free to ask them in the comments and I'll be sure to respond.