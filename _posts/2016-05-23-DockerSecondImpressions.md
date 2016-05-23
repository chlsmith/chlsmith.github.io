---
layout: post
title: Docker Second Impressions
categories: [linux,docker]
published: true
---

Not too shabby.  I now have my first ever docker image all working and have it uploaded to Docker Hub for safe keeping and reuse down the road.   I have a Dockerfile that pulls down the latest image and then gets it ready to run, and a simple command to run the thing.   My app connects to an Azure SQL database, so there's nothing else needed to make the thing run.

Going forward, maintaining this app is just a matter of updating the current image with new stuff, just as it would've been if I was doing things on non-containerized systems.   Is this better?   Maybe, maybe not.  Docker does add a layer that I probably don't need, BUT for disaster recovery, man, this is pretty sweet.   I have a single command to spin up a whole application on really any Docker host I want.  That's pretty damned cool, and I won't have a single thing to worry about in terms of rework within the app.   

Was it worth it?   I think so.