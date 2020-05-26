---
title: "Getting Started"
date: 2020-03-31T12:50:55-04:00
weight: 1
---
# Getting Started
This section gets you started with Paketo Buildpacks using Paketo **Builders**, the **Pack** CLI, and **Docker**.

## Paketo Builders
Builders are an image that consist of buildpacks and a stack image. Learn more [here](https://buildpacks.io/docs/concepts/components/builder/). The Paketo Buildpacks project releases several builder images. These are:

**Tiny** - Builder based off of a Distroless `ubuntu:bionic` stack. Ideal for most Go apps.  
`gcr.io/paketo-buildpacks/builder:tiny`

**Base** - Builder based off of the `ubuntu:bionic` stack ideal for most Java, Node.js, Go, .NET Core, and NGINX apps **without** common C libraries.  
`gcr.io/paketo-buildpacks/builder:base`

**Full** - Builder based off of the `ubuntu:bionic` stack ideal for most PHP, Java, Node.js, Go, .NET Core, and NGINX apps **with** common C libraries.  
`gcr.io/paketo-buildpacks/builder:full-cf`


## Quick Start Guide 
Let's use the `base` Paketo Builder and the **Pack** CLI to build a Node.js app as a runnable container image. App source code is available [here](https://github.com/paketo-buildpacks/samples/tree/master/demo-apps/app-source).

**Prerequisites** - Install Pack and Docker  
Follow [these instructions](https://buildpacks.io/docs/install-pack/) to get all set up.

And we're good to go! Let's build our app into a container image using the `pack build` command.
```
$ pack build paketo-demo-app -p <path/to/source> --builder gcr.io/paketo-buildpacks/builder:base
......................
===> CREATING
[creator] ---> DETECTING
[creator] paketo-buildpacks/node-engine 0.0.178
[creator] paketo-buildpacks/npm         0.1.11
[creator] ---> ANALYZING
[creator] Skipping buildpack layer analysis
[creator] ---> BUILDING
[creator] Node Engine Buildpack 0.0.178
[creator]   Resolving Node Engine version
[creator]     Candidate version sources (in priority order):
[creator]       package.json -> "~10"
[creator]
[creator]     Selected Node Engine version (using package.json): 10.19.0
......................
[creator] Adding cache layer 'paketo-buildpacks/node-engine:node'
[creator] Adding cache layer 'paketo-buildpacks/npm:npm-cache'
Successfully built image paketo-demo-app
```

We've successfully created an image called **paketo-demo-app**. Now let's run our app image and validate that everything is working.
```
$ docker run -p 8080:8080 -e PORT=8080 -d -it paketo-demo-app
02ee8dede7691c8b4addc161c151ea411b5a867141fbb28ceaaf32e749eeae60

$ curl localhost:8080/greeting
Hello from your application image
```

Awesome! Our app is now running on `localhost:8080`.

Keep reading to learn about what the Buildpack API and Paketo Buildpacks are doing under the hood to make it easy to build your apps.







