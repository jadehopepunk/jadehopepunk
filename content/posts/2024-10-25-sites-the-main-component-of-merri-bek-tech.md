---
title: "Sites: The main component of Merri-bek Tech"
summary: We're slowly learning how to build resilient local hosting, through collaboration across a range of backgrounds. Deciding on docker swarm as a key layer of the setup helps create a clear bridge between Sites and Applications, and is part of us firming up the idea of what a Site is.
author: Jade

draft: false
date: 2024-10-25T1:00:00+10:00
lastmod: 2024-10-25T12:00:00+10:00

feature_image:
feature_image_alt:

categories:
  - LocalFirst
tags:
  - Merri-bek

toc: false
related: false
social_share: true
newsletter: false
disable_comments: false
---

Merri-bek Tech has been making progress, trying to figure out how to provide low carbon web hosting for the local community that is useful both on normal days, and on days when power or internet is interrupted. Our 3 year mission is to provide useful information services at 3 sites in Merri-bek that remain in communication with each other during a 3 day power outage.

So what is a site? This [hypothetical news article from 2029](/posts/merri-bek-tech-in-2029) indicates that our services should be available at community facilities, like libraries and neighbourhood houses. That means there's an bunch of computer infrastructure at those locations, which we call a "**Site**".

We don't know how many sites should exist, but the current guess is something like 5-10 across Merri-bek.

## The physical makeup of a Site

### Computing

After initially exploring second-hand rack-mount servers, Merri-bek Tech is going all in on the [Raspberry Pi](/posts/merri-bek-tech-in-2029) because it's such an accessible and learnable small computer, and can act as a module in a larger system. We've been running a successful volunteer cohort at [Sussex Neighbourhood House](https://sussexnh.org.au/) where volunteers have learned to install and operate linux on a Raspberry Pi, and that creates a great pathway to managing larger systems.

So, while the smallest amount of compute resources at a site is probably a single Raspberry Pi, a small practical site that allows us to practice operating a group of Raspberry Pi computers might consist of 3 Pis.

### Power

A Raspberry Pi 5 requires 25W of power (5V x 5A), although it can get by on a little less. We envisage powering a site largely using low voltage DC wiring, making it safe to tinker with. It's our eventual goal to have each site powered entirely by renewable energy, and to have enough power storage for at least a three day outage, but to get started we just need surge protection and a power supply.

### Storage

Each Pi runs it's operating system off an SD Card, and uses that as a mini hard disk. However, some of our operations will need a larger disk. For example, and early goal is to serve a copy of Wikipedia, which is about 130GB for just English.

### Networking

The site needs a network switch, with a port for each Pi. The more Pis, the more ports needed. In addition to that, it needs to plug into the internet access of the building (or connect via wifi). Redundant options (an included wifi router and/or 4/5G modem) are being considered. As soon as we have two sites live, we plan to start testing communication technologies such as LoRa.

### Putting it all together

A site based on three Pis isn't very large, and probably fits in a shoebox. Adding a battery supply makes it bigger. We'll develop some options for form factors that won't be unwelcome in community facilities.

## The people who setup and run a Site

At Merri-bek Tech our model is something of a hybrid of central organisation with decentralisation. We want to be more solarpunk than corporate, and have room for people to tinker and manage stuff themselves, but we also want to be able to run a web service for say, the local bowls club, and provide them with some confidence that their website won't be defaced and their membership register not looked at.

All this means we want to encourage small groups to manage parts of the infrastructure, but on behalf of the broader community and with some responsibilities. We call this process "**Stewardship**" rather than management or ownership.

### Site stewards

Each site has a steward or stewards. These stewards are responsible for keeping the site up and running, as a platform for applications to run on. That might include swapping out failed hardware, dealing with power interruptions, etc.

### Application stewards

Each application we support, whether it's providing a Wikipedia mirror or email, is running of multiple sites (usually all sites) in Merri-bek. Applications have technical requirements, but also sometimes social ones. For example, running social networking software might require content moderation.

Merri-bek Tech is not going to run any application unless we have a small group of at least 2 volunteer stewards, who will look after the application's needs across all Merri-bek sites.

### Working together

To work together, Site Stewards and Application Stewards need a clear point of interface.

## The Software that runs Applications at a Site

### Docker

Containerisation is a common approach to bundling up an app, and everything that it needs to run, in a way that can be run independently of the details of the platform that it's running on (mostly). [Docker](https://www.docker.com/) is the most common containerisation technology, and is heavily used from hobby projects right through to large enterprises.

### Docker swarm

As we start to run applications that consist of multiple services, possibly running across more than one Raspberry Pi, we're going to want a way to orchestrate docker containers across multiple machines. There are two main options for this, Kubernetes and Docker Swarm. Kubernetes was developed by Google to run billions of containers, and is the standard approach in large industry. Many people find, however, that it's just too confusing and hard to learn for smaller projects.

[Docker Swarm](https://docs.docker.com/engine/swarm/) is right sized for us. It allows our Raspberry Pis to all be treated as one swarm offering a generalised ability to run services. You can run a service across any number of nodes (the Pis). It handles joining new Pis into the swarm, having the drop out due to failure, and so on.

While no tech choice is perfect, our current approach is to decide on Docker Swarm as our interface layer between Site and Application, and move on from there.

### Adding and removing nodes

If you were a site steward setting up a new site, you'd want easy step-by-step ways of adding a new Raspberry Pi into the swarm. There's a secret swarm token that needs to be put on the new Pi in order to connect it. We're going to start by doing this process very manually, with great documentation, but it's an important goal for us to make the process really simple for a range of skill levels, with good observability about what's going on.

### Swarm observability

There are several software platforms that provide a user interface allowing you to see, and perhaps control, what is happening with your docker swarm and what services are running on it. The biggest open source player is [Portainer](https://www.portainer.io/), with a self-installable community edition, and a more fully featured commercial offering.

We don't want to be too tied to an observability interface at this stage. We're strongly decided on Docker Swarm, but only weakly deciding on an approach to observability and we may change our mind later. For now though, the plan is to trial [Swarmpit](https://swarmpit.io/), which is an open source UI designed entirely for Docker Swarm. That makes it a little simpler than Portainer (which also handles Kubernetes).

There are some downsides to this approach (Swarmpit has not had much development activity for the last few years) and we may revisit it later.