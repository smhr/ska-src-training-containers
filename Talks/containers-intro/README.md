# Introduction to containers

In this section we provide a very short introduction to the general ideas behind containers. We briefly discuss the situations when containers can be a good choice for your problem and when other solutions might be more fitting.

## 1. What are containers

You may hear people say they are "running an image" or "running a container". These terms are often used interchangeably.

The most important feature of containers, and where their real strength comes from, is that unlike "regular" applications, they can and often do perform all their work in isolation. Your containers do not have to know what the rest of your OS is up to. They don't even have to have access to the same files as your host OS, or share the same network  (again it is possible to achieve that).

## 2. What containers are not

You will often hear the expression that "containers are like VMs", or "like VMs, but lighter". This may make sense on the surface: there are fewer moving components in the case of containers and the end result might be the same for the end user.

Containers remove a lot of components of virtual machines though: they do not virtualise the hardware, they do not have to contain a fully-fledged guest OS to operate. They have to rely on the host OS instead.

For a more in-depth explanation of the differences between VMs and containers, please [**see this website by the IBM Cloud Team** (https://www.ibm.com/cloud/blog/containers-vs-vms)

## 3. Why do you (and don't) need containers

* Containers will provide a reproducible work environment.
* They go beyond just sharing your code: you provide a fully-working software
with all its required dependencies (modules, libraries, etc.).
* You can build self-contained images that meet the particular needs of your
  project. No need to install software "just in case", or install something to
  be used just once.
* You are no longer tied to the software and library versions installed on your host system.
  Need python3, but only python2 is available? There is an image for that.

&nbsp;

* Your software still depends on hardware you run it on - make sure your results are consistent across different hardware architectures.
* Not the best for sharing large amounts of data (same as you wouldn't use git to share a 10GB file).
* Additional safety concerns, as e.g. Docker gives extra power to the user "out of the box". There is potential to do some damage to the host OS by an inexperienced or malicious user if your containerisation technology of choice is not configured or used properly.
