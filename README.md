# Hands-on Containerization

[[_TOC_]]

## :satellite: SKA regional centre training event

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

# :rocket: Get everything installed 

To work in SKA-Training it is necessary to have these three components installed **Git**, **Docker** and **Singularity**, which you can install [manually](#manual-installation) ( [Git](#git), [Docker](#docker), [Singularity](#singularity) ) or you can use our [all-in-one environment](#all-in-one-installation).


## :clipboard: Manual installation

### :octocat: Git 

Choose your operating system to install it: 

[Git for Mac OS ](#git-for-mac-os-x), [Git for Linux ](#git-for-linux) or [Git for Windows](#git-for-windows) 

####  Git for Mac OS X

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

#### Git for Linux

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


#### Git for Windows

Download the latest [Git for Windows installer](https://git-for-windows.github.io/) and install it.

Then, open a Command Prompt (or Git Bash if during installation you elected not to use Git from the Windows Command Prompt), and verify the installation was successful by typing `git --version`.
 
**Setting-up git configuration**

Once you have verified or installed `git`, you have to configure your credentials.

To do that, configure your Git username and email using the following commands, replacing Manuel's name with your own. These details will be associated with any commits that you create (remember to use the same name and email that you usually register with, for example the one you will use in GitLab):

```
git config --global user.name "Manuel"
git config --global user.email "manuel@email.com"
```

### :pill: Docker

[Docker for Mac OS ](#docker-for-mac-os-x), [Docker for Linux ](#docker-for-linux) or [Docker for Windows](#docker-for-windows) 

#### Docker for MacOS X

*Requirements:*

> MacOS must be version 10.15 (Catalina, Big Sur, or Monterey) or newer and least 4GB of RAM.

Download Docker Desktop for Mac (for Mac with Intel Architecture) [here](https://desktop.docker.com/mac/main/amd64/Docker.dmg?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-mac-amd64) (aprox. 550 MB).

Double-click `Docker.dmg` to open the installer, then drag the Docker icon to the Applications folder. 

Double-click ``Docker.ap`` in the Applications folder to start Docker (you will see an icon in the Mac bar).

After that: 

1. Open a terminal and verify the installation was successful by typing: `docker --version`.

#### Docker for Linux

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

#### Docker for Windows

*Requirements:*

> Windows 11 64-bit, Windows 10 64-bit, at least 4GB system RAM, and BIOS-level hardware virtualization support must be enabled in the BIOS settings.

Download Docker Desktop [here](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe).

Double-click `Docker Desktop Installer.exe` to run the installer. After installation Docker Desktop does not start automatically after installation. To start Docker Desktop: Search for Docker and execute it (you will see a Docker icon within the taskbar).

After that verify if Docker Engine is installed correctly by opening a Command Prompt and running the `hello-world` image:

```
sudo docker run hello-world
```


### :surfer: DSingularity

To install Singularity it is necessary to install some components first to fully support this container platform. 

[Singularity for Mac OS ](#singularity-for-mac-os-x), [Singularity for Linux ](#singularity-for-linux) or [Singularity for Windows](#singularity-for-windows) 

### Singularity for Linux

**CentOS / Fedora**

```
sudo apt-get update && sudo apt-get install -y build-essential libssl-dev uuid-dev libgpgme11-dev squashfs-tools libseccomp-dev pkg-config
```


**Debian / Ubuntu**

```
sudo yum update -y && sudo yum groupinstall -y 'Development Tools' &&  sudo yum install -y openssl-devel libuuid-devel libseccomp-devel wget squashfs-tools
```

For all flavours, download and install Go (Go Lang):

```
wget https://go.dev/dl/go1.17.6.linux-amd64.tar.gz
```

Then run the following as root or through sudo: 

```
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.17.6.linux-amd64.tar.gz
```

Add `/usr/local/go/bin` to the PATH environment variable:

```
export PATH=$PATH:/usr/local/go/bin
```

Then fix changes: 

```
echo 'export GOPATH=${HOME}/go' >> ~/.bashrc && \
    echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
    source ~/.bashrc
```

Verify that you've installed Go by opening a command prompt and typing the following command:

```
go version
```

Since we are installing Singularity v3.x you will also need to install `dep` for dependency resolution.

```
go get -u github.com/golang/dep/cmd/dep
```

Download, compile and install Singularity:

Clone respository

```
go get -d github.com/sylabs/singularity
```

Get an specific version

```
export VERSION=v3.0.3  &&  cd $GOPATH/src/github.com/sylabs/singularity && git fetch && git checkout $VERSION
```

Compling and installing Singularity

```
./mconfig && make -C ./builddir && sudo make -C ./builddir install

```

After that verify if Singularity Engine is installed correctly by running: 

```
singularity --version
```

### Singularity for Windows

Singularity cannot run natively on Windows or Mac because of basic incompatibilities with the host kernel. For this reason, the Singularity community maintains a set of Vagrant Boxes via Vagrant Cloud, one of Hashicorp’s open source tools.

Install the following programs:

- Git for Windows - [Download and install git](https://git-for-windows.github.io/).
- VirtualBox for Windows  -  [Download and install VirtualBox](https://www.virtualbox.org/wiki/Downloads).
- Vagrant for Windows - <a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_i686.msi" >32-bit</a><a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.msi" >64-bit</a>.
- Vagrant Manager for Windows - [Donwload and install VManager](https://github.com/lanayotech/vagrant-manager-windows/releases/download/1.0.2.2/VagrantManager-1.0.2.2-Setup.exe)


Run GitBash (Windows) and create and enter a directory to be used with your Vagrant VM.

```
mkdir vm-singularity && cd vm-singularity
```

If you have already created and used this folder for another VM, you will need to destroy the VM and delete the Vagrantfile.

```
vagrant destroy && rm Vagrantfile
```

Then issue the following commands to bring up the Virtual Machine. (Substitute a different value for the $VM variable if you like.)

```
export VM=sylabs/singularity-3.0-ubuntu-bionic64 && vagrant init $VM && vagrant up && vagrant ssh
```

You can check the installed version of Singularity with the following:

```
singularity version
```

### Singularity for MacOS X

You need to install several programs. This example uses Homebrew but you can also install these tools using the GUI.

First, optionally install Homebrew.

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Next, install Vagrant and the necessary bits (either using this method or by downloading and installing the tools manually).

```
brew cask install virtualbox && brew cask install vagrant && brew cask install vagrant-manager
```

Open a Terminal and create and enter a directory to be used with your Vagrant VM.

```
mkdir vm-singularity && cd vm-singularity
```

If you have already created and used this folder for another VM, you will need to destroy the VM and delete the Vagrantfile.

```
vagrant destroy && rm Vagrantfile
```

Then issue the following commands to bring up the Virtual Machine. (Substitute a different value for the $VM variable if you like.)

```
export VM=sylabs/singularity-3.0-ubuntu-bionic64 && vagrant init $VM && vagrant up && vagrant ssh
```

You can check the installed version of Singularity with the following:

```
singularity version
```


## :package: All-in-one installation

With this installation you will be able to use all the tools that we are going to use in this SKA-Training from an environment that has everything up and ready to work. 

###  Vagrant - Virtual Machine

To enable this environment, it is necessary to install some components. First you need to [install the components](#install-components) and then [deploy the environment](#deploy-ska-training-environment).

#### Install components

First install VirtualBox for your system (Linux, MacOSX or Windows):

- [Windows](https://download.virtualbox.org/virtualbox/6.1.30/VirtualBox-6.1.30-148432-Win.exe).
- [MacOS X](https://download.virtualbox.org/virtualbox/6.1.30/VirtualBox-6.1.30-148432-OSX.dmg).
- Download your VirtualBox [Linux](https://www.virtualbox.org/wiki/Linux_Downloads) version.

Then, install Vagrant for your Operating System:

**For Debian/Ubuntu**

```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install vagrant
```

**For Fedora/CentOS**

```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install vagrant
```

**For Windows**

Vagrant for <a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_i686.msi" >32-bit</a> or <a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.msi" >64-bit</a>

**For MacOS X**

From brew:

```
brew install vagrant
```

From native application, download the following [file](https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.dmg) and install it.

#### Deploy SKA-Training environment

**For MacOS X**

Open a Terminal and type the following, we will create our environment project folder and the shared folder to work with :

```
mkdir ska-training && cd ska-training
```

And then, the following to confirm you are working in a new environment (just your first time):

```
vagrant destroy && rm Vagrantfile
```

Create the SKA-Training environment for vagrant:

```
export VM=ska-training/containers && vagrant init $VM && vagrant up && vagrant ssh
```

After that, you will see:

```
vagrant@ska-training:~$

```

Finally from there you can use the `git`, `docker` and `singularity` commands, to work on the SKA-Training.

**Once in this environment, you can access**

```
cd /vagrant
```

Where you will be able to share and view/work with the files stored in that directory on your host machine.


## Training checklist

TBC.


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



