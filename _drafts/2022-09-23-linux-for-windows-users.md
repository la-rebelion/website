---
layout: post_jekflix
title: Linux for Windows Users
description: "You love Linux, but for some reason (job) you are stuck with Windows. Here I show you how to have the best of both worlds at the same time!"
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
categories: Linux
tags: [sysadmin linux]
cta:
  description: "Subscribe to get latest articles"
  short_text: I am in!
  destination: 
---

If you are a Windows user and Linux wannabe, or you use Linux daily on your job, or simply, you prefer Linux, but somehow you are stuck on a Windows PC; then, you will love this: WSL Windows Subsystem for Linux and Multipass.

These are two options you will love, trust me! Stay with me and I will show you a brief comparison of these for you to decide which one to use.

Spoiler alert, I prefer WSL and use it daily, but Multipass is practical and fast... but, let me stop here and put my hands on the flour to cook this; let's start to review and compare.

With a lot of Linux distros available, it is sometimes complicated to choose which one to use. Also, installing and configuring each distro is time-consuming and not easy for a newbie. Furthermore, they are not easily portable.

WSL is a Windows Subsystem for Linux that allows you to run native Linux applications directly on Windows. It has everything you need to run a full Ubuntu environment, including a Bash shell, core utilities, and the ability to install any compatible software.

WSL has been available for Windows 10 since the Anniversary Update, and it's included in every version of Windows 10 from that point on. It's also compatible with any Linux distribution built for ARM64 (see below).

Multipass by Canonical, the Ubuntu creators, is a software that allows you to run Ubuntu on Windows 10. It's not a virtual machine, but it gives you access to a full Ubuntu environment that runs in parallel with Windows. You can install any compatible Linux software by downloading an APT repository and running "apt-get install". 

Installation

There are three ways to install WSL: via the Windows Subsystem for Linux, via Ubuntu on Windows, or by installing a distro from the command line. Installation via Windows Subsystem for Linux is easiest and requires no additional software; simply search for "bash" in your Start menu or taskbar. Alternatively, if you want to install a distro from the command line (which is required if you want to run Linux software that's not part of the Windows store or pre-installed on your system), you'll need to install Ubuntu on Windows or another distro and then make sure that "Windows Subsystem for Linux" is enabled. You can do this by right-clicking on your start menu and selecting "Turn Windows features on or off" in the context menu or by navigating to Control Panel > Programs > Turn windows features on or off. Once you have Windows Subsystem for Linux enabled, open Bash by searching for "bash" in your Start menu or taskbar. You should see a command prompt pop up with the words "Ubuntu on Windows" at the top of it. If you don't, try restarting your computer. 

From here, you can type commands into the command prompt to install programs such as Git and Python. For example, if you want to install git on Windows 10 with Ubuntu Linux, type the following command into Bash:

Instance Creation

You’ll notice that when you open Bash for the first time, there isn’t an option to create a new instance of Ubuntu Linux. You can only access the one instance that’s already available. However, if you want to create a new instance on Windows 10 with Ubuntu Linux, it’s pretty easy to do so. Just type "bash" into your Start menu or taskbar and select "Ubuntu on Windows" from the list of results that appear. 

Comparison

The main difference between Bash on Ubuntu Linux and Ubuntu on Windows is that the latter allows you to run more than one instance of Ubuntu Linux at a time. You can even run different versions of Ubuntu simultaneously, which is great if you want to test out how well your favorite applications work in different releases.

Why do I prefer WSL over Multipass?

First of all, Windows Subsystem for Linux isn’t a “subsystem,” at least not in the traditional sense. It isn’t an emulation layer that allows you to run Linux applications on top of Windows like VirtualBox or Wine; it’s just a way to run native Ubuntu Linux binaries directly on your PC. The filesystem is shared easily between both Operative Systems, which means that you can access your Linux files from Windows and vice versa. This is a huge advantage over other methods of running multiple operating systems on the same computer, like VirtualBox or VMware. Windows Subsystem for Linux also offers better performance than virtualization software like VirtualBox because it doesn’t have to boot up a full-blown Linux instance every time you launch an app.

Windows Terminal by Microsoft allows you to have multiple tabs to easily access different sessions, either Windows (bash) or Linux (bash). Windows Terminal is a modern host application for command-line shells.

Bonus

Install those tools to improve your productivity as a developer!

nccm

rvm

nvm

