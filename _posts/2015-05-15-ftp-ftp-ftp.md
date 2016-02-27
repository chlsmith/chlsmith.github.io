---
layout: post
title: FTP FTP FTP
date: 2015-05-15 22:52


categories: [Uncategorized]
---
I had no idea we were so dependent upon FTP anymore.   I'm running 3 FTP servers: one for production use, one for our staging, and one for our devs to have a way to upload/download to our Azure environment without having to go to blob storage.   That's all fine and good, but each of these runs multiple protocols (ftps, ftp, etc.) on different ports, for different user accounts.

This week I had 2 of them poop out on me.   The first was the one for the devs to use for what I call "transient files".   They upload there and use them throughout the environment off of a file share on the same directory.   Darn thing quit working, so I had to fix it, and in the process, I went ahead and enabled AD integration to make it right.

Then the second outage came along.   This was more nefarious and was the production server, which our dealers all use to get updates to our software.   Something happened and it just went kaput.   The SSL cert on it expired a month before, so I don't know how we didn't hear of it then, but things must have continued to work until last night, when something happened to kill the whole thing.   Working with the devs at CrushFTP (the makers of our FTP server app), we were able to get the server at least up again with the expired cert.   The problem remains, though, that I don't have the PFX file for the new cert, or the password for it.  Our users still are probably erroring out because of the expired cert, but at least FTP is running.

In between, there was a 3rd issue with the staging server, but that turned out to just be a miscommunication from folks.  I haven't messed with FTP for several years until the last couple of weeks.   I hope it works for good once I get the new SSL cert on the production site.
