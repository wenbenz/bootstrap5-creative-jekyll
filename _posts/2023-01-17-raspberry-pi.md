---
layout: post
title: "Why I love the Raspberry Pi"
date: 2023-01-17 12:00:00 -0500
background: '/assets/img/posts/raspberrypi.jpg'
includeMeta: yes
---
When I bought this little device back in 2020, I never expected to use it as much as I do today. I simply wanted to spin up a real network to learn about network exploits. After some time, it fulfilled its purpose and sat in a drawer for more than a couple years... until a certain megacorporation changed their cloud storage policy making it such that if you have too many photos and videos, your email stops working. This spurred a series of projects which are as useful now as they were educational to build.

## [Photoprism](https://photoprism.app/)

This project started it all. I needed a safe place to put my photos where I don't have to look over my shoulder for storage quotas. With each photo ranging from 2-6MB, and much more for videos, it really doesn't take long before needing to upgrade to more expensive storage plans. I also have a fairly large external hard drive I used for back-ups and there's tons of space there so I might as well put some photos on it.

> **Quick math**: 
> At the time of writing, aforementioned megacorporation wants to charge $13.99/mo = **$167.88/yr** for 2TB of storage.
> An external hard disk of the same capacity costs **$84.99 once**.

Now, it goes without saying that the cloud solution does provide other services out of the box with no additional effort like being able to access all your photos everywhere and the data is automatically backed up. How much those services are worth is up to the individual to decide.

## Hosting my website

Photoprism introduced me into the self-hosting world. Hosting my own photo server gave me a sense of autonomy and independence, and it made me think:

> What else can I self-host?
> I have a website, and it's due for a makeover...
> It's just a static site now, but what if I want to upgrade it later to host dynamic content?
>
> **I should host my website!**

This led me to find [Jekyll](https://jekyllrb.com/) for building the site itself and Photoprism's website mentioned [Caddy](https://caddyserver.com/) which was an interesting candidate for running the actual webserver since it automatically handles TLS/HTTPS. Using these, I now have a beautiful personal landing page on my own domain that is HTTPS secured. I also got a refresher on how the internet is connected and got my hands dirty with dynamic DNS configs (which I'm still not sure is fully working). Discovering Jekyll is also the reason I thought I should write a blog.

## Samba

I'm hosting a photo server locally and I still have a massive amount of storage... why not every other file type? Samba is a SMB server which essentially allows my pi to function as a network access storage (NAS). Now, on top of the already massive storage on my desktop, I have even more storage on a shared drive in my local network!

### It takes two to samba!

On it's own, a NAS is pretty cool, but it also happens to synergize well with Photoprism. I found an app [SMBSync2](https://play.google.com/store/apps/details?id=com.sentaroh.android.SMBSync2&hl=en_CA&gl=US) that allows me to create a task to push recent photos to the imports folder in Photoprism. So my photos are always backed up to my locally hosted server, and the best part: no data required!

## I love pi!

I really didn't expect to go down this rabbit hole of pi projects, but it really has been a great learning experience and produced some useful results. There's likely more pi projects to come.