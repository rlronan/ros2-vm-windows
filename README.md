# Instructions for installing Robot Operating System 2 Foxy Distribtuion (Ros2-Foxy) inside a virtual machine, inside of Windows 10. 

These instructions are for Windows 10. They should _probably_ work on a Mac, but I have not tested. If you are installing on a Mac and run into the Virtualbox "kernel driver not installed (rc=-1908)" error, see the bottom of this page.

## Install Oracle VM VirtualBox Manager
You will need VirtualBox to run your virtual machines inside of Windows. Windows 10 now includes native suport for running a Linux VM inside of Windows through the Microsoft Store but there are still issues with networking and GUIs; so we will use VirtualBox.

Download VirtualBox: https://www.virtualbox.org/wiki/Downloads
Click on "windows hosts" --> save file --> then find the file and run it. Follow the installation instructions.


## Download an Ubuntu Desktop
Download the most recent Ubuntu version _and do not extract the content._
Simply save the downloaded file. 
(It should be Ubuntu 20.xx.yy.z LTS) https://ubuntu.com/download/desktop

## Install Ubuntu in a virtual machine
Follow the instructions in the following link to create a new VM and install the ubuntu iso.
In order to install and use Ros2-Foxy, you will **likely need at least 30gb** of space dedicated to the virtual machine. If you run out of space in your VM you will need to repeat the process, or delete things inside your VM. (It is possible to enlarge the VM if it is dynamically allocated, but it can be a hassle). 

I reccommend you **do not** check "don't show this message again" in the information box that pops up when you run a virtual machine. 

On windows, you will have to click (by default) the right ctrl button on your keyboard to 'escape' the virtual box in some cases. Depending on your settings, you may just be able to click outside of the virtual box, but if that doesn't work you will have to hit the right ctrl button on your keyboard in order to be able to move your mouse outside of the VM, and type outside of the VM. 

You can change the number of processors, the video memory, and the amount of RAM allocated to the VM after the install by selecting your Ubuntu VM in VM VirtualVox Manager and clicking settings. 

Instructions for creating an ubuntu VM: https://brb.nci.nih.gov/seqtools/installUbuntu.html

If you get an error about Virtualization when trying to start the VM, try the following: 
https://www.howtogeek.com/213795/how-to-enable-intel-vt-x-in-your-computers-bios-or-uefi-firmware/


## Working inside of the Virtual Machine
In order to use Ros2-Foxy, you will need to set up a couple of things. 
All of these are done inside your virtual machine, not in your windows operating system

(If you cannot copy and past from your host machine (Windows) to your guest (Ubuntu), make sure you have configured bidirectional copying for the 

### Install and configure Git
1. Open a terminal ( you can do this by right-clicking on the desktop and clicking "open terminal here", or by typing "terminal" in the search bar).
2. In the terminal run the following commands with your own username and email (keep the quotation marks): 
3. `sudo apt-get update`
4. `sudo apt install git-all`
5. `git config --global user.name "Your User Name"`
6. `git config --global user.email "Your email"`
7. `git version`

### Install and configure Docker
1. Open a terminal
2. run the following commands:
3. `sudo apt-get update`
4. `sudo apt-get install \`
    `apt-transport-https \`
    `ca-certificates \`
    `curl \`
    `gnupg \`
    `lsb-release`
5. `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`
6. `echo \`
  `"deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`
7. `sudo apt-get update`
8. `sudo apt-get install docker-ce docker-ce-cli containerd.io`



### Install and configure Ros2-Foxy
Follow the instructions to install and setup Ros2-Foxy in your Ubuntu VM:
You will need to open a terminal again, or use the same terminal as before.
https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html

Make sure you proceed to the Configuring your ROS 2 environment page after your install:

https://docs.ros.org/en/foxy/Tutorials/Configuring-ROS2-Environment.html


### Install additional depedencies
The instructions for these installs can be found in the tutorials, but you can install them straight away.
1. Open a terminal ( you can do this by right-clicking on the desktop and clicking "open terminal here", or by typing "terminal" in the search bar).
2. In the terminal run the commands from the next two sections:

#### Install Colcon
1. `sudo apt install python3-colcon-common-extensions`

#### Install Rosdep
1. `sudo apt-get install python3-rosdep`
2. Needs to be called only once after installation: `sudo rosdep init`
3. Needs to be called at least once or when updating (there might be new needed definitions your local installation of rosdep doesn't know about yet): **Do NOT run rosdep update with sudo**. It is not required and will result in permission errors later on. `rosdep update`


## Continue with the Ros2-Foxy tutorials:
https://docs.ros.org/en/foxy/Tutorials/Turtlesim/Introducing-Turtlesim.html#turtlesim


## Mac Kernel driver not installed error
If you are installing on a Mac and run into the Virtualbox "kernel driver not installed (rc=-1908)" error, see the bottom of this page. it may be resolvable by doing the following From a **comment** on this post https://medium.com/@Aenon/mac-virtualbox-kernel-driver-error-df39e7e10cd8:

"It’s not necessary to reinstall VirtualBox in order to resolve this problem. As described in the VirtualBox forum for macOS hosts, you can do the following instead:
Restart your machine and enter Recovery Mode (Press and hold ⌘-R on reboot.)
Open the Terminal.
Type the following: spctl kext-consent add VB5E2TV963
Press Enter.
Restart your machine."
