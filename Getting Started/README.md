# Getting Started
These pages are to help you get started using Riviera.
They include definitions of common words or terms, instructions on the basics of Linux and Riviera, and much more (eventually)!

Topics to add:
- Common Definitions
- What is a "high-performance compute" (HPC) cluster?
  - How does it differ from a regular computer, or a bunch of regular computers?
- What is Riviera?
  - It's an on-campus cluster
  - Costs
- Fair share usage
  - Storage capacity
- Dos and Don'ts
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
 Setting up the SSH connec
  - Connecting via the terminal
  - Using MobaXTerm, Putty, etc.
  - Reiterate the point of not using an IDE (or using it correctly)
  - Who to contact if you can't log in
- Linux basics
  - Moving around: `cd`, `ls`, `pushd`, `popd`, etc.
  - Editing files: `nano`, `vim`, `emacs`
  - Moving files locally: `cp`, `mv`, `rm`, `mkdir`, `rmdir`
  - Moving files remotely: `scp`, `rsync`, `git`, FileZilla
- The module system
- Link to the "Slurm" category for job submissions, etc.
