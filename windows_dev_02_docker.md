---
layout: ../../layouts/thoughtPost.astro
title: The Docker install recipe
abstract: Now that we've a working local environment, running on WSL2, let's install Docker in it!
categories: 
- WindowsDev
- Win10
- WSL2
- Docker
published: true
date: 20210705
---
# In this post I bulk up and install Docker!

I left you with a beautifull Linux distro running on WSL2 last time. I'm sure that you were able to bloat it correctly since?
Well let's see how, why and especially which commands to use to run Docker.

## The intro

First you should make sure you're able to connect to your Linux box from your normal Windows explorer. You can add a shortcut to it by [connecting a new network drive, explained in the official Microsoft documentation](https://support.microsoft.com/en-us/windows/map-a-network-drive-in-windows-10-29ce55d1-34e3-a7e2-4801-131475f9557d). My shortcut points to `\\wsl$\Ubuntu-20.04\home\MYLINUXUSERNAME` so that I can easily drag and drop file into it, open files from it (usefull when adding your ssh key to github for example, hint hint).

Then, you should [create a Github account](https://github.com/join?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home) if you don't have one. I'll not get into details about github but you should learn it because it will be used **every single hour** in your future job. Learn the 5 basics commands of it and you're well more advanced that a good part of your peers. I can't stress how important it is. There's [amazing ressources like Atlassian](https://www.atlassian.com/git) to learn more about it. Take the time now to really learn it, it's tedious, it takes time but it's an amazing tool far better than sharing files on FileZilla.

Now we will create a SSH key for the WSL distro. To do so [follow the amazing tutorial hosted on GitHub](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account). What you need to know about SSH is that  
> It allow to authenticate yourself securely, as long as nobody get access to your private key. You've a pair of keys and they must match, you give people access to your public one. An analogy is the fact that everyone may send you an email but you're the only one who can read it (I came up with it on the spot, don't shoot me).

So follow along the [linked Github tutorial](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) to generate the key, then you've to add it in your Github settings. To do so, go into the connected drive you created earlier and open your `.ssh/id_ed25519.pub` file with VSCode. If you can't see said folder, I invite you to go to the first part of this serie when I talk about enabling hidden files or just [follow this tutorial from Microsoft](https://support.microsoft.com/en-us/windows/view-hidden-files-and-folders-in-windows-10-97fbc472-c603-9d90-91d0-1166d1d9f4b5#:~:text=Open%20File%20Explorer%20from%20the,folders%2C%20and%20drives%20and%20OK.).  
Add this key under `Settings > SSH and GPG keys` or go to [github.com/settings/keys](github.com/settings/keys) directly.

## The Docker install

Now we will install [Docker](https://www.docker.com/) on our Ubuntu box. To do so [follow the Docker documentation directly](https://docs.docker.com/engine/install/ubuntu/) but everything is on this page also if you're using following along and using Ubuntu.

First install the required dependencies  
```dos
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
Yes you can install multiple packages at once using this syntax. You could chain them together without the `\` but it would be a lot more clustered.

Add Docker's official GPG key and then add the **stable** repository using the 2 followings code blocks. (The one I show here is for amd64 processors. [Docker documentation has the commands for other versions](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository))
```dos
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
```dos
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

To finish we install the engine by running this code block
```dos
sudo apt-get update && sudo apt-get install docker-ce docker-ce-cli containerd.io
```
To make sure Docker is installed just run a simple `Hello World` container, you've to manually start the Docker service before.
```dos
sudo service docker start && sudo docker run hello-world
```

And that's it. We've installed Docker inside our WSL2 install. Our development environment is starting to take shape. Onwards!