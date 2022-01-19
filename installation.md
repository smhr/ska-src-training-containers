[[_TOC_]]

# :satellite: Installation instructions for the SKA hands-on Containerization

To work in SKA-Training it is necessary to have these three components installed **Git**, **Docker** and **Singularity**. We propose two alternatives to have them in your system, please choose one of them and follow the instructions below:

- [All-in-one installation](#all-in-one-installation) using Virtual Box and Vagrant.
- [Manual installation](#manual-installation) of the three dependencies:[Git](#git), [Docker](#docker), [Singularity](#singularity).

Follow the instructions for your Operating System. Linux, MAC OS or Windows.

## :package: All-in-one installation

With this installation you will be able to use all the tools that we are going to use in this SKA-Training from an environment that has everything up and ready to work. To enable this environment, it is necessary to install some components. First you need to install de components Virtual Box and Vagrant, and then you need to deplot the SKA training environment.

**Minimum requirements**:

> A 64-bit Intel CPU or Apple Silicon CPU
> macOS Catalina (10.15) (or higher)
> Command Line Tools (CLT) for Xcode (from `xcode-select --install` or `https://developer.apple.com/download/all/`) or Xcode
> At least 2 GBytes of available RAM and 50 GB minimum storage.


### Linux

First install VirtualBox for your system following the instructions here:

Download your VirtualBox [Linux](https://www.virtualbox.org/wiki/Linux_Downloads) version.

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

Finally, deploy SKA-Training environment:

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

Once in this environment, you can access

```
cd /vagrant
```

Where you will be able to share and view/work with the files stored in that directory on your host machine.

Finally, to confirm that everything is installed and working, run the following commands in this environment:

*Check `git`*

```
git --version
```

*Check `docker`*

```
docker --version
```

*Check `singularity`*

```
singularity --version
```

That's all, :smile: enjoy our :milky_way: :rocket: SKA training on git and containers.


### MAC OS

First install VirtualBox for your system following the instructions here: [MacOS X](https://download.virtualbox.org/virtualbox/6.1.30/VirtualBox-6.1.30-148432-OSX.dmg).

Then, install Vagrant from brew:

```
brew install vagrant
```

From native application, download the following [file](https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.dmg) and install it.

Finally, deploy SKA-Training environment:

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

Once in this environment, you can access

```
cd /vagrant
```

Where you will be able to share and view/work with the files stored in that directory on your host machine.

Finally, to confirm that everything is installed and working, run the following commands in this environment:

*Check `git`*

```
git --version
```

*Check `docker`*

```
docker --version
```

*Check `singularity`*

```
singularity --version
```

That's all, :smile: enjoy our :milky_way: :rocket: SKA training on git and containers.


### Windows

First install VirtualBox for your system following the instructions here:

[Windows](https://download.virtualbox.org/virtualbox/6.1.30/VirtualBox-6.1.30-148432-Win.exe).

Then, install Vagrant using this file:

Vagrant for <a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_i686.msi" >32-bit</a> or <a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.msi" >64-bit</a>

Finally, deploy SKA-Training environment:

Open a Command prompt and type the following, we will create our environment project folder and the shared folder to work with :

```
md ska-training
cd ska-training
```

And then, the following to confirm you are working in a new environment (just your first time):

```
vagrant destroy
del Vagrantfile
```

Create the SKA-Training environment for vagrant:

```
set VM=ska-training/containers
vagrant init %VM%
vagrant up
vagrant ssh
```

*Remember that after this point you will be executing the commands from that virtual environment.*

Last command will allow you access to the created VM, you will see:

```
vagrant@ska-training:~$

```

Finally from there you can use the `git`, `docker` and `singularity` commands, to work on the SKA-Training.

Once in this environment, you can access

```
cd /vagrant
```

Where you will be able to share and view/work with the files stored in that directory on your host machine.

Finally, to confirm that everything is installed and working, run the following commands in this environment:

*Check `git`*

```
git --version
```

*Check `docker`*

```
docker --version
```

*Check `singularity`*

```
singularity --version
```

That's all, :smile: enjoy our :milky_way: :rocket: SKA training on git and containers.



## :clipboard: Manual installation

At the end of this installation you should have **Git**, **Docker** and **Singularity** available in your computer.

### Linux

#### :computer: Git for Linux

Probably your Linux distribution has git installed. If not, follow these instructions:

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

#### :pill: Docker for Linux

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

#### :surfer: Singularity for Linux

To install Singularity it is necessary to install some components first to fully support this container platform.

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




### MAC OS

#### :computer: Git for MAC OS

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
#### :pill: Docker for MAC OS

*Requirements:*

> MacOS must be version 10.15 (Catalina, Big Sur, or Monterey) or newer and least 4GB of RAM.

Download Docker Desktop for Mac (for Mac with Intel Architecture) [here](https://desktop.docker.com/mac/main/amd64/Docker.dmg?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-mac-amd64) (aprox. 550 MB).

Double-click `Docker.dmg` to open the installer, then drag the Docker icon to the Applications folder.

Double-click ``Docker.ap`` in the Applications folder to start Docker (you will see an icon in the Mac bar).

After that:

1. Open a terminal and verify the installation was successful by typing: `docker --version`.

#### :surfer: Singularity for MAC OS

You need to install several programs. This example uses Homebrew but you can also install these tools using the GUI.

First, optionally install Homebrew.

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Next, install Vagrant and the necessary bits (either using this method or by downloading and installing the tools manually).

Update `brew` repository:

```
brew update
```

Install VirtualBox, Vagrant, and Vagrant-manager for Catalina, BigSur:

```
brew install --cask virtualbox && brew install --cask vagrant && brew install --cask vagrant-manager
```

Install VirtualBox, Vagrant, and Vagrant-manager for Monterrey:

```
brew install virtualbox && brew install vagrant && brew install vagrant-manager
```

*Note that here you will be asked for permissions to install some system extension(s)*

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


### Windows

#### :computer: Git for Windows

Download the latest [Git for Windows installer](https://git-for-windows.github.io/) and then  install it.

Then, open a Command Prompt (or Git Bash if during installation you elected not to use Git from the Windows Command Prompt), and verify the installation was successful by typing `git --version` and checking it's showing a version greater or equal than `2.34`.

**Setting-up git configuration**

Once you have verified and installed `git`, you have to configure your credentials.

To do that, configure your Git username and email using the following commands, replacing Manuel's name with your own. These details will be associated with any commits that you create (remember to use the same name and email that you usually register with, for example the one you will use in GitLab):

```
git config --global user.name "Manuel"
git config --global user.email "manuel@email.com"
```

#### :pill: Docker for Windows

*Requirements:*

> Windows 11 64-bit, Windows 10 64-bit, at least 4GB system RAM, and BIOS-level hardware virtualization support must be enabled in the BIOS settings.

*Note: Linux kernel for Windows (WSL2) and Docker requires a Windows restart once installed.*

Download and install the Linux kernel (WSL2) [update package](https://docs.microsoft.com/windows/wsl/wsl2-kernel).

Then, download and install Docker Desktop [here](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe).

Double-click `Docker Desktop Installer.exe` to run the installer. Docker Desktop does not start automatically after installation. To start Docker Desktop: *Search for Docker and execute it* (you will see a Docker icon within the taskbar).


After that verify if Docker is installed, up and running correctly by opening a Command Prompt and running the `hello-world` image, to do this:

Open a Command Prompt and type the following:

```
docker run hello-world
```

#### :surfer: Singularity for Windows

Singularity cannot run natively on Windows or Mac because of basic incompatibilities with the host kernel. For this reason, the Singularity community maintains a set of Vagrant Boxes via Vagrant Cloud, one of Hashicorp’s open source tools.

*Note: Singularity for Windows requires a restart once installed.*

Install the following programs:

- Git for Windows - [Download and install git](https://git-for-windows.github.io/).
- VirtualBox for Windows  -  [Download and install VirtualBox](https://www.virtualbox.org/wiki/Downloads).
- Vagrant for Windows - <a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_i686.msi" >32-bit</a> or <a href="https://releases.hashicorp.com/vagrant/2.2.19/vagrant_2.2.19_x86_64.msi" >64-bit</a>.
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

*Note: This command needs some time to complete :smile:*

You can check the installed version of Singularity with the following:

```
singularity version
```

Your version should be greater or equal than `3.0`.
