# Getting Started
These pages are to help you get started using Riviera.
They include definitions of common words or terms, instructions on the basics of Linux and Riviera, and much more (eventually)!

Topics to add:
- Common Definitions
## What is a "high-performance compute" (HPC) cluster?
  - How does it differ from a regular computer, or a bunch of regular computers?
### What is Riviera?
  Riviera is an collection of high end computers CSU has purchased and physcially stored on campus. These computers can range from GPU nodes which can run computationally intensive programs thousands of times faster than your laptop, high memory computers with over 20 times as much RAM as a tpyical desktop, and CPU nodes which are smiliar to the GPU nodes but easier to set up at the cost of performance. **MENTION HOW MANY OF EACH TYPE OF NODE AND MAYBE THE SPECS**. Riviera itself can't be accessed in person like a typical computer so special steps need to be taken in order to use it. Please see [How to Connect](#how-to-connect) for more detail. Connecting to Riviera is also done through a central computer so no users can access the special computers with SSH, instead you need to use special programs like SLURM which tell the main login computer to send off your program to the computers you specified, please refer to [SLURM](#slurm) section for more detail.
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

## File Downloading and Uploading

## Linux Basic Commands
### Moving Around
- `cd`: Change Directory. This command is used to navigate between directories. For example, `cd Documents` will move you to the Documents directory.
- `ls`: List. This command lists all files and directories in the current directory.
- `pushd`: Push Directory. This command is used to save the current directory so you can return to it later. For example, `pushd Documents` will save the current directory and move you to the Documents directory.
- `popd`: Pop Directory. This command returns you to the directory saved by the pushd command.
- `pwd`: Print Working Directory. This command displays the current directory you’re in.
### Editing Files
- `nano`: Nano is a simple and intuitive text editor for beginners. It’s easy to use and has a help menu at the bottom of the screen. To save a file in nano, you can use Ctrl+O and then hit Enter to confirm. To exit nano, you can use Ctrl+X.
- `vim`: Vim is a powerful and efficient text editor, but it can be a bit difficult for beginners. It has two modes: command mode and insert mode. When you first open a file with vim, you’re in command mode. To switch to insert mode and start editing the file, press i. To save changes and stay in vim, press Esc to switch back to command mode, then type :w and hit Enter. To save changes and exit vim, type :wq in command mode and hit Enter. If you want to exit without saving changes, type :q! and hit Enter.
- `emacs`: Emacs is a highly customizable text editor with a steep learning curve. It uses combinations of Ctrl and Alt (labeled as C and M respectively in emacs documentation) with other keys for commands. To start editing a file, just start typing. To save a file in emacs, you can use Ctrl+X Ctrl+S. To exit emacs, you can use Ctrl+X Ctrl+C.
- `cat`: This command is used to display the contents of a file. It’s useful for quickly viewing small files.
- `less`: This command is used to view the contents of a file one page at a time. It’s useful for viewing large files.
- `head`: This command is used to display the first part of files.
- `tail`: This command is used to display the last part of files.
### Moving Files Locally
- `cp`: Copy. This command is used to copy files or directories. For example, `cp file1 file2` will create a copy of file1 and name it file2.
- `mv`: Move. This command is used to move or rename files or directories. For example, `mv file1 file2` will rename file1 to file2.
- `rm`: Remove. This command is used to delete files. For example, `rm file1` will delete file1.
- `mkdir`: Make Directory. This command is used to create a new directory. For example, `mkdir new_directory` will create a new directory named new_directory.
- `rmdir`: Remove Directory. This command is used to delete a directory. For example, `rmdir directory` will delete the directory named directory.
- `touch`: This command is used to create a new empty file.
- `ln`: This command is used to create a link between files.

## SLURM
As you may have noticed, users of Riviera can only connect to what we call the "login node". You can think of this as the central computer that acts as a bridge between you and the computing resources. You can directly ssh into the login node but not any other node. In order to use the other nodes, a job manager called SLURM is used. This program manages all the jobs people run and prevents competing for resources. It will automatically pick which node for you to use and if all are busy, it will put you in line and run your program as soon as it can without any input so you can walk away and grab a coffee! Using this program however can be a challenge at first. Also, please note that code should never be run on the login node, this is the node all users are connecting to so if you slow it down, the over 100 users on Riviera will also be impacted. 
The first step to using SLURM is to load it, to do so simple run `module load slurm`. Now you can run `squeue` to see the current jobs running and the waitlist. You can also run `sinfo` to see the partitions (these are all the ways you can run your script ranging from short run on a GPU to week long on a high ram computer). Here is a basic SLURM script:
```
#!/bin/bash
#SBATCH --job-name=NAME
#SBATCH --output=out
#SBATCH --error=err
#SBATCH --partition=PARTITION
python main.py
```

- `NAME` will let you choose what your job is called. You and all users can see this by running `squeue`. If you're running multiple jobs the name will let you easily distinguish between them
- `PARTITION` specifies the type of computer you want to use and how long. Running `sinfo` will show you all the options but as of the time of writting these are the current options (for example if you wanted short GPU session replace #SBATCH --partition=PARTITION     with     #SBATCH --partition=short-gpu) :
  
day-long-highmem    1 day

short-cpu           2 hours

short-gpu           2 hours

short-highmem       2 hours

week-long-cpu       7 days

week-long-cpu       7 days

week-long-gpu       7 days

week-long-highmem   7 days

day-long-cpu        1 day

day-long-cpu        1 day

day-long-gpu        1 day


## The module system
- Link to the "Slurm" category for job submissions, etc.
