---
layout: ../../layouts/blogPost.astro
title: WSL2 basic installation
abstract: So we want to install Linux on a Windows 10 machine? All that without using VMs? Here's the post you've been looking for!
categories: 
- WindowsDev
- Win10
- WSL2
published: false
---
# The why of this post

First of all, as a Youtube content creator said whom I don't recall the name *Learning by teaching is the best way*. And I'm at a moment in my career that I want to apply this concept, let's see if it sticks for more than 2 weeks...

That's it. I finally decided to start software development on my Windows machine, well I already did software development on this machine but it was a messy process.

It's clear that Windows is a bit behind other operating systems when it comes to the development experience. The terminal experience was lackluster when I last used it, using PowerShell is great but you've to explicitly allow it to launch script, Spotlight is dearly missed (but can now be replaced with the amazing [Power Toys, that you can download from there,](https://docs.microsoft.com/en-us/windows/powertoys/install) to have the same quick `command + space` launcher experience).

I don't want to have to dual boot to a Linux distro, I did it in the past and managing disk partitions, space and boot order is too much work, call me lazy, I assume it. A Hackintosh is also out of the question. So it's going to be WSL2 : I've heard of it, I know the basic overview `It lets you run Linux on Windows` but I've never used it. I never used Docker containers extensively either, I can launch one up but that's it. That's what I aim to learn to do right now. Create a development environment using WSL2 & Docker containers. Why you may ask?

- I've to get a portofolio up and running.
- If it could've a blog attached to it that would be great.
- I've already decided to go with Strapi as a *backend* (please don't hurt me).
- Either NextJS or Svelte for the front-end application. I still need to decide.
- I don't want to install NodeJS and have to manage depencies from Windows.
- I want to learn new things and Docker seems to be an excellent candidate.
- I want people to be able to launch my pets projects easily (a man can dream).

## So how do I start this journey?
---
This article will mainly focus on getting WSL2 up and running, it's a quick painless jobs that I've written far too much words on already...

Let's start with a clean install of Windows 10 21H1 : I only had 4GB left on my C drive and it was driving me crazy. [If you want to know more about my own definition of clean install]() (I think I've developed a fast and efficient TODO List for a clean install during the years, I added new things recently so I'll see how this work out).

45min later and my install is done. Time to install WSL2, a quick Google search (if people knew that Google is what keep us afloat...) tells me to use the following code block from an elevated PowerShell prompt.

`dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`

Next we enable virtualization. **This command will restart your pc add the `/norestart` option at the end if you don't want to**

`dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all`

and we've to do a restart after. Thanks to modern browsers I can get right back to the next command... Oh wait, I haven't enabled Virtualization in my BIOS (btw it's called SVM on Ryzen chips). Back to the configuration.

Go [on Microsoft help pages](https://aka.ms/wsl2kernel) and install the required update to be able to run WSL version 2. To finish with the installation of it just do:  

`wsl --set-default-version 2`

My WSL installation is up and hopefully using version 2, which I've been told is *better* and I will go with that explanation for now. To check that, we need to install our Linux subsytem aka distribution.

I choose Ubuntu, I've no strong feelings with any of them and I know it's one of the largest community, plus Manjaro is not available on the Windows Store. Btw, if you like me never use a Microsoft Account you just have to deny any account request and can still install things from the Store.

Finally launch your installed distribution, set up an user and a password and there you go. Check from a terminal the list of running distributions with `wsl -l -v` & hopefully you should see the following in your terminal.

| NAME            | STATE     | VERSION |
|---              |---        |---      |
| Ubuntu-20.04    | Running   | 2       |

You're running a Linux distribution from Windows without having to fiddle with VMWare or others. Which, if I say so, is **pretty** cool. What an age we lives in!

Btw if you've selected Ubuntu as your distribution you should upgrade the installed packages right away to start from a clean & up-to-date state. Just enter the following commands in your terminal

to get an up-to-date list of software versions  
`sudo apt update`  
to install those new versions  
`sudo apt upgrade`  
or combine them into this one liner  
`sudo apt update && sudo apt upgrade`

In the next blog post we will focus on Docker and creating our contained waste management system, I mean development environment!  
Feel free to read further for WSL/PowerShell/ZSH customization and other things.

### Quick tips
- Your BIOS can be accessed by pressing DEL at boot and the virtualization option is, most of the time, in the Advanced Settings under CPU configuration.
- If you want to forcefully remove a directory from PowerShell use `Remove-Item PATH -Force`.
- Install [Windows Terminal from the Microsoft Store](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab) it handles your Winux (yeah, I like this) distribution natively
 
### Linux tips
- Install ZSH in your Linux installation if you're used to it `sudo apt install zsh`
- Switch the main linux shell to ZSH `chsh -s $(which zsh)`
- Install Oh-My-Zsh for cool color and auto-completion `sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
- If you want to install a them for OhMyZsh just [browse the available themes](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes) and RTFM!
- Reload your Zsh settings with `source ~/.zshrc`

Further down we're talking of Windows Terminal and Oh-My-Zsh customization, feel free to leave

### WSL Customization
### This is only for fonts
I had some problems with PowerLine font not displaying correctly inside the Windows Terminal and had to fix it.
- I followed [this tutorial](https://medium.com/@hjgraca/style-your-windows-terminal-and-wsl2-like-a-pro-9a2e1ad4c9d0) & [this one by Dev Genius](https://blog.devgenius.io/make-your-powershell-7-truly-powerful-eb56b3fbe37f).

- I've since started using [this repository](https://github.com/ryanoasis/nerd-fonts) to get all my normal fonts with added nerdiness. Still need to do a PR to change the name of *FuraCode* back to *FiraCode* oh well...I'm using JetBrains Mono for now!
- To set the default font for the whole Windows Terminal add this to the config.json inside the `profiles.defaults` object
>   "fontFace": "JetBrainsMono Nerd Font",  
>   "fontSize": 14

Another problem I then encoutered following this guide is with the Install-Module command. It appears PowerShell does not auto-update to the latest version, or should I say Windows comes bundled wiht an older version, so I add to [manually download it from their website](https://aka.ms/powershell-release?tag=stable). The joy of Windows development once again.

**Now for some Windows Terminal customization**

Since I really got accustomed to using the terminal while using my Mac and iTerm2, I wanted to reproduce nearly the same experience on Windows

That's it for installing WSL2. In the next blog post I will talk about installing the required tools inside our Linux development box running on Windows 10 from the Windows Terminal connected to it (isn't this phrase amazing? Is your mind melting? It's part of the learning process I've been told).

See you next time!




