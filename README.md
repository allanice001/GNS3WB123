# GNS3WB123
GNS3 WorkBench 12.3 Linux Self-serve Installation Instructions

Supported Platforms
===================

Linux Mint 17.0 32bit - highly recommended

Ubuntu 14.04 32bit    - recommended

Linux Mint 17.0 64bit - Has issues with qemu

Ubuntu 14.04 32bit    - Has issues with qemu


Download Instructions
=====================

The only file you NEED to download to install GNS3 WorkBench on your Linux install is installGNS3WB.tar.gz.  Unpack all the files in this archive to a directory and from that directory run
./installGNS3WB.sh

The installGNS3WB.sh script will download the other two files (GNS3WBFilePackage.tgz and VBVMsFilePackage.tgz) during the install. However, these files could be downloaded independently and saved to your $HOME directory - if found there, the installer (in interactive mode) will ask if you want to download them again at the appropriate stage.

Files
=====

installGNS3WB.tar.gz   Contains:
                       * installGNS3WB.sh
                         An install script to install GNS3 WorkBench on Linux
                         (Linux Mint 17.0 32bit recommended)
                       * installGNS3WB.components.sh  
                         Used by installGNS3WB.sh 
                       * installGNS3WB.help
                         Help file for the install script (installGNS3WB.sh)
                       * installGNS3B.readmeLinuxSelfServe.txt
                         This file

GNS3WBFilePackage.tgz: All the GNS3 WorkBench and GNS3 Vault projects, plus the 
                       scripts other bits that make GNS3 WorkBench tick
                       For a fulllist of files contained here, see
                       ~/GNS3/WorkBench/Scripts/Administrative/WBFilePackageFiles.txt

VBVMsFilePackage.tgz:  is a collection of Oracle VirtualBox Virtual Machines:
                       Linux Microcore 3.8.2 (base for Linux1)                      
                       Linux1 (a linked clone of Linux Microcore 3.8.2)
                       Linux Microcore 4.0.2 (base for Linux2)                      
                       Linux1 (a linked clone of Linux Microcore 4.0.2)
                       Vyatta (Base for Vyatta1 & Vyatta2)
                       Vyatta1 (a linked clone of Vyatta)
                       Vyatta2 (a linked clone of Vyatta)
                       Note: The username/password required for the Vyatta 
                       routers is vyatta/vyatta123
                       see 
                       ~/GNS3/WorkBench/Scripts/Administrative/VBFilePackageFiles.txt


Prerequisites:
==============

Before you can even begin to get GNS3 WorkBench (self-serve version) installed you will need three elements:

1. A Virtual Machine Hypervisor (VMware recommended) in which you create a Virtual Machine and install Linux.
2. An image for the version of Linux you wish to install on your VM. Linux Mint 17.0 32bit or Ubuntu 14.04 32bit are the only Linux versions fully tested successfully at this stage.
3. Images for a Cisco IOS routers, ASA and Juniper routers.

If you don't have a copy of a Cisco IOS, you will still be able to use GNS3 WorkBench, but you will be restricted to the ONE routing lab that you could run using a Vyetta image - which you can then use as a model to create more labs of your own.

But ideally, before you start you will have copies of:

c3725-adventerprisek9-mz.124-15.T10.bin [to run Cisco routers - this is the only image you need for MOST labs and exercises]
c3640-ik9o3s-mz.124-25a.bin [to run GNS3 Vault exercises]
c7200-adventerprisek9-mz.150-1.M.bin [to run some GNS3 Vault exercises]
asa842-k8.bin [to run Cisco Adaptive Security Appliances]
jinstall-9.6R1.13-domestic-signed.tgz [to run Juniper Junos]

You will also need to have a Virtual Machine Hypervisor.  I have VMware Fusion v5.0, but the steps will be similar for other versions.  Virtual Box may work.

You will need to have downloaded a suitable Linux image - I used Linux Mint 17.0 Cinnamon 32 bit.  Other Debian/Ubuntu based images that use the ".deb" package distribution method should also be suitable, but Linux versions that use ".rpm" package distribution will not be able to run the install script.

The total install time is considerable, especially if your Internet connection is slow.  My best download speed is about 3Mb/s, and I estimate it would take me approximately two hours to two and a half hours to complete the FULL install from scratch - after you have your hypervisor installed and images downloaded.

Task 1 - Create your VM
-----------------------

Create a new virtual machine in the normal way (detailed steps for creating a VM using VMware Fusion follow), making sure that you:
1. Give the VM 40GB HD space
2. Allocate as much free RAM as you can spare on your setup
3. Give the VM 2 Network Interface cards, make sure the first one is mapped to your physical Ethernet adapter, the second as a shared connection with the host computer.   Be careful, by default, the first adapter will be configured as a shared connection with the host computer too.
4. [Optional] You probably won't need sound - so you can remove the sound card if you want to save on resources.
5. [Optional] You will probably want to add some shared folders if you already have files on your host computer that you wish to copy to your VM - like the files listed above - although you may have trouble getting shared folders to work, especially on Linux Mint.

Walkthrough of Task 1 using VMware Fusion 5.01
..............................................

In VMware Fusion, select File | New
Click Continue without disc
Click Choose a disc or disc image- then select the Linux image you wish to use.  Click Continue.
When prompted for Operating System and Version, I left them at the default Linux and Ubuntu, because Linux Mint is based on Debian and Ubuntu.  Click Continue

IMPORTANT:
Click Customize Settings.  You will be prompted to save your VM and give it a name. I called mine LinuxMint170Cinnamon.vmwarevm
Now change the following settings:
Processors and Memory: Give it a much RAM as you can spare.  I Have 16GB so I gave it 8GB (8192 MB) and two processor cores. If you want to add any advanced options like Enable hypervisor applications on this machine so you can run Linux KVM, then do that here too.
Network Adapter: Change the network adapter to Ethernet
Hard Disk: Change the size of the hard disk to at least 40GB
Add a device and add a Network Adapter and Share with the host machine.
[Optional] Sound Card: Click Remove Sound Card
[Optional] Sharing: Turn Shared Folders on, and add the folders from your host that you wish to share.  Unfortunately, shared folders doesn't always work - especially on Linux Mint 

Close the system preferences, and you will see that you have a new virtual machine. Mine is called LinuxMint170Cinnamon because that is the name I chose earlier.

Task 2 - Install Linux [Allow 60 min]
-------------------------------------

In this stage, you complete the Linux install on your VM. The following walkthrough should guide you.

Walkthrough of Task 2 using VMware Fusion 5.01
..............................................

Boot your VM, and as your machine boots, hit the F2 key to go into the BIOS Setup Utility and set the state of the Legacy Diskette A: to Disabled.  Press F10 to save and exit. 

When you VM boots, go through the normal Linux install - set your keyboard, country, computer's name etc and make sure you have a user called user - this is how I set mine up:

Once the install is finished, shut down your machine.

Back in the VMware application interface, add some descriptive comments to your VM.  I wrote:
Linux Mint 16.0 Cinnamon.  No VMware Tools installed, no updates installed.

Task 3 - Update Linux and install VMware tools
----------------------------------------------

Before you start using your VM, you need to install VMware Tools.  However, sometimes the install of VMware Tools fails, especially if you want to use the Shared Folders feature on Ubuntu or Mint. So at this point, I recommend that you make a copy of your VM - I did my copy by copying LinuxMint170Cinnamon.vmwarevm and renamed it GNS3WB86.vmwarevm  and then complete this stage using the copy.

Walkthrough of Task 3 using VMware Fusion 5.01 and Linux Mint 17.0
..................................................................

Boot up your copied VM - you will get a dialogue from VMware where you can tell VMware that you copied this VM by clicking on I copied it when prompted.

As the VM is booting, you will notice in your VM Library that you now have two VMs called LinuxMint170Cinnamon.  Now is a great time to rename this copied machine to something a bit more manageable - I renamed mine to GNS3WB86.  This gives a more specific name to you VM, but leaves the files on my HDD inside the GNS3WB86.vmwarevm package with names like LinuxMint170Cinnamon.xxx reflecting the original OS.

Once the VM is booted, check that your OS is up to date - in Linux Mint 16.0 Cinnamon, I did this by running the Update Manager (search for it if you can't find it).  It might take 20 minutes or more to complete all the updates (it did on my system).

You can now begin the job of installing VMware tools.  If you are a little paranoid, you may even wish to take another copy of your VM after doing the updates and before installing VMware Tools - just in case you have to start again and want to save the time it takes to install the updates.

To install VMware Tools, choose Virtual Machine | Install VMware Tools from the VMware Fusion menus.  You will see a CD/DVD open with a file called VMwareTools-9.2.2-893683.tar.gz or similar.  Open this file (double-click on it) and inside you will find a folder called vmware-tools-distrib.   Extract this folder to your /tmp directory.

To complete the VMware tools install, you will have to use the command line.  Right-click on the desktop and choose Open in terminal.  A terminal session will open and you will be at the Desktop directory.  First up, change the terminal settings so you have unlimited scrollback (this is a long install script - you may want to scroll back to check for errors).  In your terminal window, choose Edit | Profile Preferences (if you don't have a menu, try right-clicking in the middle of the terminal and selecting Show Menubar).  On the [Scrolling] tab, check the [x] Unlimited option for Scrollback:

Issue a command cd /tmp/vmware-tools-distrib/ to change directory, then issue the command sudo ./vmware-install.pl -d to install vmware tools - you will be prompted for your password.

cd /tmp/vmware-tools-distrib/
sudo ./vmware-install.pl -d

Once VMware tools is installed, you should be able to run the VM in full screen mode, but first, there is some cleaning up to do:

* Exit the terminal session and any open file browsers
* Eject the VMware Tools DVD
* Shutdown your VM

This is also another good place where you might want to take another copy of your VM.

Task 4 -  Prepare Linux image with OS files
-------------------------------------------

Make sure you have the firmware images that will make GNS3 WorkBench run - in other words you need the following files copied to your VM:

* At least one IOS image.  Ideally, this will be c3725-adventerprisek9-mz.124-15.T10.image in the /home/user/GNS3/images/IOS directory.  Create the directory structure as you go.
* If you intend to run the GNS3 Vault exercises, make sure you also have copies of c3640-ik9o3s-mz.124-25a.image and c7200-adventerprisek9-mz.150-1.M.image in the /home/user/GNS3/images/IOS directory.
* If you intend to run ASA labs, make sure you also have a copy of asa842-k8.bin in the /home/user/GNS3/images/QEMU/ASA directory.  Create the directory first.
* If you intend to run Juniper Junos, make sure you have a Junos image.  This install has been tested with jinstall-9.6R1.13-domestic-signed.tgz.  Make sure you have this file or another Juniper Junos image in the same format.
* This image needs to be placed in the /home/user/GNS3/images/QEMU/Junos directory.  Create the directory first.

Walkthrough of Task 4
.....................

Your Cisco router images need to be in a specific directory, so start by creating the directory structure to hold the images.  The following commands will create all the directories you need to complete this task.

mkdir /home/user/GNS3/images
mkdir /home/user/GNS3/images/QEMU
mkdir /home/user/GNS3/images/QEMU/ASA
mkdir /home/user/GNS3/images/QEMU/Junos

To download the Cisco IOS images, do a Google search for the image name - such as c3725-adventerprisek9-mz.124-15.T10.bin.  You should see a link to the Cisco website where you can download the image (provided you have a valid maintenance contract for a Cisco c3725).

Once downloaded, move the image to /home/user/GNS3/images/IOS.  Next decompress the image, giving it a .image extension.  The commands to do this are:
cd /home/user/GNS3/Images
unzip -p c3725-adventerprisek9-mz.124-15.T10.bin > c3725-adventerprisek9-mz.124-15.T10.image

Similarly, download and decompress c3640-ik9o3s-mz.124-25a.bin and c7200-adventerprisek9-mz.150-1.M.bin to c3640-ik9o3s-mz.124-25a.image and c7200-adventerprisek9-mz.150-1.M.image.

The ASA image MUST NOT be decompressed.  Find asa842-k8.bin and move it to the /home/user/GNS3/images/QEMU/ASA directory.

A Google search for jinstall-9.6R1.13-domestic-signed.tgz may not give you a link to the Juniper website where you can download the image.  Instead, you may have to visit http://www.juniper.net/support/downloads/junos.html - but you may find that you'll have to get a later version than 9.6R1.13 - which may or may not work.

Once you have downloaded jinstall-9.6R1.13-domestic-signed.tgz, move it to the /home/user/GNS3/Images/Junos directory and the install script will take you through the image preparation.

Task 5 -  Run the GNS3WB install script [Allow 90 mins]
-------------------------------------------------------

This task is executed in your Linux Virtual Machine, and is really the part that makes GNS3 WorkBench more than just another GNS3 install.

Walkthrough of Task 5
.....................

Working in your VM, download the GNS3WB install script form http://sourceforge.net/projects/gns3workbench/files/v12.3/installGNS3WB.sh and save it in your home directory.  Probably the easiest way to do this is to open a terminal session and enter the following commands

cd ~
wget -O installGNS3WB.sh \ http://sourceforge.net/projects/gns3workbench/files/v12.3/installGNS3WB.sh/download

You'll have to make the script executable, so use the chmod command to do that like this:

chmod +x installGNS3WB.sh

Now you need to run the install script as superuser, so the command is:

sudo ./installGNS3WB.sh

The install script carries out the following tasks:

* Updates your Linux OS with the latest patches and adds the repository where GNS3 resides.
* Downloads and installs the scripts to enable support for ASA and Juniper
* If you have downloaded the ASA image, it will be prepared for use in GNS3
* Downloads and installs the following:
o NIO tap adapter
o Qemu
o open-ssh server
o CPU Limit utility
o Oracle VirtualBox emulator
o Wireshark
o terminal applications Xterm, PuTTY and Konsole
o dynamips
o GNS3
o the Virtual PC Simulator (VPCS)
o a specially prepared Qemu freeBSD image for use with Juniper routers
* if you have Juniper image available, the script then takes you through the tedious Juniper install process.
* Downloads a collection of Virtual Box VMs that are used in the GNS3 WorkBench
* Downloads the GNS3 WorkBench exercises and sets up the default settings in GNS3 and your desktop
* Fixes file permissions so you can run the labs smoothly

Task 6 -  Tweak the user interface ? optional
---------------------------------------------

I made the following changes to the environment to suit me - you may wish to follow suit.

gedit.
......

Edit | Preferences | [View] tab
- Right Margin [x] Display right margin .. at column [85]

To allow gedit to open all files;
1. Create a file called /home/user/.local/share/nemo/actions/openwithgedit.nemo_action
2. Put the following text
[Nemo Action]
Name=Open with gedit
Comment=Open shellscript for editing
Exec=gedit %F
Icon-Name=gedit-icon$
Selection=S
Extensions=any

3. Ref: https://wiki.archlinux.org/index.php/Nemo
https://wiki.archlinux.org/index.php/Nemo


Network Connections
...................

Menu | Preferences | Network Connections
Rename the connections eth0 and eth1 as appropriate

Terminal 
........

(If there is no Menubar, right-click inside the terminal window and select Show Menubar)
Edit | Profile Preferences | [Scrolling] tab
- Scrollback: [x] Unlimited
Edit | Profile Preferences | [Background] tab
(x) Transparent background (approx 75%)
Edit | Profile Preferences | [Colours] tab
[ ] Use colours from the system theme
Built-in schemes: [Custom]	
Text colour: White
Bold colour: Orange
Background colour: Custom: #3f3f3f
Palette
Built-in schemes: Tango
Before you close, you may wish to also set the following recommended tweaks on the [General] tab: check the [x] Allow bold text option and the [x] Show menubar by default in new terminals

Nemo File manager
.................

Edit | Preferences | [Behavior] > Executable Text Files
(o) Run executable text files when they are opened
