## Goal

The goal of this project is to automatically apply and update all of the various changes needed to make Linux work properly on the GPD Pocket.

###### Supported Linux Distributions
- Arch-based distributions (ArchLinux, Manjaro, etc.)
- Debian-based distributions (Debian, Kali, Mint, Ubuntu, etc.)
- Fedora-based distributions (experimental - could really use some feedback!)
- Gentoo-based distributions (Funtoo, Gentoo, etc.)

## Install

###### Bootstrap ISO

1.) Setup a Linux environment (Virtualbox + Ubuntu LiveCD is a quick option.) An existing Linux install using any of the above listed distros will work also.

2.) Download your ISO to this Linux machine - you can do this using: `wget http://url.here/file.iso`

3.) Run the following to build the ISO (replacing ISO_FILENAME with the actual name of the file.)

    git clone https://github.com/cawilliamson/ansible-gpdpocket.git
    cd ansible-gpdpocket
    bash bootstrap-iso.sh ISO_FILENAME

4.) Write the file to USB by running the following (replacing USB_DEVICE with the actual device path for your USB drive):

    fdisk -l /dev/sd* # find the disk ID of your USB drive and use in command below.
    dd bs=1m if=~/bootstrap.iso of=USB_DEVICE

5.) Boot your GPD Pocket using the USB drive and you should have a completely working installer for your distribution of choice.

###### Bootstrap Installed System

In order to install my Ansible playbooks please complete the following steps:

1.) Start by downloading the latest ZIP of my ansible playbooks from:

https://github.com/cawilliamson/ansible-gpdpocket/archive/master.zip

2.) Copy this file to a USB drive and insert that drive in to the GPD Pocket

3.) Mount the USB drive somewhere (`mount /dev/sda1 /mnt` for example)

4.) Using `cd` navigate to that new directory (for example, `cd /mnt`)

5.) Run the following command:

`sudo bash bootstrap-system.sh`

## Update system after install

1.) Run `sudo gpd-update`

2.) Reboot if any changes were made to ensure they get applied properly.

## Status

###### Broken

- Distorted audio ( kernel bug - https://bugzilla.kernel.org/show_bug.cgi?id=196351 )
- USB-C Data Connectivity
- When installing from a Debian-based distro you will likely be told that modules cannot be loaded and asked if you wish to continue anyway. Select 'Yes' and you will be able to continue the installation without any problems. This is due to the fact that we are patching in a different kernel to an existing initrd image.

###### Working

- Accelerated Video
- Audio
- Battery manager
- Bluetooth
- Display brightness
- Display rotation
- Suspend (sleep/wake)
- Thermal control
- Touchscreen
- Wi-Fi

## Made possible by...

- efluffy at https://github.com/efluffy/gpdfand - great work on actually getting the fans in this thing to work.
- hansdegoede at http://hansdegoede.livejournal.com/17445.html - absolutely EVERYTHING related to the kernel was this guy.
- linuxiumcomau at http://linuxiumcomau.blogspot.com/ - inspired my work on bootstrapping install isos.
- stockmind at https://github.com/stockmind/gpd-pocket-ubuntu-respin - various code contributions and ideas.

## Donation
If this project helped you - feel free to buy me a coffee (I could sure use one!)

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=JGZUV7JA5A44E)