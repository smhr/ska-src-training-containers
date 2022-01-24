# Building your own containers

There are now many images that contain some of the most popular software. Often they will be enough to meet your needs. Just go to the [**Docker Hub**](https://hub.docker.com/search?q=&type=image)and see for yourself how many images there are available **(8,766,202 at the time of writing)**.

Chances are however that you work in a specialised field and none of these millions of images will do what you need, or they do, but not exactly how you would like them to. One of the main driving forces behind the increasing use of containers is the ability for the developers to package their software inside the image and provide end users with a stable environment. You can do it with your software as well, and that is what we are going to learn now.

## In this section you will learn

- [**How to build Docker images**](#1-building-docker-images)
- [**How to build Singularity containers**](#2-building-singularity-containers)
- [**What to consider before building**](#3-general-considerations-before-building)

## 1. Building Docker images

The development of every Docker image starts with a Dockerfile. It is a recipe that contains a series of commands for installing and configuring software packages included in your image. As we will see below, we can think of a Dockerfile as a collection of regular shell expressions combined with an extra Docker syntax that tells Docker how to construct the image. If you have used a *nix system before, this Dockerfile should look familiar:

```docker
FROM ubuntu:18.04

WORKDIR /software

RUN apt update && apt -y install git \
  && git clone https://gitlab.com/ska-telescope/src/ska-src-training-containers.git

CMD ./ska-src-training-containers/Talks/containers-build/files/hello_container.sh
```

- **The first line**
  
    ```docker
    FROM ubuntu:18.04
    ```

    is a must for your Dockerfile. The `FROM` instruction tells Docker
    which *base image* to use. Think about it like a basic OS installation
    on your new machine: you install bare-bones OS and then add the
    required software.

    Here we tell Docker to use a pre-build image as the
    foundation we will build upon. We use an `ubuntu:18.04` base
    image. There are base images available for all the most popular Linux operating
    systems (or as close as possible to what you may need) as well as Windows.

    Not only we tell Docker to use an ubuntu image, but also specify an
    additional *tag*. This tag allows you to document possible multiple
    versions of the same software stack. If no tag is specified, the `latest` tag
    is used by default. This is bad practice from the reproducibility point of
    view as you always download the newest version of the software and can run into
    problems with dependencies and software stability.

- **Let's install some software**
    We then proceed to install some software:

    ```docker
    RUN apt update && apt -y install git \ 
      && git clone git clone https://gitlab.com/ska-telescope/src/ska-src-training-containers.git
    ```

    The above line is exactly what you would run when installing software on your Debian-based machine, with the additional `RUN` instruction which tells Docker to execute the command and include the results in the
    image. The outcome is not unexpected - our new image will have `git` installed and the repository for this course will be cloned into the `/software/ska-src-training-containers/` directory (we changed the directory for the `RUN` command with `WORKDIR` instruction above).

    We divide the command into multiple lines by using `\` (backslash), which tells Docker that these lines form a single `RUN` command. There is nothing stopping us from writing the whole command on a single line but that can produce unreadable Dockerfiles (like any badly-structured code).

    Also note how we put all of our commands as part of the same `RUN` instruction. In principle, there is nothing stopping us from using multiple run instruction, but each `RUN` instruction creates a separate layer, which increases the size of the final image.

    ```docker
    RUN apt update && apt -y install git
    RUN git clone https://gitlab.com/ska-telescope/src/ska-src-training-containers.git
    ```

## 2. Building Singularity containers

We will now recreate the same recipe, but this time with Singularity. In this case, we are using a *Singularity definition file*. As before, we use this file to speficy a series of instructions that will install software, move the data, etc. to form our final container.

```singularity
Bootstrap: docker
From: ubuntu:18.04

%post
  apt -y update
  apt -y install git
  mkdir /software/
  git -C /software/ clone https://gitlab.com/ska-telescope/src/ska-src-training-containers.git

%runscript
  /software/ska-src-training-containers/Talks/containers-build/files/hello_container.sh
  ```

- **Header**

    ```singularity
    Bootstrap: docker
    From: ubuntu:18.04
    ```

    Your definition file should always have a header at the very beginning of the file. First we instruct the build system of the bootstrap agent. Think of it as a source of your base image. `Bootstrap` is also a required keyword and has to be present **on the first like of every definition file**. In the above definition file we let Singularity know that we would like to build our container based on a Docker image. THis is an important feature than makes transition from Docker to Singularity relatively easy - you can still use Docker images to not only run them with Singularity, but also use them as base layers in your definition files.

    We again use a specific version of Ubuntu, the same one as with our Dockerfile. Feel free to experiment and use different versions of Ubuntu or even completely different operating systems!

- **Installing software**

    After installing our base operating system, we are now ready to install some software. Singularity definitions file have a dedicated `%post` section for this purpose:

    ```singularity
    %post
      apt -y update
      apt -y install git
      mkdir /software/
      git -C /software/ clone https://gitlab.com/ska-telescope/src/ska-src-training-containers.git

    ```

    The main difference is how we create our `/software` directory and clone the repository into it. We explicitly create the directory and then use it as the parent directory for our repo. After that, you can access the training materials when running the container from `/software/ska-src-training-containers`.

Here we covered only the most basic definition file structure. For more details please see [**Singularity documentation**](https://apptainer.org/user-docs/master/definition_files.html)

- **Run something**

  The last section, `%runscript` specifies what we would like to execute when the container is run. Here we just execute our script that prints our a welcome message. You can however include multiple commands in this section. You can even pass options to your commands, just the way you would when writing regular Bash scripts.

## 3. General considerations before building

Docker and Singularity handle some of the building and execution details quite differently (and the differences are not only in syntax that you have seen). There are however few best practices and things you have to consider before creating your Dockerfiles or Singularity definition files and creating your images and containers.

- **Do you need that software?** - it might be very tempting to install software "just in case" At the end of the day we all need our favourite text editor, our favourite programming language and other tools that make our life easier. Both our Docker image and Singularity container are relatively small, around 100MB in size, but we have not done much in them, just installed `git` and downloaded this training repository, but this is just a single package, on top of a relatively small base OS. When you are working on your own containers you have to make sure you only include software that you actually need. Make sure you only use libraries/modules that you absolutely need. If you are developing software and need additional tools such as compilers and debuggers, it is always a good idea to maintain two version of your images: one for development work and another, much smaller containing production-ready code. Make sure that your base images are not unnecessarily heavy. Do you need a whole operating system or could you work with its smaller version? Do you need all the packages and libraries provided by the software developer? This point is especially important if you store your images in a remote repository and have to often upload and download them.
  
- **Do you need that data?** - similar to deciding on which software is obsolutely necessary for smooth operation of your container, you need to include as little external data as possible. It is often good idea to provide some data for testing purposes to make sure that the user has all the software working correctly, but the size of this dataset should be kept to an absolute minimum.

- **DO NOT store any secrets** - never store any passwords inside your build recipes (this one is kind of obvious) or inside final build products. It is easy to forget to get rid of them and in some cases (Docker layers) it is possible to make them invisible in the final product but still be discoverable by anyone with acces to the image. If you need to use a password, for example to download a private git repository, please consider alternative approaches.

- **Share your recipes** - if you intend for other researchers to run your containers, make sure you also make recipes available. It is important that you comment them, so that anyone trying to recreate your work can do it easily.
