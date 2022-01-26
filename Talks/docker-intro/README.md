# Introduction to Docker

In this section you will learn the basics of Docker, arguably one of the most popular containerisation technologies. Since its initial release in 2013, Docker has been widely adopted in many areas of research and the ‘industry‘. It is used to provide access to e-commerce and streaming services, machine learning platforms and scientific pipelines (CERN, SKA, NASA).

More generally, you should use it as a tool for distributing consistent software environments. Currently it is only one of many existing container technologies that researchers can choose from. Two popular alternatives are Singularity (covered later) and Podman. Some solutions offer better support for High Performance Computing, while others provide a low-level control of the environment. There really is something for everyone.

## In this section you will learn

- [**How to start Docker containers**](#1-running-first-docker-container)
- [**How to manage your Docker images**](#2-managing-docker-images)
- [**How to manage your Docker containers**](#3-managing-docker-containers)
- [**How to work with Docker containers**](#4-working-with-docker-containers)

## 1. Running first Docker container

For our first example, we will run a short Docker command to download the *Hello World* of **Docker images** and start our very first **Docker container**.

```docker

$ docker container run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete 
Digest: sha256:9f6ad537c5132bcce57f7a0a20e317228d382c3cd61edae14650eec68b2b345c
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

```

### **Let's examine the command and the generated output step by step.**

- **The command that we execute**
  
    ```docker
    $ docker container run hello-world
    ```

    instructs Docker that we would like to start a container using a `hello-world` image. This command can also be written as `docker run hello-world`, omitting the `container` part. This change was [**introduced in 2017**](https://www.docker.com/blog/whats-new-in-docker-1-13/) with a major overhaul of the Docker CLI (Command Line Interface). If the version of Docker installed on your machine comes from before these changes were introduced (we strongly recommend that you upgrade it due to security reasons), the full command will not work and you will have to use the short version. This section however is written with the new versions of Docker in mind and will **follow the convention of using the extended versions of the commands**.

- **The next few lines**

    ```docker
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    b8dfde127a29: Pull complete 
    Digest: sha256:9f6ad537c5132bcce57f7a0a20e317228d382c3cd61edae14650eec68b2b345c
    Status: Downloaded newer image for hello-world:latest
    ```

    tells us that Docker was not able to find this image on our machine and has to download it from the external repository. If you have used this particular image in the past, you will not see any information about Docker trying to download the image.

    You could also separate the `docker container run ...` command above into two instructions:

    ```docker
    $ docker image pull hello-world
    $ docker container run hello-world
    ```

    In this case we are very explicit and tell Docker to first download (pull) the image from the external repository and then start the container based on that image. If you already have the image on your host machine, you can skip the `pull` command. In this case, including the `docker image pull` separately can be seen as a bit redundant as Docker takes care of any missing images with `docker container run`. You can however just pull the image and not run it at all, or pull it when you have access to the Internet and later start the container when you are offline.

- **The rest of the output**

    The rest of the output is the most interesting part. It is an
    innocent-looking list, but as items 3 and 4 from that list explain, that
    particular part of the output was generated INSIDE the container and only
    then sent back to the terminal for us to see. That means we have **successfully
    created and run our very first Docker container**.

## 2. Managing Docker images

- **Examine local images**

    How does Docker know whether it has to download the image or that the image is already present on your computer? Can you have this knowledge as well? Docker keeps track of all the images and layers that you download. There usually is a directory on your system which contains all the currently downloaded images and the associated SHA256 keys used to identify them. This ensures that the same layer or image is not downloaded twice and can be reused if necessary. For an in-depth description on how Docker stores images, please refer to [**this help guide**](https://docs.docker.com/storage/storagedriver/).

    The placement and structure of relevant directories can be different depending on your Docker installation and require root permissions to access. There is however a short command that lists all the locally available images:

    ```docker
    $ docker image ls
    ```

    Depending on how long (if at all) you have been using Docker for, the output will show only a single image that we have used above or multiple (as many as few tens of) images, as seen below (this is what I see when I run the above command on my work PC - **you will see something different**)

    ```docker
    REPOSITORY                 TAG                      IMAGE ID       CREATED         SIZE
    <none>                     <none>                   670fa2d9f98c   2 months ago    3.14GB
    <none>                     <none>                   2187b33a009b   2 months ago    714MB
    <none>                     <none>                   16b9ad7fc05d   2 months ago    3.12GB
    python                     3.7-alpine               6c59ae21a586   2 months ago    41.6MB
    redis                      alpine                   f7cdff500577   2 months ago    32.3MB
    ubuntu                     18.04                    3339fde08fc3   3 months ago    63.3MB
    nvidia/cuda                10.0-devel-ubuntu18.04   f1cb864ecfaf   3 months ago    2.24GB
    nvidia/cuda                10.2-devel-ubuntu18.04   5fe1e15ef79b   3 months ago    2.96GB
    hello-world                latest                   d1165f221234   3 months ago    13.3kB
    jupyter/scipy-notebook     latest                   dab5e9968512   7 months ago    2.7GB
    nvidia/cuda                9.2-cudnn7-devel         0a6a8962363e   8 months ago    2.88GB
    nvidia/cuda                9.2-base                 7def1f9b9d8d   9 months ago    80.8MB
    nvidia/cuda                9.2-base-ubuntu18.04     7def1f9b9d8d   9 months ago    80.8MB
    nvidia/cuda                9.2-devel-ubuntu18.04    b06eca0e3d4a   9 months ago    2.2GB
    cuda                       8.0-base-ubuntu16.04     f240c010c4f2   10 months ago   142MB
    ubuntu                     16.04                    005d2078bdfa   14 months ago   125MB
    rabbitmq                   3.8.2                    b8956a8129ef   16 months ago   151MB
    nvidia/cuda                9.2-devel-ubuntu16.04    1874839f75d5   19 months ago   2.35GB
    nvidia/cuda                10.0-base-ubuntu18.04    841d44dd4b3c   19 months ago   110MB
    ```

    If you know its name, you can list just a specific image:

    ```docker
    $ docker image ls hello-world
    ```

    or even use wildcards if you are not sure about the full image name (was it `nvidia/cuda` or `nvidia/CUDA`?):

    ```docker
    $ docker image ls nvidia/*
    REPOSITORY    TAG         IMAGE ID       CREATED        SIZE
    nvidia/cuda   10.1-base   bfa75f8b799e   6 months ago   105MB
    nvidia/cuda   9.2-base    5eabb7ffec15   6 months ago   80.7MB
    ```

    This is the default output that tells us that there are two images starting with `nvidia/` available locally on our machine, with the `9.2-base` and `10.1-base` tags. You can treat the tags as an extra bit of information about the version of the image. Next comes the image ID, which is a shortened version of the SHA256 key (or digest, using Docker vocabulary) used to identify the image and information on when the image was created. This information refers to when the image was first built and not pulled.

    We have used the most basic version of the image listing command, with the exception of using wildcards. For a complete reference and advanced examples, such as formatting and filtering, please visit [**this docker images reference**](https://docs.docker.com/engine/reference/commandline/images/). **Quick note:** the above document refers to a `docker images` command, which is *an alias* to the full `docker image ls` command. All the options however will work with both versions of this command. You can still use it as a reference for the `--format` and `--filter` options.

- **Remove the image**

    We made sure that the container was no longer running and then we removed it. What if we want to go one step further and want to get rid of the underlying image? Docker has a fairly intuitive command for that as well - instead of removing a container, we tell it to remove the image instead:

    ```docker
    $ docker image rm  hello-world
    Untagged: hello-world:latest
    Untagged: hello-world@sha256:9f6ad537c5132bcce57f7a0a20e317228d382c3cd61edae14650eec68b2b345c
    Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
    Deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
    ```

    In this case we use the **image name** and Docker prints out the confirmation that it was removed successfully.

## 3. Managing Docker containers

- **Examine currently running containers**

    In the same way we listed the images currently available locally on our machine, we can examine currently running containers:

    ```docker
    $ docker container ls
    CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
    ```

    We see nothing really useful. This means there are no containers running at this moment in time.

    When we launched our `hello-world` container above, it started, it did the job it was designed to do and it stopped immediately. In the case of the `hello-world` image, the designers decided it should print out a helpful output once the container is launched successfully, but that may not always be the case.

    We still have an option to check whether our container was started at all. We can force Docker to list *all* the containers with the extra `-a` option:

    ```docker
    $ docker container ls -a
    CONTAINER ID   IMAGE                   COMMAND                  CREATED        STATUS                    PORTS     NAMES
    7dd021096f75   hello-world             "/hello"                 3 hours ago    Exited (0) 3 hours ago              trusting_herschel

    ```

    In this case we actually get some useful information about our container we have just run. We see that we launched the container, it ran and it exited with code 0, meaning a successful, error-free execution. We can also see when the container was created and when it completed its execution. As you have seen, we get the results from the `hello-world` container pretty much immediately, and therefore the `CREATED` and `Exited` times are the same, but generally this is not the case.

    Every container has a "human-readable" name assigned to it at launch. It makes it easier to refer to the container using that name instead of the container ID, listed in the first column of the above output. These names are randomly generated from a list of adjectives and famous scientists and Docker does not guarantee the name will repeat for the same container (it is extremely unlikely your container will have the same name as the one listed above).

    It is therefore important to provide a name with the `run` command using the `--name` option to ensure reproducible and predictable deployment. This is especially important when you run multiple  containers at the same time, e.g. making it easy to differentiate front- and backend Node-based containers that can have the same underlying image, or rely on automatic scripts that require predictable names.

    If you are running containers right now, you will see them as "Up", as below

    ```docker
    $ docker container ls -a
    CONTAINER ID   IMAGE            COMMAND                  CREATED        STATUS         PORTS     NAMES
    f1d9fa05caae   rabbitmq:3.8.2   "docker-entrypoint.s…"   2 months ago   Up 5 minutes             rabid_rabbit
    ```

- **Remove the container**

    Exited containers can be thought of as being hibernated - they are not running, their internal state is saved and they can be woken up and run again. When we are satisfied with the results provided by our container launch,  we might need to remove it. We can do this with the help of `container rm` command:

    ```docker
    $ docker container rm trusting_herschel
    trusting_herschel
    ```

    Here we used the Docker-assigned name to remove the container. We can also use the container ID to achieve the same result. Make sure you replace the name above with the name or the container ID that you got by running the `docker container ls -a` command.

## 4. Working with Docker containers
Using a `hello-world` image is one thing, actually doing some work with containers is another. As interesting as it might be, the above image doesn't do much beyond printing out the message we have seen at the start. Not very useful from the astrophysics perspective. 

We are going to experiment with a much more useful image: an official Python 3.10.2 image based on Debian bullseye (it's slimmed down version to be more specific - 123MB vs over 900MB for the 'traditional' bullseye).

Instead of just running the image, we fill first download it:

```
$ docker image pull python:3.10.2-slim-bullseye
```

If we just run it, we won't get any output like when using the `hello-wold` image (we will also explicitly test whether the container is running):


```
$ docker container run --name python-test python:3.10.2-slim-bullseye

$ docker container ls -a
CONTAINER ID   IMAGE                         COMMAND                  CREATED          STATUS                      PORTS     NAMES
67b36e6034d2   python:3.10.2-slim-bullseye   "python3"                27 seconds ago   Exited (0) 22 seconds ago             python-test
```
The container exits immediately, just like the `hello-world` one. That's because by default, there is no work to be done inside this container. We can change that. We can remove the container like we have done before, but this time, we can use the name we have provided explicitly with `--name` flag (I used `python-test`, feel free to name your container something else, just make sure you change the name in the commands that use it).

```
$ docker container rm python-test
```

I removed this container because I want to reuse the name and also keep my Docker containers to bare minimum. We can use the same image to actually start executing some code from INSIDE the running container. We will start slowly, I want to find out a version of Python available inside the running container:

``` 
$ docker container run --name python-test python:3.10.2-slim-bullseye python3 --version
Python 3.10.2
```

That's the version we expected to see based on the image we're using. Most importantly, this is version that is shipped inside this Python image and executed inside our container. You do not have to have Python installed on your host machine, or can have a completely different version (for example I am running 3.8.5 on my host) - Python inside your container is not eve aware of that other version.

But let's do some actual work. We will do it in two ways. First we will launch a very simple script that you can download from **here**. You do not have to be familiar with Python to understand what it does: we simply print out a welcome message and perform some very basic operations.

As we have mentioned before, containers by default do not know much about their host machine. Most importantly, they do not share any files with it, so they will not be able to find our Python script and run it. We therefore have to make it available inside the container.  We launch our image it with the additional options that *mount* the data inside the container:

```
docker container run --name python-test-2 --mount type=bind,source=$(pwd),target=/scripts python:3.10.2-slim-bullseye python3 /scripts/script.py
Welcome to Docker Python
8
13
2.0
0.5
We  are  done!
```
The `--mount` option may seem a bit verbose if you have not seen it before,
but it should be fairly easy to understand. First we specify the
`type=bind` to tell Docker to use a bind mount (it is not the only type of
mount we can have, but we are not going to cover them here). We then 
provide two [key]:[value] pairs separated by a comma ( , ) that specify
the source and target directory and/or file. As we are using distinctive keys,
the order of the pairs is not important, but try to keep it in some
order for consistency. 

Here we make only a single file available inside the
container, but it is also possible to make whole directories available
and bound to a directory inside your container.

**IMPORTANT:** bind mounts do not create a copy of the data! Your data is
shared between your host and container environments. Any changes that you
make to your data on the host side, will be visible inside the container
and vice versa. Be careful if you are manipulating any data that you cannot
afford to corrupt - it might be safer to make a copy in this case!

Making data available inside your container at a runtime has some obvious
drawbacks. With that approach, your data and your software are no longer
placed in a single environment. You have to rely on your end-users to 
provide their own data or to be able to access your data from external
sources. This can also increase the development time for your software, as
you have to take into account and prevent errors that users can introduce
if their data does not meet your requirements.
The decision on whether to include the data inside your image
during the build time or as a mount during the runtime will be entirely
up to you and will depend on your project and user requirements.

Second approach can be running our image *interactively*. In this case our container will behave like a usual Python CLI interpreter and we can treat it as such. 
```
docker container run --name python-test-3 -it python:3.10.2-slim-bullseye
Python 3.10.2 (main, Jan 18 2022, 20:00:03) [GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print("I'm inside the container")
I'm inside the container
```
However, we are not limited to running just Python. This particular image comes with bash installed, so we can make use of it. We can launch an ibteractive bash session and treat this container like a regular terminal (albeit with many things missing):
```
docker container run --name python-test-4 -it python:3.10.2-slim-bullseye /bin/bash
root@2decf291ee44:/# pwd
/
root@2decf291ee44:/# ls -l
total 64
drwxr-xr-x   1 root root 4096 Jan 18 20:02 bin
drwxr-xr-x   2 root root 4096 Dec 11 17:25 boot
drwxr-xr-x   5 root root  360 Jan 22 23:36 dev
drwxr-xr-x   1 root root 4096 Jan 22 23:35 etc
drwxr-xr-x   2 root root 4096 Dec 11 17:25 home
...
```
This way you can just containers not just for one-off jobs, but also use it for interactive work.

**IMPORTANT:**  Launching our container the way we did just now
may seem innocent enough, but comes with a **serious security problem**.
If you look closely at the command line prompt, we are listed as a use `root`, meaning we have administrative privileges inside the container. This becomes a very serious issue if we give our container access to any external resources such as host disks or network. We usually do not perform our day-to-day activities with privileged accounts and we shouldn't do that inside our containers either.

We can change this default behaviour by providing a `--user` flag to our `run` command:

```
docker container run --user 1000:1000 --name python-test-5 -it python:3.10.2-slim-bullseye /bin/bash
I have no name!@46023ae04069:/$
```

 We have launched a new container with user ID 1000 and
group ID 1000 (the format is `--user [user ID]:[group ID]`). As we have not
created this user inside the container, Docker has no idea who that user is
exactly, but we can still perform various tasks with the same permissions
as the original user on the host OS.
