---
layout: post
title: Photoprism
subtitle: Self-Hosted Google Photos alternative
date: 2023-01-25 12:00:00 -0500
background: '/assets/img/posts/photoprism.jpg'
includeMeta: yes
---
I have been a long-time user of Google Photos, but the moment I found out that photos would be subject to the Google Drive storage limits, it was time to find an alternative. Google drive has always had a 15GB storage limit in their free tier, but it wasn't until recently that files in Google Photos would count towards that limit. When that limit is reached, other services that require storage would stop working--this includes Gmail. I personally find that this shared quota effectively renders Google Photos unusable; the fact that automatic backups to Google Photos could disable emails is unacceptable. I needed a new solution: **Photoprism**.

**Why not just buy more storage?**

Obviously, I could have paid for more storage, but each image with a modern smartphone camera occupies 1-6MB of storage and videos can easily extend into the 100sMB. Also, as my library grows, the monthly cost for storage increase and it would become increasingly difficult to migrate away in the future. But most importantly: **I'm cheap**.

> At the time of writing, the maximum Google One plan is $13.99/mo = **$167.88/yr** for 2TB of storage.
> An external hard disk of the same capacity costs **$84.99 once**.

# Ingredients
Here's what you will need to set it up at home:
- A 64-bit computer that can run 24/7 with networking capabilities; I used my Raspberry Pi 4 running Raspberry Pi OS Lite because it consumes much less power than a PC.
    - Official system requirements for Photoprism [here](https://docs.photoprism.app/getting-started/#system-requirements).
- Enough storage for all your photos and videos; I used a 3TB external hard drive that I had lying around.

# Directions
These directions may look long but that's only because I added all the code snippets so that it'll be mostly copy-paste. These directions assume you're doing a raspberry pi setup, but it should be similar for any OS because we're running the server in Docker.
- Install Docker
```
curl -sSL https://get.docker.com | sh
sudo usermod -aG docker <username>
```
- If storing photos in an external drive, remember to mount the drive.
    - Create a directory to mount the device to
```
mkdir /media/ext_hdd
```
    - List devices with `sudo fdisk -l` and the output should contain look something like this
```
Device         Start       End   Sectors   Size Type
/dev/sda1      65535 488366819 488301285   1.8T unknown
/dev/sda2  488366820 732550229 244183410 931.5G Microsoft basic data
```
    - My hard drive has 2 partitions; one encrypted linux partition that is ~2TB and one windows partion ~1TB. I can see that my hard drive is `/dev/sda` and the partitions are `sda1` and `sda2`
```
sudo mount /dev/sda1 /media/ext_hdd
```
    - If your partition is LUKS encrypted like mine (you'd know if it is), then you'll have [extra steps](https://askubuntu.com/questions/63594/mount-encrypted-volumes-from-command-line) to decrypt it
```
sudo apt install cryptsetup
sudo cryptsetup luksOpen /dev/sda1 sda1_decrypted
sudo mount /dev/mapper/sda1_decrypted /media/ext_hdd
```
- Make a directory where you want to save the server files to. I saved mine to `~/photoprism`
```
mkdir ~/photoprism
cd ~/photoprism
```
- Download the docker-compose file from [photoprism](https://docs.photoprism.app/getting-started/docker-compose/). The one for Raspberry Pi is attached below.
```
wget https://dl.photoprism.app/docker/arm64/docker-compose.yml
```
- Configure the server by opening `docker-compose.yml` in your favourite text editor. Here we'll use `vim`.
```
vim docker-compose.yml
```
    - The main things you'll want to configure are `volumes`, and `PHOTOPRISM_ADMIN_PASSWORD`.
    - Hint: each item under volumes tells Docker how to mount the folders inside the Docker container. The path left of `:` is the directory in your local machine, and the path on the right is the directory inside the docker container. So if your photos are stored in a directory called `Pictures` in your external hard drive mounted to `/media/ext_hdd`, then volumes should contain `"/media/ext_hdd/Pictures:/photoprism/originals"`.
- Start the server
```
docker compose up -d
```
- Now the server should be running on `http://localhost:2342/`. Login with user `admin` and the password you configured in `PHOTOPRISM_ADMIN_PASSWORD`. Navigate to Library > Index and index your files so they show up in the UI!