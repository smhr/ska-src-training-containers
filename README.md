# Hands-on Containerization

## SKA regional centre training event

The Science User Engagement (SUE) group of the SKA Regional Centre Steering Commitee is glad to announce the SKA Regional Centre Training Event Series: Hands-on Containerization

This is the first event of a series that will drive the attendants to understand the basics and dig into more advanced knowledge of the technologies and instruments that will be useful to approach the Square Kilometre Array data. The event will be fully virtual, and it will consist of lectures, tutorials and practicals spread over 3 hour sessions twice a week for three weeks. The format will allow participation and engagement across different time zones.

Main webpage can be found in this [Indico event](https://indico.skatelescope.org/event/876/overview)

More details soon ...

### Registration

Registration is open here: [registration](https://indico.skatelescope.org/event/876/registrations/339/)

### Preliminary programme 

**Thursday 27/1/22:** technical support to get everything installed

**Monday 31/1/22:** lessons and tuturials (around 3 hours in total, times TBC)
- Welcome, data handling challenges and portability 
- Introduction to the first SKA science data challenge & algorithm
- Introduction to Git
- Introduction to Github/Gitlab
- Introduction to Docker/Singularity containers
- Hands on Git and Containers - Beginners

**Thursday 3/2/22:** availability for Q&A (extended time zone availability)

**Monday 7/2/22:** lessons and tutorials (around 3 hours in total, times TBC)
- Open Q&A to follow up on the issues found
- Intermediate Github - pull requests/command line
- Building your own custom containers
- Hands on Git and Containers - Intermediate

**Thursday 10/2/22:** availability for Q&A (extended time zone availability)

**Monday 14/2/22:** availability for Q&A (extended time zone availability)

# Training event materials 

## Get everything installed 

### Manual installation

#### Git 
#####  Git for Mac OS X

There are several ways to install Git on a Mac. If you've installed XCode (or it's Command Line Tools), Git may already be installed. 
To find out, open a terminal and enter `git --version`. If the command returns the git version, then it is installed, otherwise you can install [Xcode from the App Store](https://apps.apple.com/us/app/xcode/) or use the other methods below. 

**Install Git on a Mac is via the stand-alone installer**

1. Download the latest Git for Mac installer [here](https://sourceforge.net/projects/git-osx-installer/files/) and then install it.
2. Open a terminal and verify the installation was successful by typing `git --version`.


**Install Git with Homebrew**

First you need to have [HomeBrew](http://brew.sh/) installed, after that follow the next:

1. Open your terminal and install Git using Homebrew: `brew install git`.
2. Verify the installation was successful by typing `git --version`.

**Setting-up git configuration**

Once you have verified or installed `git`, you have to configure your credentials.

To do that, configure your Git username and email using the following commands, replacing Manuel's name with your own. These details will be associated with any commits that you create (remember to use the same name and email that you usually register with, for example the one you will use in GitLab):

```
git config --global user.name "Manuel"
git config --global user.email "manuel@email.com"
```

##### Git for Linux

Depending on your Linux distribution, you can use the following options.

**Debian / Ubuntu (with apt-get)**

From your shell, install Git using `apt-get`:

```
sudo apt-get update
sudo apt-get install git
```

Verify the installation was successful by typing `git --version`

**Fedora (dnf or yum)**

From your shell, install Git using dnf (or yum, on older versions of Fedora):

``
sudo dnf install git
``
or
``
sudo yum install git
``

Verify the installation was successful by typing `git --version`.

**Setting-up git configuration**

Once you have verified or installed `git`, you have to configure your credentials.

To do that, configure your Git username and email using the following commands, replacing Manuel's name with your own. These details will be associated with any commits that you create (remember to use the same name and email that you usually register with, for example the one you will use in GitLab):

```
git config --global user.name "Manuel"
git config --global user.email "manuel@email.com"
```


##### Git for Windows

Download the latest [Git for Windows installer](https://git-for-windows.github.io/) and install it.

Then, open a Command Prompt (or Git Bash if during installation you elected not to use Git from the Windows Command Prompt), and verify the installation was successful by typing `git --version`.
 
**Setting-up git configuration**

Once you have verified or installed `git`, you have to configure your credentials.

To do that, configure your Git username and email using the following commands, replacing Manuel's name with your own. These details will be associated with any commits that you create (remember to use the same name and email that you usually register with, for example the one you will use in GitLab):

```
git config --global user.name "Manuel"
git config --global user.email "manuel@email.com"
```

#### Docker

##### Docker for MacOS X

*Requirements:*
- MacOS must be version 10.15 (Catalina, Big Sur, or Monterey) or newer and least 4GB of RAM.

Download Docker Desktop for Mac (for Mac with Intel Architecture) [here](https://desktop.docker.com/mac/main/amd64/Docker.dmg?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-mac-amd64) (aprox. 550 MB).

Double-click `Docker.dmg` to open the installer, then drag the Docker icon to the Applications folder. 

Double-click ``Docker.ap`` in the Applications folder to start Docker (you will see an icon in the Mac bar).

After that: 
1. Open a terminal and verify the installation was successful by typing: `docker --version`.

##### Docker for Linux

Depending on your Linux distribution, you can use the following options.

**Debian / Ubuntu**

Older versions of Docker were called docker, docker.io, or docker-engine. If these are installed, uninstall them:

```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

Update the apt package index and install packages to allow apt to use a repository over HTTPS:

```
sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Add Docker’s official GPG key:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Use the following command to set up the stable repository:

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Update the apt package index, and install the latest version of Docker Engine and containerd

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

After that verify if Docker Engine is installed correctly by running the `hello-world` image.

```
sudo docker run hello-world
```

**CentOS / Fedora**

Older versions of Docker were called docker or docker-engine. If these are installed, uninstall them, along with associated dependencies.

```
sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

Install the dnf-plugins-core package (which provides the commands to manage your DNF repositories) and set up the stable repository.


```
sudo dnf -y install dnf-plugins-core

 sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo

```

Install the latest version of Docker Engine and containerd:

```
sudo dnf install docker-ce docker-ce-cli containerd.io
```

Start Docker

```
sudo systemctl start docker
```

After that verify if Docker Engine is installed correctly by running the `hello-world` image.

```
sudo docker run hello-world
```

##### Docker for Windows

Requirements:
- Windows 11 64-bit, Windows 10 64-bit, at least 4GB system RAM, and BIOS-level hardware virtualization support must be enabled in the BIOS settings.

Download Docker Desktop [here](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe).

Double-click `Docker Desktop Installer.exe` to run the installer. After installation Docker Desktop does not start automatically after installation. To start Docker Desktop: Search for Docker and execute it (you will see a Docker icon within the taskbar).

After that verify if Docker Engine is installed correctly by opening a Command Prompt and running the `hello-world` image:

```
sudo docker run hello-world
```



#### Singularity


## Talks

- Introduction on data handling challenges and portability - Marcella Massarti (INAF) and Anna Bonaldi (SKAO)
- Introduction to the first SKA science data challenge and algorithm - Philippa Hartley (SKAO)
- Introduction to Git - Mateusz Malenta (University of Manchester)
- Introduction to Github/Gitlab - Javier Moldón (IAA-CSIC)
- Hands on on GitLab - Manuel Parra (IAA-CSIC)
- Intro to docker/singularity containers - Manuel Parra (IAA-CSIC) and Mateusz Malenta (University of Manchester)
- Hands-on on Git and Containers - Alex Clarke (SKAO) and Manuel Parra (IAA-CSIC)
- Intermediate Github: pull requests/command line - Javier Moldón (IAA-CSIC)
- Building your own custom containers - Mateusz Malenta
- Intermediate git/docker - Alex Clarke (SKAO)



