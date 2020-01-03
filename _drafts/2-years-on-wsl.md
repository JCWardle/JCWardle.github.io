# 2 Years using WSL (Windows Subsystem for Linux)

WSL or Windows Subsystem for Linux is similar to a virtual machine that you install, but it's built right into your Windows installations. You can run all your favourite Linux distributions in Windows now. I've been running Ubuntu in WSL to develop The Big Crunch, we have three developers with a mix between Windows 10, MAC OS and a Ubuntu production server. WSL let's us Windows developers run all the Linux build utilities and scripts same as the server rather than re-writing them in Windows bash or Powershell.

## The good

### SSH is super easy

Before WSL you had to run Putty or CYGwin (shudders) to SSH into Linux servers, WSL works much better than these solutions because it runs on a real Linux Kernal implementation. Meaning you're running the same Linux distribution as everyone else.

### Clone and run

All the NodeJS and React repositories I've come across on Github only supply utilities for Linux and not Windows. I believe this is because most people are developing on MAC OS now. With WSL I don't need to worry about Windows getting in the way, I clone the repository and fire it up with no dramas most of the time.

### Easily share your code with your MAC pals

At The Big Crunch we are a mix of MAC and Windows. Using WSL means we'll have similar environments, leaving us with far fewer issues than if we were building the system for both Windows and Linux.

### Easily simulate your server environment

Before WSL you would have to run a full blown Virtual machine using Oracle Virtual box or VMWare. Running a VM takes up a lot of your resources because they're dedicated heavy weight environments, not to mention trying to develop in one is a nightmare. WSL is significantly more light weight than a VM, you just fire up the terminal and your away. It doesn't hog resources on your PC and all it's individual processes are managed by Windows, meaning they play well together.

### Have to learn Linux

Windows developers should learn Linux it's great! It took me about 3-4 months before I was proficient enough to be really productive and feel confident. Now I've learnt, Windows Server looks like an ugly beast I don't plan on revisiting. Now that more than 50% of Azure is Linux machines chances are I won't have to look back.

### Cheaper hardware

A new 16" MAC book pro is $4,400 (AUD) while a similar hardware spec Windows HP costs $2,200 (AUD) and if the HP isn't to your liking there's lots of other choice out there.

## What's bad about it

### Paths! ARG

Oof, this has to be the biggest problem I've faced, because Windows drives don't work like Linux drives the WSL team has come up with the solution of putting all your drives at the root directory `/`. For example to access your `C` drive you need to go to the path `/mnt/c/` . This is a generally fine solution until it's not. Docker gets tripped up on it when mounting directories all the time. There is a solution however, you can change your WSL configuration to remove the `/mnt/` and just use `/c/` as suggested by Nick Janetakis in his guide (<https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly).>

When I changed my WSL configuration to remove the `/mnt` prefix NPM failed to unzip freshly downloaded packages as well as Hex (Elixir Package manager).

### Graphics

Running a graphical application from WSL is annoying you need to use a program on windows called `xming` <http://www.straightrunning.com/XmingNotes/> which is a small server that WSL can communicate with to send graphics to your Windows installation. It's not too painful, if you've used CYGwin you are most likely familar with it. The part I found tricky was getting the Elixir performance monitor to display from our EC2 instance on my Windows machine, it's 3 or 4 layers of integration to get it to finally show in Windows and did my head in for a day or two. By the end I was begging for an Elixir performance monitor like `top` which runs in the terminal.

(Image of integration cake)

### Searching your problems is hard

Most of the time when I'm running into an issue in my WSL environment it turns out to be some kind of Ubuntu problem and solution, which is really awesome because it means I learn more about Ubuntu and solve my problem. Sometimes, it's a WSL specific problem and it's not obvious it's a WSL related problem, for example the problem I mentioned above Hex packages wouldn't unzip in my WSL environment after changing my path configuration. I googled the issue profusely finding no resources on the issue. Eventually I found a related Github issue (<https://github.com/hexpm/hex/issues/474)> and posted the solution of removing the `wsl.conf` file.

This is just one example I've run into a few, the fastest way I've found to solve these problems is to find a Github issue with your error message and find the poor soul who has run into your issue on WSL as well.

### Docker is a bit tricky

Docker can't run in WSL because it's a virtual machine / simulation. Running docker in it would be similar running docker in docker. The way it works is the Docker Daemon runs in Windows while you interface with Windows docker via WSL. The way WSL paths works can be a bit of a nightmare here, but overall once it's running you're ok.

The one stop shop for setting up docker in WSL is here - <https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly>

### Moving files and locks

Microsoft don't recommend you modify files you use in WSL in Windows because the two operating systems have two fundamentally different permissions models. But with all rules they are made to be broken, I run VSCode directly in Windows and modify files that my WSL instance is running, compiling and serving. For the most part this is fine, until I use VSCode to move a file or folder, then all hell breaks loose. Windows locks the file in a strange way where WSL or Windows can't access it anymore, meaning you can't commit it to GIT, delete the file or do anything with it. Until you implement the age old solution of turning it off and on again. Now I'm familiar with the issue I encounter it rarely, but when I do it's really frustrating.

(Turning off an on again image)

## Overall

WSL is an amazing addition to Windows and I plan to use it more and more. If I'm starting a new project now I always jump straight into WSL because I know it will be a much better time than if I was using powershell and CMD. I'm looking forward to the new WSL 2, there's some changes I will have to make in my workflow and it resolves some of the issues I've mentioned here.
