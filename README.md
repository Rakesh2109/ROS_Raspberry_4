# ROS_Raspberry_PI4
Capture measurements from the thermal camera, RGB camera, and mmWave radar using ROS 

# ROS Noetic Installation and Setup on Raspberry Pi 4

This repository contains a script to help you set up Ubuntu 20.04 on a Raspberry Pi 4, connect to the internet, install ROS Noetic, and create a ROS workspace.

## Prerequisites

- **Raspberry Pi 4**: Ensure you have a Raspberry Pi 4 with at least a 16GB microSD card.
- **Ubuntu 20.04 Server OS**: You must install Ubuntu 20.04 server os on your Raspberry Pi 4 using the [Raspberry Pi Imager tool.](raspberrypi.com/software/)


## Connection to the Internet via Ethernet.
The following commands are to followed every time
```bash
sudo ip link set eth0 up
sudo dhclient eth0
sudo netplan apply
```


## Follow the Prompts to the Ubuntu desktop

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install ubuntu-desktop -y
```
# Software installation




## ROS Installation 

After installing Ubuntu 20.04 on the Raspberry Pi 4, we installed the ROS Noetic operating system. We chose ROS because it allows for simultaneous measurements without creating additional lags or delays. Moreover, ROS is easy to configure and allows for seamless integration of additional sensors.

Please note that we installed ROS Noetic as this is the version compatible with Ubuntu 20.04.

We followed the installation steps of ROS Noetic which can be found in the following link:  
[ROS Noetic Installation on Ubuntu 20.04](https://wiki.ros.org/noetic/Installation/Ubuntu)

## Create a ROS Workspace

Before you start writing code in ROS, you need to create a workspace. A workspace is a set of directories (or folders) where you store related pieces of ROS code. The official name for workspaces in ROS is catkin workspaces.

We followed the installation steps to create a ROS workspace which can be found in the following link:  
[ROS Workspace](https://automaticaddison.com/how-to-create-a-ros-workspace/)

## RGB camera (Pi camera)
To install a package that requires C and V4L2 (Video for Linux 2) libraries on a Linux system using the below commands

```bash
sudo apt-get install autotools-dev autoconf build-essential
sudo apt-get install libv4l-dev v4l-utils
```

## Instructions to Download, Unzip, and Move Files
Download the zip file by clicking on the Code button and selecting Download ZIP.
Once the zip file is downloaded, you need to unzip it
After unzipping, move the contents to your `<workspace dir>/src`: directory

Note: In `<workspace dir>/src` you must have four folder such as capra_thermal_cam-master; serial; ti_mmwave_rospkg; and usb_cam. 

Next copy the `<workspace dir>/src/capra_thermal_cam-master/udev` file in your /etc/udev/rules.d/ folder.

Go back to `<workspace dir>`:

```bash
catkin_make && source devel/setup.bash
echo "source <workspace_dir>/devel/setup.bash" >> ~/.bashrc
```

Enable command and data ports on Linux:

```bash
sudo chmod 666 /dev/tty*
```
### Raspi-Config Installation : ###

```bash
apt-get install libnewt0.52 whiptail parted triggerhappy lua5.1 alsa-utils -y

wget https://archive.raspberrypi.org/debian/pool/main/r/raspi-config/raspi-config_20180406+1_all.deb -P /tmp

sudo dpkg -i /tmp/raspi-config_20180406+1_all.deb 
```
### For USB camera to work properly
   	
dit your /boot/config.txt file and make sure the following lines look like this:
```
start_x=1             # essential
gpu_mem=128           # at least, or maybe more if you wish
```

## To launch radar 

## Launch the thermal cam 

```bash
roslaunch capra_thermal_cam capra_thermal_cam.launch
```




