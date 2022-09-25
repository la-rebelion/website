---
layout: post_jekflix
title: Linux for Windows Users
description: "You love Linux, but for some reason, you are stuck with Windows. Here I show you how to have the best of both worlds at the same time!"
image: https://images.unsplash.com/photo-1629654297299-c8506221ca97?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1074&q=80
references:
  photo:
    from: Gabriel Heinzer
    url: https://unsplash.com/@6heinz3r?utm_source=la-rebelion&utm_medium=referral
    source: unsplash
  articles:
    - url: https://learn.microsoft.com/en-us/windows/wsl/install
      text: Install Linux on Windows with WSL
    - url: https://multipass.run
      text: Ubuntu VMs on demand
    - url: hhttps://canonical.com
      text: Canonical
    - url: hhttps://learn.microsoft.com/en-us/windows/terminal/
      text: Windows Terminal
    - url: https://www.cygwin.com/
      text: Open Source tools which provide functionality similar to a Linux distribution on Windows
    - url: https://mobaxterm.mobatek.net/
      text: MobaXterm free Xserver and tabbed SSH client for Windows
categories: Linux
tags: [sysadmin, linux]
cta:
  description: "Subscribe to get latest articles"
  short_text: I am in!
  destination: 
---

If you are a Windows user; but love Linux (as most developers are), or you use Linux daily on your job on remote servers, or simply, you prefer Linux, but somehow you are stuck on a Windows PC; then, you will love this: WSL (Windows Subsystem for Linux) and Multipass.

With a lot of Linux distros available, it is sometimes complicated to choose which one to use. Also, installing and configuring each distro is time-consuming and not easy for a newbie. Furthermore, they are not easily portable. To solve this problem, Windows user has been using [cygwin](https://www.cygwin.com/), or [MobaxTerm](https://mobaxterm.mobatek.net/), because these are great Linux emulators and allows you to feel like you are in your natural environment.

These are two options you will love most, trust me! Stay with me and I will show you a brief comparison of these for you to decide which one to use.

Spoiler alert, I prefer WSL and use it daily, but Multipass is practical and fast... but, let me stop here and put my hands on the flour to cook this cake; let's start to review and compare.

**WSL** is a Windows Subsystem for Linux that allows you to run native Linux applications directly on Windows. It has everything you need to run a full Ubuntu environment, including a Bash shell, core utilities, and the ability to install any compatible software. WSL has been available for Windows 10 since the Anniversary Update, and it's been included in every version of Windows 10 from that point on. It's also compatible with any Linux distribution built for ARM64.

**Multipass** by Canonical, the Ubuntu creators, is a software that allows you to run Ubuntu on Windows 10. It's not a virtual machine, but it gives you access to a full Ubuntu environment that runs in parallel with Windows. You can install any compatible Linux software by downloading an APT repository and running `apt-get install`.

## Installation

### WSL

There are three ways to install WSL: via the Windows Subsystem for Linux, via Ubuntu on Windows, or by installing a distro from the command line. Installation via Windows Subsystem for Linux is easiest and requires no additional software; simply search for "bash" in your Start menu or taskbar. Alternatively, if you want to install a distro from the command line (which is required if you want to run Linux software that's not part of the Windows store or pre-installed on your system), you'll need to install Ubuntu on Windows or another distro and then make sure that "Windows Subsystem for Linux" is enabled. You can do this by right-clicking on your start menu and selecting "Turn Windows features on or off" in the context menu or by navigating to *Control Panel > Programs > Turn windows features on or off*. Once you have Windows Subsystem for Linux enabled, open Bash by searching for "bash" in your Start menu or taskbar. You should see a command prompt pop up with the words "Ubuntu on Windows" at the top of it. If you don't, try restarting your computer.

<iframe width="640" height="360"
src="https://www.youtube.com/embed/SvwzSiC4gv0?autoplay=1">
</iframe>

From here, you can type commands into the command prompt to install programs such as `Helm` or `Python`, just as you would do on Linux, this is a Linux kernel!
<div class="tenor-gif-embed" data-postid="16548735" data-share-method="host" data-aspect-ratio="1.05611" data-width="33%"><a href="https://tenor.com/view/kanye-west-blink-blinking-eyes-attitude-gif-16548735">Kanye West Blink GIF</a>from <a href="https://tenor.com/search/kanye+west-gifs">Kanye West GIFs</a></div> <script type="text/javascript" async src="https://tenor.com/embed.js"></script>

### Multipass

1. [Download Multipass Installer for Windows](https://multipass.run/download/windows).
2. Run the downloaded installer. Be sure to add the Multipass directory to your `PATH` during the installation process.
3. Open a new Powershell or `cmd` session and follow the steps in the next section to create an instance.

## Instance Creation

You’ll notice that when you open Bash for the first time, there isn’t an option to create a new instance of Ubuntu Linux. You can only access the one instance that’s already available. However, if you want to create a new instance on Windows with a specific Linux distro, it’s pretty easy to do so. Just type `cmd` into your Start menu or taskbar, then list the available distros and install it from the list of results that appeared.

### WSL

`wsl --list -o`

![WSL List distros]({{page.url}}/wsl-list-o.png)

`wsl --install -d <Distro>`

Examples:

```sh
wsl --install -d Ubuntu
wsl --install --distribution Debian
```

### Multipass

what options do we have?

`multipass find`

![Multipass List available versions]({{page.url}}/multipass-find.png)

```sh
# let's try Ubuntu 22.04
multipass launch --name la-rebelion-rules --cpus 2 --mem 3G --disk 6G jammy
# connect to the VM
multipass shell la-rebelion-rules
```

If you want to share the filesystem between Windows and Linux instance, you must mount the directory on Windows, but, before you will need to install 'multipass-sshfs' in the Linux instance. With WSL you don't need these extra steps.

```sh
# Update the apt package index
sudo apt-get update
sudo apt-get -y install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg \
  lsb-release \
  sshfs

mkdir -p ~/la-rebelion-dir && cd $_
```

Go to a PowerShell session (On Windows host) and type:

`multipass mount <source> <target> [<target> ...]`

Example:  
`multipass mount . la-rebelion-rules:~/la-rebelion-dir`

## Comparison

One great thing about these two options, WSL and Multipass, is that both allow you to run more than one instance of Ubuntu Linux at a time. You can even run different versions of Ubuntu simultaneously, which is great if you want to test out how well your favorite applications work in different releases.

The main difference is that the WSL allows you to run different Linux distributions, such as Ubuntu, Debian, Alpine, openSUSE, AlmaLinux, OracleLinux or Kali for Free, other options with cost are Pengwin, Rocky.

Both have available the latest version of Ubuntu, 22.04, Jammy Jellyfish!

Multipass provides images with `docker` and `minikube` ready to run.

WSL shares the full Windows filesystem, while, with Multipass you need to mount the directories you would like to share, only. Tedious if there are several directories you work with.

### Why do I prefer WSL over Multipass?

First of all, Windows Subsystem for Linux isn’t a “subsystem,” at least not in the traditional sense. It isn’t an emulation layer that allows you to run Linux applications on top of Windows like VirtualBox or Wine; it’s just a way to run native Ubuntu Linux binaries directly on your PC. The filesystem is shared easily between both Operative Systems, which means that you can access your Linux files from Windows and vice versa. This is a huge advantage over other methods of running multiple operating systems on the same computer, like VirtualBox or VMware. Windows Subsystem for Linux also offers better performance than virtualization software like VirtualBox because it doesn’t have to boot up a full-blown Linux instance every time you launch an app.

Windows Terminal by Microsoft allows you to have multiple tabs to easily access different sessions, either Windows (bash) or Linux (bash). Windows Terminal is a modern host application for command-line shells.

## Bonus

Install these tools to improve your productivity as the super developer or sysadmin you are!

* [nccm](https://github.com/flyingrhinonz/nccm) - NCurses ssh Connection Manager (nccm)
* [rvm](https://rvm.io) - Ruby Version Manager allows you to easily install, manage, and work with multiple ruby environments from interpreters to sets of gems.
* [nvm](https://github.com/nvm-sh/nvm) - Node Version Manager allows you to quickly install and use different versions of node via the command line.
* [z](https://github.com/rupa/z) - You don't need to type and remember the FULL path to those most used directories, `z` will take you to the most 'frequent' directory that matches the regexes given on the command line.
* [octant](https://github.com/vmware-tanzu/octant) - Single pane of glass for ALL your Kubernetes clusters.

If you found this post useful, don't forget to spread the voice, share it on your social media, and recommend us to help more DevOps and SysAdmin fellows to take advantage of these tips.
