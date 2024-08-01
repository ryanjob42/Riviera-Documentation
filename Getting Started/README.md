# Getting Started
These pages are to help you get started using Riviera.
They include definitions of common words or terms, instructions on the basics of Linux and Riviera, and much more (eventually)!

Topics to add:
- Common Definitions
## What is a "high-performance compute" (HPC) cluster?
  - How does it differ from a regular computer, or a bunch of regular computers?
### What is Riviera?
  Riviera is an collection of high end computers CSU has purchased and physcially stored on campus. These computers can range from GPU nodes which can run computationally intensive programs thousands of times faster than your laptop, high memory computers with over 20 times as much RAM as a tpyical desktop, and CPU nodes which are smiliar to the GPU nodes but easier to set up at the cost of performance. **MENTION HOW MANY OF EACH TYPE OF NODE AND MAYBE THE SPECS**. Riviera itself can't be accessed in person like a typical computer so special steps need to be taken in order to use it. Please see [How to Connect](##HowtoConnect) for more detail. Connecting to Riviera is also done through a central computer so no users can access the special computers with SSH, instead you need to use special programs like SLURM which tell the main login computer to send off your program to the computers you specified, please refer to [SLURM](##SLURM) section for more detail.
  - Costs
### Fair share usage
  I don't actually know what this is
### Dos and Don'ts
  - Do: debug your code before running it here
  - Don't: use GUI programs
  - Don't: use IDEs (VSCode, PyCharm, etc.) incorrectly
    - Once pages are made for using them correctly, link them in here.
## How to Connect 
  ### Off Campus
  The first step to accessing Riviera is to make sure your computer can talk to the Riviera's login computer. If you are on campus and connected to the wifi then you're good to go! If not you need to set up and connect to the CSU VPN. Luckily, CSU IT has a very good tutorial with pictures for each step. First, click [here](https://it.colostate.edu/cybersecurity/globalprotect-vpn/#install-agent) to install a program called "Global Protect". Next, setup Global Protect by following the steps [here](https://it.colostate.edu/cybersecurity/globalprotect-vpn/#gp-connect-PC-mac). When you connect to Global Protect, your computer now acts as if it's using CSU's wifi even though you're remote. Now you're ready to talk to the login computer by using an SSH connection mentioned bellow.
 ### Using SSH
 At this point, you're computer should now be able to talk to Riviera! Unfortuantly, this isn't as simple as logging into a CSU on campus computer. Riviera doesn't have what's called a "GUI" so all communication has to be typed messages in what we call a terminal (this process looks like hackers you see on TV). You can think of the terminal like iMessage or WhatsApp, as it will connect you with Riviera and allow for sending and recieving messages. To use the terminal for SSH connection please refer to [this tutorial](https://www.tomshardware.com/how-to/use-ssh-connect-to-remote-computer). While the tutorial mentioned references "smartipi" and "pi@raspberrypi.local" please instaed use "usesrname@riviera.colostate.edu" where username is the name provided by the person managing the riviera computer. If you forget this username, please reachout to them.
 To make sure things are running properly please type "passwd" and press enter. This message which we call a command is what will allow you to change the complex randomly generated password into one of your choosing.
 One limitation of the terminal is that you can only interact through messages making things like file transfer a complex task but luckily there are very simple work arounds mentioned later in the documentation.
 If you are interesting in using an IDE (like VSCode or PyCharm) to connect to Riviera, **DON'T**. These programs in the background cause massive problems that can prevent/lag the entire system for every user. 
## Linux basics
  - Moving around: `cd`, `ls`, `pushd`, `popd`, etc.
  - Editing files: `nano`, `vim`, `emacs`
  - Moving files locally: `cp`, `mv`, `rm`, `mkdir`, `rmdir`
  - Moving files remotely: `scp`, `rsync`, `git`, FileZilla
## SLURM
## The module system
- Link to the "Slurm" category for job submissions, etc.
