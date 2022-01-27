

# Introduction to Singularity containers

[[_TOC_]]

## Objectives and scope
In this tutorial we will work with a containerization system called Singularity, which has many features that make it interesting for workflow development and long-term reproducibility.

We will cover the following:

- Singularity and Docker
- Preparing the work environment
- Use of Singularity
- Create our first container
- Share your work!

## What is Singularity and what advantages does it have over Docker.

Singularity is a container platform. It allows you to create and run containers that package up pieces of software in a way that is portable and reproducible. You can build a container using Singularity on your laptop, and then run it on many of the largest HPC clusters in the world, local university or company clusters, a single server, in the cloud, or on a workstation down the hall. Your container is a single file, and you don’t have to worry about how to install all the software you need on each different operating system.


**Advantages:**

- Easy to learn and use (relatively speaking)
- Approved for HPC (installed on some of the biggest HPC systems in the world)
- Can convert Docker containers to Singularity and run containers directly from Docker Hub
- [SingularityHub](https://cloud.sylabs.io/)


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

So after this part we assume that you have Singularity installed for your system.

### The Singularity Usage Workflow

There are generally two groups of actions you must implement on a container; management (building your container) and usage.

![Workflow](https://sylabs.io/guides/2.5/user-guide/_images/flow.png)

On the left side, you have your build environment: a laptop, workstation, or a server that you control. Here you will (optionally):

- develop and test containers using --sandbox (build into a writable directory) or --writable (build into a writable ext3 image)
- build your production containers with a squashfs filesystem.

And on the right side, a consumer profile for containers.


### Singularity Commands

To work with the Singularity there are really only a few commands that provide us with all the operations:

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

This command will simply download an image that already exists in Docker (`docker://godlovedc/lolcow` from DockerHub: [lol docker](https://hub.docker.com/r/godlovedc/lolcow) ), and store it as a local file with SIF format.


Confirms you have a file named: `lolcow_latest.sif`: 

```
ls -l lolcow_latest.sif
```

Then, we execute the image as an executable, simply typing: 

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

## Interact with images

### Using an image for SKA training

We have prepared an image that is available in the Singularity image repository ( [link here](https://cloud.sylabs.io/library/manuparra/ska/skatrainingplot) ). This container image contains the following:

- It creates a python framework that includes the python libraries: `scipy`, `numpy` and `mathplotlib`.
- It includes a python application that draws a plot in a output file.

The source code to generate it is located [here](link) (we will work on it later).

### Pulling the new image

This download takes about 300 MBytes.

```
vagrant@ska-training:~$ singularity pull library://manuparra/ska/skatrainingplot:latest
```

After that you will see a new file named `skatrainingplot_latest.sif` with the downloaded image.


### Entering the images from a shell

The shell command allows you to open a new shell within your container and interact with it as though it were a small virtual machine. This would be very similar to what you do with docker and run a shell with bash (`docker run .... /bin/bash`):

```
vagrant@ska-training:~$  singularity shell skatrainingplot_latest.sif
```

Once executed you will be connected to the container (yopu will see a new prompt):

```
Singularity skatrainingplot_latest.sif:~> 

```

From here you can interact with container, and  you are the *same user* as you are on the host system.

```
Singularity skatrainingplot_latest.sif:~> whoami

vagrant

Singularity skatrainingplot_latest.sif:~> id

uid=900(vagrant) gid=900(vagrant) groups=900(vagrant),27(sudo)

```

**NOTE**

If you use Singularity with the shell option and and image from `library://`, `docker://`, and `shub://` URIs this creates an ephemeral container that disappears when the shell is exited.

### Executing command from a container

The exec command allows you to execute a custom command within a container by specifying the image file. For instance, to execute the cowsay program within the `skatrainingplot_latest.sif` container:

To do that, type `exit` from Singularity container and you will return to your host machine. Here, we can execute commands within the container, but not entering on the container. Executing something and then exiting at the same time 

```
vagrant@ska-training:~$ singularity exec skatrainingplot_latest.sif python3
Python 3.8.10 (default, Nov 26 2021, 20:14:08) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.

``` 
This way you are running `python3` from the container with all the libraries that the container has provided. And once we exit the python shell we return to the host. 

Type `CTRL+D` to exit from the python3 shell, and you will return to your host machine.

This is very interesting because we can run something in the container environment that does something, in this case the container provides specific libraries, which are not on the host machine. To try this, we run the following on the host machine:

```
vagrant@ska-training:~$ python3
Python 3.6.9 (default, Dec  8 2021, 21:08:43) 
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'numpy'

```
You can see that we haven't installed `numpy`, so we can't use `numpy`.

Now we execute `python3` within the container:

```
vagrant@ska-training:~$ singularity exec skatrainingplot_latest.sif python3
Python 3.8.10 (default, Nov 26 2021, 20:14:08) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy

```

Our container has `numpy` and other libraries installed, so you can use them.

In this way we could use the container to execute a script that we have created and run it with all the environment that enables the container, in this case some libraries in some specific versions. 
This is important because it allows to isolate the host environment with our development, with this we could have different containers with different library versions for example. To test it, we create a `python` file in our host machine:

```
vi test.py
```

And we add the following content:

```
import numpy as np
a = np.arange(15).reshape(3, 5)
print(a)
```

Then we can execute it typing the following:


```
vagrant@ska-training:~$  singularity exec skatrainingplot_latest.sif python3 test.py
[[ 0  1  2  3  4]
 [ 5  6  7  8  9]
 [10 11 12 13 14]]

```

If we try it on our host machine:

```
vagrant@ska-training:~ $ python3 test.py 
Traceback (most recent call last):
  File "test.py", line 1, in <module>
    import numpy as np
ModuleNotFoundError: No module named 'numpy'
```


### Running a container

Singularity containers can execute runscripts. That is, they allow that when calling them from Singularity with the exec option, they execute a scripts that define the actions a container should perform when someone runs it.

In this example for `lolcow_latest.sif` you can see a message, that is generated because for this container the developer has created a start point when you call Singularity with the option `run`.

```
vagrant@ska-training:~$ singularity run lolcow_latest.sif
 _____________________________________
/ You have been selected for a secret \
\ mission.                            /
 -------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

`run` also works with the `library://`, `docker://`, and `shub://` URIs. This creates an ephemeral container that runs and then disappears.

Now we try with our container:

```
vagrant@ska-training:~/builkd$ singularity run skatrainingplot_latest.sif 
-----------------------------------------------
SKA training: Git and Containers
Plot generated in example.png by default, please provide an output plot file
```

And now you can see that this command has generated an image called `example.png`.

With this option we can run an application already predefined in the container, but this is not always the default option and depends on how the container was built.

```
vagrant@ska-training:~/builkd$ singularity run skatrainingplot_latest.sif myplotforska.png
-----------------------------------------------
SKA training: Git and Containers
Plot generated in myplotforska.png file.
```

This command has generated an image called `myplotforska.png`.


## Interact with files

**It is important to comment that a key feature is that from the container we have access to the host files in a transparent way.**

For instance:

```
vagrant@ska-training:~$ singularity shell skatrainingplot_latest.sif 
```

And then if you type `ls -l`, you will see your own files from the folder you were. *You are in the container* :smile:. 

So here, you can create a file:

```
Singularity skatrainingplot_latest.sif :~> echo "This is a SKA training" > hello.txt
```

You can see the file created inside the container but it is also in your host folder.

```
Singularity skatrainingplot_latest.sif :~> exit
vagrant@ska-training:~$ ls -l
...
hello.txt
...
```

**By default Singularity bind mounts `/home/$USER`, `/tmp`, and `$PWD` into your container at runtime.**

## Build images

And now the question is, how can I create my own container with my software?

With `build` option you can convert containers between the formats supported by Singularity. And you can use it in conjunction with a Singularity definition file to create a container from scratch and customized it to fit your needs.


### Downloading a container from Docker Hub

You can use build to download layers from Docker Hub and assemble them into Singularity containers.

```
$ sudo singularity build lolcow.sif docker://godlovedc/lolcow
```

### Building containers from Singularity definition files

Singularity definition files,  can be used as the target when building a container. Using the Docker equivalence, these would be the Dockerfile's we use to build an image.

Here you can see an example of a definition file `lolcow.def`:

```
Bootstrap: docker
From: ubuntu:16.04

%post
    apt-get -y update
    apt-get -y install fortune cowsay lolcat

%environment
    export LC_ALL=C
    export PATH=/usr/games:$PATH

%runscript
    fortune | cowsay | lolcat
```

We can build it with:

```
$ sudo singularity build lolcow.sif lolcow.def
```

Now we can see how the test container we have made for ska is built (`skatraining.def`):

```
Bootstrap: docker
From: ubuntu:20.04

%post
apt-get update && apt-get install -y vim python3 python3-pip
pip3 install matplotlib
pip3 install scipy
pip3 install numpy

cat << EOF > /plot.py

import numpy as np
import sys
from scipy.interpolate import splprep, splev

import matplotlib.pyplot as plt
from matplotlib.path import Path
from matplotlib.patches import PathPatch

plotname = sys.argv[1] if len(sys.argv)>1 else "example.png"

N = 400
t = np.linspace(0, 3 * np.pi, N)
r = 0.5 + np.cos(t)
x, y = r * np.cos(t), r * np.sin(t)
fig, ax = plt.subplots()
ax.plot(x, y)
plt.xlabel("X value")
plt.ylabel("Y value")
plt.savefig(plotname)
print("-----------------------------------------------")
print("SKA training: Git and Containers")
print("Plot generated in " + plotname + " file.")
print("-----------------------------------------------")
EOF 

%runscript
  if [ $# -ne 1 ]; then
        echo "-----------------------------------------------"   
        echo "SKA training: Git and Containers"   
        echo "Plot generated in example.png by default, please provide an output plot file"
        exit 1
  fi
  python3 /plot.py $1
```

Then we build with:

```
$ sudo singularity build skatraining.sif skatraining.def
```

We now explain each of the components of the build file:

- Where the image comes from and what is the component:
```
Bootstrap: docker
From: ubuntu:20.04
```

- What will be done in the image to build it. In our case include some packages and libraries, and add a python file that makes some plots.
```
%post
```


- What we will execute when the container is called with the `run` option.
```
%runscript
```

And this is all for now with containers. In the following training sessions we will go deeper into the use of containers.

