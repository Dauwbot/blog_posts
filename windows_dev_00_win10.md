# Windows install

### Which version to chose
Preferably install an Education version, you can always [download the most up-to-date version from Microsoft own ISO creation tool](https://go.microsoft.com/fwlink/?LinkId=691209) - Why Education instead of Pro? Less bloatware to remove right after installation, [it's basically a fork of Pro without all the added fluff](https://support.microsoft.com/en-us/topic/windows-10-editions-for-education-customers-bf2572aa-5555-2b1e-f7ce-81e8ba890444#:~:text=Windows%2010%20Pro%20Education%20builds,including%20the%20removal%20of%20Cortana*.). You will have to provide your own license of course.

### Right after installation
Don't connect to internet - You can but Windows will start downloading older display drivers on it's own
Create a Domain account so your user name in windows is what you want
Install graphic drivers - [nvidia](https://www.nvidia.com/Download/index.aspx) or [amd](https://www.amd.com/en/support)

### Now you've a choice to make (not mandatory)
I started isolating my installs in different directory than default, on a different drive even. You can access the repository folder from `regedit` at this address in  
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion`. You need to do this before anything else or Chrome will break for example (ask me how I know...). Edit both values of `ProgramFilesDir` & `ProgramFilesDir (x86)` for 64 & 32 bits software respectively.


### Back to installation
Install Chrome from Edge. Set Chrome as default browser (sorry Edge, yes I do really want to switch and not *check you out*). Connect to Google Account, I don't care what you think about this, it's easy and I'm really really enjoying the fact that I can access my thousands of favorites from anywhere (I'm playing the meme game here, I only have like 100).

Recomended extensions for Chrome
---
- [uBlock Origin](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm?hl=en) (duh)
- [Kmdr](https://chrome.google.com/webstore/detail/kmdr/lbigelojleemicaaaogihjnabfndkdii) - Display code blocks on website and let you interact with them, you can see what each commands do, and code blocks are really enhanced. Highly recommended
- [React Dev Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) - I'll see your nested components
- [Momentum](https://chrome.google.com/webstore/detail/momentum/laookkfknpbbblfpciffpaejjkokdgca) - I try to use ToDo lists, I suck at this

Let's resume our programs installation

First install [Windows required runtimes and SDK](https://dotnet.microsoft.com/download/dotnet). I link directly to the download page you're grown ass developers.  
Then install [PowerToys](https://aka.ms/installpowertoys). Why? It has Fancy Zones & I can launch program at *la Spotlight* by pressing the `alt + space` shortcut and once you get used to it you can do without.  

## [Continue downloading programs manually](#those-are-the-tools-i-use-to-develop-and-should-come-pre-installed-with-windows) or use a *package manager*. I'll try [Scoop](https://scoop.sh/) personally

### [Scoop documentation](https://scoop-docs.vercel.app/docs/getting-started/Quick-Start.html#requirements)
Since I've a separated drive for my install let's use it  

All the infos underneath is copy/pasted from [Scoop documentation](https://scoop-docs.vercel.app/docs/getting-started/Quick-Start.html#requirements)
From an elevated default Powershell installation. This will install scoop in your selected directory  
`$env:SCOOP='DRIVELETTER:\scoopDirectory'`  
`[environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')`  
Then change the scoop packages install location  
`$env:SCOOP_GLOBAL='DRIVELETTER:\scoopInstallDir'`  
`[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')`  

You can then install Scoop apps using  
`scoop install -g <app>`

I will need git for sure so for example I will do  
`scoop install -g git` and it will install git, and at the same time 7Zip which is needed to extract the portable version of git and which I would have installed anyway, winwin

I'll get deeper into Scoop in another blog post. There's some caveat to be aware off : for example I add to manually add git to my path otherwise my terminals didn't know what I was talking about. It's a quick 2min job when you know what to do but it can be a pain. For now I'll finish listing my essentials apps for a developer using Windows, you go and install them how you want it was just a quick overview of Scoop as a package manager.

## Those are the tools I use to develop and should come pre-installed with Windows
- [Your JetBrains IDE of choice](https://www.jetbrains.com/products/) - I mainly use [Rider](https://www.jetbrains.com/rider/) since I prefer it, for my junior use, to [Visual Studio]() when I've to work with .NET projects. I also use it [to work with Unreal](https://www.jetbrains.com/lp/rider-unreal/). Btw it's free to access while in preview.  
- I need to get used to [WebStorm](https://www.jetbrains.com/webstorm/) since I mainly do WebDev but Rider works well on it's own so...  
- [Visual Studio Code](https://code.visualstudio.com/) I like it for the lightning fast launch time when working with .json files. I know people use it as their main development software but I feel like having to add multiple extensions, debuging code and all that is more suited to a full fledged IDE. I also like to always **run as administrator** so I can launch PowerShell commands that require elevation from it. 
- [Insomnia](https://insomnia.rest/download) - It's my REST API tester, I know people use [Postman](https://www.postman.com/product/api-client/) also, I just like it better!
- An [updated version of PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-7.1) - Seriously it will save you some headaches later down the StackOverflow line.
- Finally [install WSL (version 2 preferrably)](https://docs.microsoft.com/en-us/windows/wsl/install-win10). Another article is coming out about it. I would love to have a clean development experience using Docker containers & WSL
- Talking about it. If you so which to follow along this serie, [install Docker right now](https://docs.docker.com/docker-for-windows/install/)
- If you want to learn gamedev chose between [Unity](https://unity.com/) & [Unreal](https://www.unrealengine.com/en-US/), how to chose? This is a sensible subject.
-  You want to do 2D platformers? Go with [Unity](https://store.unity.com/download-nuo).
-  You want hyper-realistic environment to do architecture representation? Go with [Unreal](https://www.unrealengine.com/en-US/download). 
- [Version 5 is coming](https://www.unrealengine.com/en-US/unreal-engine-5) soon and it's an exciting time to join!

## Those are my apps, I like them
- [KeeWeb](https://keeweb.info/) - Password manager. Available as a WebApp (access them from my Google Drive account remotely) or a desktop app  
- [Thunderbird]() - My favorite mail client. Can be used with [Protonmail](https://protonmail.com/) when installing the [Protonmail bridge](https://protonmail.com/bridge/)  
- [Affinity Design Suite](https://affinity.serif.com/en-gb/) - I bought them on sale, they are replacement for Photoshop/InDesign/Lightroom. I need to use them more.

And that's all for me. Yes you can install whatever games launcher you want but it's not the topic here. You should now have a working base to start developing on Windows and not have to switch when it's past 5 and you want to game some!  
See you soon for the next parts of this serie: we will talk about WSL2, Docker and containers (oh man, that's gonna be fun, I'm so well versed in it! /s) and finally how to develop a web app using mordern tooling, and that's something I would've loved to get a view on from someone without 5+ years in the industry working at a top tier FAANG or up-scale start-up, and that's the main motivator behind this serie.