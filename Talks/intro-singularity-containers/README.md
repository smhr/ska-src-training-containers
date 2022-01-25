## Objectives and scope

In this tutorial we will work with a containerization system called Singularity, which has many features that make it interesting for workflow development and long-term reproducibility.

**Overall steps:**

What is singularity and what advantages does it have over Docker.
Preparing the work environment
Simple use of Singularity
Create our first container
Share your work!

## What is singularity and what advantages does it have over Docker.

Singularity is a container platform. It allows you to create and run containers that package up pieces of software in a way that is portable and reproducible. You can build a container using Singularity on your laptop, and then run it on many of the largest HPC clusters in the world, local university or company clusters, a single server, in the cloud, or on a workstation down the hall. Your container is a single file, and you don’t have to worry about how to install all the software you need on each different operating system.



**Advantages:**

- Easy to learn and use (relatively speaking)
- Approved for HPC (installed on some of the biggest HPC systems in the world)
- Can convert Docker containers to Singularity and run containers directly from Docker Hub
- SingularityHub!


**Disadvantages:**

- Less mature than Docker
- Smaller user community
- Under very active development 

Singularity is focused for scientific software running in an HPC environent. 

### Aims

- Mobility of Compute
- Reproducibility
- User Freedom
- Support on Existing Traditional HPC

### The Singularity container image

Singularity makes use of a container image file, which physically includes the container. 

#### Supported container formats

- `squashfs`: the default container format is a compressed read-only file system that is widely used for things like live CDs/USBs and cell phone OS’s
- `ext3`: (also called writable) a writable image file containing an ext3 file system that was the default container format prior to Singularity version 2.4
- `directory`: (also called sandbox) standard Unix directory containing a root container image
- `tar.gz`: zlib compressed tar archive
- `tar.bz2`: bzip2 compressed tar archive
- `tar`: uncompressed tar archive


#### Supported Unified Resource Identifiers (URIs)

Singularity also supports several different mechanisms for obtaining the images using a standard URI format.

- `shub://` Singularity Hub is the registry for Singularity containers like DockerHub.
- `docker://` Singularity can pull Docker images from a Docker registry.
- `instance://` A Singularity container running as service, called an instance, can be referenced with this URI.


#### Copying, sharing, branching, and distributing your image

A primary goal of Singularity is mobility. The single file image format makes mobility easy. Because Singularity images are single files, they are easily copied and managed. You can copy the image to create a branch, share the image and distribute the image as easily as copying any other file you control!



## Starting

### Preparing the work environment

You will need a Linux system to run Singularity natively. Options for using Singularity on Mac and Windows machines, along with alternate Linux installation options are discussed in the installation guides.

So after this part we assume that you have singularity installed for your system.

### The Singularity Usage Workflow

There are generally two groups of actions you must implement on a container; management (building your container) and usage.

![Workflow](https://sylabs.io/guides/2.5/user-guide/_images/flow.png)

On the left side, you have your build environment: a laptop, workstation, or a server that you control. Here you will (optionally):

- develop and test containers using --sandbox (build into a writable directory) or --writable (build into a writable ext3 image)
- build your production containers with a squashfs filesystem.

And on the right side a consumer profile for containers.


### Singularity Commands

To work with the singularity there are really only a few commands that provide us with all the operations:

- `build` : Build a container on your user endpoint or build environment
- `exec` : Execute a command to your container
- `inspect` : See labels, run and test scripts, and environment variables
- `pull` : pull an image from Docker or Singularity Hub
- `run` : Run your image as an executable
- `shell` : Shell into your image

### Run a test

Go to the environment where you have Singularity installed to do some tests. You can test your installation like so:

```
vagrant@ska-training:~$ singularity pull docker://godlovedc/lolcow
```

This command will simply download an image that already exists in Docker (docker://godlovedc/lolcow from DockerHub: [lol docker](https://hub.docker.com/r/godlovedc/lolcow) ), and store it as a local file with SIF format.


Confirms you have a file named: `lolcow_latest.sif`: 

```
ls -l lolcow_latest.sif
```

Then, we execute the image as an executable: 

```
vagrant@ska-training:~$ singularity run lolcow_latest.sif
 ____________________
< Beware of Bigfoot! >
 --------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```



