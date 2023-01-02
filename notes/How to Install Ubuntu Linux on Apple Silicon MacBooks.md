_If you enjoy this topic, you will probably like my articles, tweets, and stuff. If you're wondering, check out my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow since I'm offering programming and motivating tools and information to help you achieve your dreams._

Linux is a really good operating system for development and many large corporations like Amazon use it for their backend. Today we will learn how to install and set up the popular Ubuntu Linux on Apple Silicon MacBooks. This has been tested and is working on macOS Ventura 13.1.

There are 3 good virtualisation tools available on Macs and we will be using two of them to install Ubuntu Linux. The list of 3 is:

[UTM](https://mac.getutm.app/) (FREE)
[Parallels Desktop for Mac](https://www.parallels.com/uk/) (Paid but has a FREE trial)
[VirtualBox](https://www.virtualbox.org/) (FREE)

We won't be using VirtualBox because as of writing it does not have good support for Apple Silicon MacBooks although it should work if you have an older Intel model.

## UTM Setup

UTM is a virtualisation tool for ARM64 operating systems to operate on Apple Silicon at close to native speeds, UTM uses Apple's Hypervisor virtualization technology.

### 1. Download and install UTM

Before we begin the first thing that you will need to do is download the latest version of the macOS virtualisation software [UTM](https://mac.getutm.app/).

### 2. Download the ARM version of Ubuntu

Next, you will have to download the latest version of Ubuntu Linux and ensure that it is the ARM version which will work on Apple Silicon computers.

You should be able to find the latest version in one of these links:

[64-bit ARM (ARMv8/AArch64) desktop image](https://cdimage.ubuntu.com/jammy/daily-live/current/jammy-desktop-arm64.iso)

[Ubuntu 22.04.1 LTS (Jammy Jellyfish)](https://cdimage.ubuntu.com/releases/22.04/release/)

### 3. Install and setup Ubuntu using UTM

Now use UTM to set up Ubuntu by configuring the settings for your personal setup. Follow the example setup and tailor it to your own preferences. This stage is the longest but it will be much faster when you have got it installed.

Select the Virtualize option.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337085/utm-setup-01_z8wclt.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337085/utm-setup-01_z8wclt.jpg)

Choose Linux for the Operating System

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337147/utm-setup-02_ui95ij.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337147/utm-setup-02_ui95ij.jpg)

Use a similar configuration as below and use the browse button to find your Linux iso image.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337176/utm-setup-03_a18yfc.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337176/utm-setup-03_a18yfc.jpg)

Configure your hardware settings like in the example.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337233/utm-setup-04_srdblo.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337233/utm-setup-04_srdblo.jpg)

I chose 64GB storage you can use whatever you want just make sure its enough so maybe minimum 20GB.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337277/utm-setup-05_dke3xe.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337277/utm-setup-05_dke3xe.jpg)

You can choose a shared directory so it can connect to a folder in your macOS environment. I chose the Downloads folder you can choose any folder.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337352/utm-setup-06_ewqdfi.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337352/utm-setup-06_ewqdfi.jpg)

Just give it a name and select save.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337438/utm-setup-07_ogg12a.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337438/utm-setup-07_ogg12a.jpg)

Open the UTM settings menu and set the display to Retina so it's nice and sharp.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337502/utm-setup-08_sbgtrl.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337502/utm-setup-08_sbgtrl.jpg)

It's go time! Hit the play button and start it up!

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337572/utm-setup-09_opjado.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337572/utm-setup-09_opjado.jpg)

Select the option for Try or Install Ubuntu and then eventually you will reach the Ubuntu home screen. We are almost done! In the bottom right-hand corner of the desktop, you will see an Install icon. Click on it and follow the setup until you get to the installation type screen.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337634/utm-setup-10_zyoy2o.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337634/utm-setup-10_zyoy2o.jpg)

Choose the first option it won't wipe your main macOS hard drive so don't worry! It's only using the virtual machine storage.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337864/utm-setup-11_akfpxn.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337864/utm-setup-11_akfpxn.jpg)

Create your user details and don't forget the username and password you will need that for the login!

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672337977/utm-setup-12_jlwjqp.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672337977/utm-setup-12_jlwjqp.jpg)

Now restart your computer inside the VM and you should be at the Ubuntu homes screen after you login. Next you will probably need to install the latest updates for Ubuntu. If for whatever reason it crashes you can try to do the Ubuntu installation again or restart the VM to get it working.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672338045/utm-setup-13_ajtct2.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672338045/utm-setup-13_ajtct2.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672339121/utm-setup-14_hjv7gu.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672339121/utm-setup-14_hjv7gu.jpg)

### 4. Open the Terminal application

Open the applications menu and then start the Terminal application. Lets setup a basic starter development environment.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672339225/utm-setup-15_fwkfzm.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672339225/utm-setup-15_fwkfzm.jpg)

### 5. Make sure Ubuntu has the latest packages

Copy and paste these commands into the terminal and then press the enter key to run them. These commands will update all of your packages in Ubuntu.

```shell
sudo apt update
sudo apt upgrade
```

### 6. Download and install Visual Studio Code

Download and install the latest version of Visual Studio Code and make sure that it is the Linux version that has the `.deb` file extension at the end [https://code.visualstudio.com/](https://code.visualstudio.com/).

### 7. Install git

Use the commands below inside of your Terminal window to install git.

```shell
sudo apt install git
```

### 8. Install zsh and Oh My Zsh (optional)

This step is optional but well worth it in my opinion.

> Oh My Zsh is a delightful, open source, community-driven framework for managing your Zsh configuration. It comes bundled with thousands of helpful functions, helpers, plugins, themes, and a few things that make you shout...

Firstly install `zsh` using the command below in your Terminal.

```shell
sudo apt install zsh
```

Then use this curl command to install Oh My Zsh. You can find the GitHub repo here [https://github.com/ohmyzsh/ohmyzsh](https://github.com/ohmyzsh/ohmyzsh).

If you don't have `curl` installed then install it first.

```shell
sudo apt  install curl
```

```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### 9. Install npm and Node.js

Lets now install npm and Node.js which we are definitely going to need for installing JavaScript packages. You can find the latest versions of Node.js here [https://github.com/nodesource/distributions/blob/master/README.md](https://github.com/nodesource/distributions/blob/master/README.md)

As of writing the latest version is **Node.js v19.x**. We can use the command below in our Terminal to install npm and Node.js.

```shell
curl -fsSL https://deb.nodesource.com/setup_19.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

### 10. Install Docker Engine

It is time for us to install Docker. Please be aware that at the moment the Docker Desktop application does not have a version for ARM unfortunately.

> Docker Desktop on Linux runs a Virtual Machine (VM) so creates and uses a custom docker context `desktop-linux` on startup. This means images and containers deployed on the Linux Docker Engine (before installation) are not available in Docker Desktop for Linux. For more information see [What is the difference between Docker Desktop for Linux and Docker Engine](https://docs.docker.com/desktop/faqs/linuxfaqs/#what-is-the-difference-between-docker-desktop-for-linux-and-docker-engine)

They only have versions for Intel, AMD and Apple Silicon, there is no supported version for Linux. It's unfortunate but we can still use Docker we will just have to use the command line. Developers live in the command line anyway 😉 You can find all of the Docker commands here [https://docs.docker.com/engine/reference/commandline/docker/](https://docs.docker.com/engine/reference/commandline/docker/).

Follow the steps in the Docker documentation to [install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/).

## Parallels Desktop for Mac Setup

Since version 16.5 it also supports Macintosh systems with Apple silicon-based CPUs. Parallels Desktop for Mac is software that offers hardware virtualization for Macintosh computers with Intel processors.

### 1. Download and install Parallels Desktop for Mac

Go here and download it [https://www.parallels.com/uk/](https://www.parallels.com/uk/)

### 2. Install and setup Ubuntu using Parallels

The Parallels Ubuntu Linux installation is considerably simpler because there is an automated setup. See the example images of the setup below to give you an idea. When you have completed the installation you can go to step **4. Open the Terminal application** in the UTM setup to install your development environment because it's the same process.

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672341910/parallels-setup-01_hmudcx.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672341910/parallels-setup-01_hmudcx.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672341926/parallels-setup-02_wxgnto.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672341926/parallels-setup-02_wxgnto.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672341940/parallels-setup-03_yrajzd.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672341940/parallels-setup-03_yrajzd.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672341953/parallels-setup-04_klfja4.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672341953/parallels-setup-04_klfja4.jpg)

![https://res.cloudinary.com/d74fh3kw/image/upload/v1672341965/parallels-setup-05_mxsk2o.jpg](https://res.cloudinary.com/d74fh3kw/image/upload/v1672341965/parallels-setup-05_mxsk2o.jpg)

_If you like this article, chances are that you would like my posts, tweets and content as well. If you are curious, have a look at my [social media profiles](https://limey.io/andrewbaisden) and don't forget to subscribe and follow because I am sharing programming and motivation resources and knowledge to support you in achieving your goals 💫_
