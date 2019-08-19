---
layout: post
subtitle: "Use docker for simple flask app"
tags: [cs, docker, python]
comments: true
bigimg: /img/docker/docker1.jpg
---
>Disclaimer: I'm only beginner in docker and the tech behind it.  
This post is only sharing
my practice when I transform my "packaging products" from 
traditional method to using container and docker.

When I started writing code and package my products, the process is quite complicated.
You need to setup your production environment with proper dependencies and configuration, 
and with different virtual machine, you might need different setup and it's not very flexible.

Then I know about container and docker.

From the docs, container is a *standard unit of software that packages up code and all its dependencies*
which means all the code, configuration, dependencies and so on of my app will be packaged in a *container*
and when I want to deploy my app, I deploy that *container* without worrying about the environment of the hosts.

### Get Started
---

Make sure you are install Docker, the guideline is available in docker page.

```bash
$ docker --version
Docker version 19.03.1, build 74b1e89
```

Create new directory to build our app, in my case I call it `flasker` a flask app using docker for packaging.
```bash
$ mkdir flasker && cd flasker
```

The docker container in my mind is like a box, that contain all necessary things for my app
and to tell which is necessary we need a `Dockerfile`
```bash
$ touch Dockerfile
```

**_Updating..._**

