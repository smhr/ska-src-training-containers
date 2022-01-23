# Building your own containers

There are now many images that contain some of the most popular software. Often they will be enough to meet your needs. Just go to the [**Docker Hub**](https://hub.docker.com/search?q=&type=image)and see for yourself how many images there are available **(8,766,202 at the time of writing)**.

Chances are however that you work in a specialised field and none of these millions of images will do what you need, or they do, but not exactly how you would like them to. One of the main driving forces behind the increasing use of containers is the ability for the developers to package their software inside the image and provide end users with a stable environment. You can do it with your software as well, and that is what we are going to learn now.

## In this section you will learn

- [**How to build Docker images**](#1-building-docker-images)

## 1. Building Docker images

The development of every Docker image starts with a Dockerfile. It is a recipe that contains a series of commands for installing and configuring software packages included in your image. As we will see below, we can think of a Dockerfile as a collection of regular shell expressions combined with an extra Docker syntax that tells Docker how to construct the image. If you have used a *nix system before, this Dockerfile should look familiar:

```docker
FROM ubuntu:18.04

WORKDIR /software

RUN apt update && apt -y install git \
  && git clone https://gitlab.com/ska-telescope/src/ska-src-training-containers.git

CMD ./ska-src-training-containers/Talks/containers-build/files/hello_docker.sh
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
