---
layout: post
title: "Docker: Getting to the container quickly"
date: 2017-09-30
---

Small barriers can really kill productivity. Recently I've been dealing with
this a lot in Docker. Sometimes it's that my `Dockerfile` isn't building,
sometimes it's that the running container isn't behaving how I was expecting,
but every time I find myself needing to lookup the commands I need to start
debugging.

This week I finally got sick of it and added a couple commands to my `.bashrc`
to make my life better.

## Insta ##
<script src="https://gist.github.com/kjschiroo/deed3f9352d3f46307a2921fa347ab9f.js"></script>
`insta <image_name>` spins up a container and drops you into the shell. This
is handy both when your `Dockerfile` isn't building and when you just need to
get a quick instance of an image to see what the behavior is in it.

## Dock ##
<script src="https://gist.github.com/kjschiroo/869cde4589ab6c037c13842e65fa7e69.js"></script>
When your container is misbehaving sometimes you just have to take a look
inside. That is what `dock <container_name>` gives you. If using `docker-compose`
the container names are predictably `<proj_dir>_<service>_<number>`.
