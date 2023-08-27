---
title: "Ox-Bike: Local-First Vehicle Sharing Software"
seo_title: "Ox-Bike: Local-First Vehicle Sharing Software"
summary: Software to run a local multi-house vehicle sharing co-op, even if the internet goes down.
description:
slug: ox-bike
author: Jade

draft: false
date: 2023-08-27T11:40:00+10:00
lastmod:
expiryDate:
publishDate:

feature_image: crown-shy.webp
feature_image_alt: Cover art from Becky Chambers' novel, "A Prayer for the Crown Shy" by FeiFei Ruan.

project types:
    - Current

techstack:
    - Local-first
    - Resilience
    - Technology
live_url:
source_url: https://github.com/jadehopepunk/oxbike/
---

# OxBike

## About the software

OxBike is a fairly simple software application to track availability and bookings for vehicles in a vehicle sharing scheme. What makes it unique is that it is a local-first app, powered by the excellent [P2Panda Protocol](https://p2panda.org/), which ensures that it each "node" can synchronise data with other nodes. This allows us to run it on a [Raspberry Pi](https://www.raspberrypi.com/) within [Mojo Manor](/projects/mojo-manor), and access it over the local network even without internet. However, as we start to share vehicles with other houses, they can have nodes in their house which synchronise booking requests and acknowledgements as/when they have connection.

The first users of OxBike will be the [Mojo Transport Collective](/projects/mojo-transport).

## My involvement

At the moment I'm the sole developer on this, and I'm finding it to be a pleasant technical project to tinker with after hours. The bulk of the heavy lifting to achieve the local-first effect is of course powered by the open source libraries and applications that make up P2Panda. P2Panda is new (incomplete), and I'm following along closely with it's development as part of this project.

## Theory of Change

### 1. Prefigurative technology

When it comes to technology choices, the personal is political. It somewhat feels like the battle between "open source" and "closed source" technology has moved on, because open source software has been comfortably embraced by capitalist business models. What really matters is that we use technology with represents the futures we want to try living. In this case, that means small, local software that invites tinkering and shaping to local collective processes. The selection of P2Panda as a protocol is not just because of it's local-first nature, but also because of it's strong focus on inviting and fun user documentation, and I want OxBike to be similarly welcoming.

### 2. Resilience

In a climate crisis future, I have genuine worries about the reliance on centralised infrastructure. By building software that runs on local tech, is built and administered by skilled local people, and can survive brown-outs and internet failures, we start to develop systems that can provide a resilient local future. If OxBike proves useful, I imagine building many other systems to meet local needs using similar technology, and teaching others to do so.