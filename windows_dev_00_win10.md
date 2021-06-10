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

### Continue downloading package manually under or use a *package manager*. I'll try [Scoop](https://scoop.sh/) personally

## [Scoop documentation](https://scoop-docs.vercel.app/docs/getting-started/Quick-Start.html#requirements)
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

Install Keeweb


## Prog

VSCode
JetBrains IDE
Insomnia
GIT
Docker