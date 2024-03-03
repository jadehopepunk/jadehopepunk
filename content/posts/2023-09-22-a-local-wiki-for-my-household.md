---
title: A Local Wiki for my Household
summary: I've built a local web-server on a Raspberry Pi, that runs the wiki software that my household can use to document anything we like. You can setup your own Pi the same way using my Git repository.
slug: local-wiki
author: Jade

draft: false
date: 2023-09-22T12:00:00+10:00
lastmod: 2023-09-22T12:00:00+10:00
expiryDate:
publishDate: 2023-09-22T12:00:00+10:00

feature_image:
feature_image_alt:

categories:
  - LocalFirst
tags:
  - Radish House
  - RedBug

toc: false
related: false
social_share: true
newsletter: false
disable_comments: false
---

# Our Needs

Radish House (formerly Mojo Manor) is a co-living household with four residents. As well as talking in person around the kitchen table, we use written communication in a number of ways:

* A signal chat that usually contains time sensitive messages like "can you pick up some bread"
* Some additional signal chats to include common visitors, or discuss special topics like the garden roster
* Some house meeting notes appended to a shared google doc
* A google spreadsheet of our finances
* Todo list on the physical whiteboard in the kitchen
* Some shared values on post-it notes on the pantry door

We're slowly starting to do a more explicit job of deciding on some of our values and future direction, both in house-meetings and discussions on Signal. These things should really be pulled out and written down somewhere, or they become lost in the flow of conversation and we risk going round and round in circles.

The obvious place is yes another google doc, or if we want to structure our thoughts across multiple pages, I admit that I really like Notion.

# The Medium is the Message

At Radish House, we're starting to talk about future plans. We want to collectivise resources more, be more intentional about our relationships, and do more to tackle the ecological and social challenges of our time.

We've discussed making big changes, like moving into our perfect co-living house, but what's resonating with us more right now is trying [small and slow solutions](https://permacultureprinciples.com/permaculture-principles/_9/) that help us improve where we are now, allow us to get better at relating intentionally, and help us [prefigure](https://commonslibrary.org/prefigurative-politics-in-practice/) the future we want to live in.

The technologies we use to communicate and store our knowledge are no different. There's no such thing as a technology choice that is apolitical. If we choose to use Notion, or google docs, then we're buying in to centralisation, surveillance capitalism, and the [enshitification](https://pluralistic.net/2023/01/21/potemkin-ai/) of the internet.

# #LocalFirst

There's a growing trend around [#LocalFirst](https://martin.kleppmann.com/papers/local-first.pdf) software. This tends to mean that software lives first and foremost on the machine you're using it on (your laptop, phone, etc), and has network collaboration and backup capabilities as an add-on, not the other way around.

That feels more resilient, which is important to me in an era of growing climate crisis. However, the way it's expressed can feel very individualistic. I don't want self-sovereign data, I want data that is contextualised and embedded in the community and place in which it is developed and used.

For us at Radish House, that means that the "local" in "local first" isn't the individual, it's the house. This means I want to store our house knowledge in a way that:

* Works for those in the house even if centralised services (the internet) go down
* Is controlled by the house, and tinkerable and customizable to our needs
* Works to share information with guests to the house
* Lessens the extent to which negative externalities are shifted elsewhere

An obvious solution was to store our knowledge on a server on our local wifi network in the house. When we start to think about multi-user web software, we don't need fancy "local first" systems like [Anytype](https://anytype.io/) or [AppFlowy](https://appflowy.io/). In fact there's several decades of nice little PHP web apps to choose from.

In the end, we went went with [Dokuwiki](https://www.dokuwiki.org/dokuwiki). It's not everything I think we might need, but it's simple enough to get us started and better learn what our needs are. We're running it on a Raspberry Pi, on the local network. So for us, it's just at `radish.local/wiki`.

# Infrastructure as Code

So now the house is reliant on a Raspberry Pi. That's easy and fun to setup. But, I'm looking for patterns that I can share with the other co-living houses in my networks, and I'm also aware that I'm going to want multiple apps on this, our needs are going to change over time, and eventually it's going to become a complex mess I'll have to throw away and start again.

That means we need our infrastructure to be code, so we can make repeatable changes, and rebuild this machine as often as we need.

## Ansible

I'm a software engineer, not an infrastructure expert, so it took some hunting around to find the infrastructure platform that was the right mix of simplicity and power, and common enough that it was worth recommending others around me use too.

I've gone with [Ansible](https://www.ansible.com/), an open source infrastructure tool from Red Hat. My ansible scripts are also open source, and others can form them for their needs.

## Try it Out

Here is my ansible project for setting up a Raspberry Pi to run Dokuwiki, as well as proxy to let it run multiple apps at sub-directories (since you can't use subdomains on local WiFi without setting up DNS).

[redbugcollective/household-pi-setup](https://github.com/redbugcollective/household-pi-setup)

I'm going to keep working on this, and add the other apps that Radish House needs, so if you only want Dokuwiki, for it or use it as a reference.

## Backup

The final thing I needed before letting my housemates loose on this was some sort of backup solution. #LocalFirst does not mean no recovery if the device is ruined. I'd love to do cool things with backups, like backing up to the Pi's of other houses in my local network, or backing up to a [municipal web hosting collective](/projects/merri-bek-hosting/), but I don't have any of those thing and I want to get started and get learning.

So, I'm renting a Digital Ocean droplet and rsyncing backups there. It's an easy way to get started, but I hope to revisit that soon.

Plus, no sense in getting too fancy. Let's see if my housemates use this first...