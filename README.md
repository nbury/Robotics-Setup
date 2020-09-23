# Robotics-Setup
Hi everyone!
This repo is going to be for helping everyone setup a virtual machine with ROS installed, as well as a few other things to help us in the future.\
(If you already have an Ubuntu 18.04 VM go ahead and skip to ROS setup)\
This will be different for Users, so follow the appropriate instructions.

# VM Setup

## Windows
For windows, we can use Windows Subystem for Linux 2 (WSL2).\
Go ahead and download ubuntu 18.04 LTS from the Microsoft Store.\
If this is the first time setting up a VM you'll have to change a few settings.
There's a tutorial on how to do this [here](https://docs.microsoft.com/en-us/windows/wsl/install-win10)\
Go ahead and turn it on, and make sure you can see the terminal.

WSL2 only allows for terminal use, but we need to allow programs to run in their own windows, so we'll use a program called [VcxSrv](https://sourceforge.net/projects/vcxsrv/)\
Download and install this, then launch the app, which will be called XLauch now.\
Stick with the default settings except for the box 'Native OpenGL' which you should turn off. (This is in the extra settings box)\
After that run this code in your linux terminal to let it connect to VcxSrv
```
echo "export DISPLAY=:0" >> ~/.bashrc
source ~/.bashrc
```
Now you should be all set to install ROS

## Mac
(Please note I don't have a Mac and don't know much about them so I'm kinda just following others here)\
For windows we're going to use Virtualbox 6.1\
Go ahead and download install from [here](https://www.virtualbox.org/wiki/Downloads)\
Then run the application, and create a new VM by clicking the add button\
We'll be using Ubuntu 18.04 LTS\
You can keep the default settings for RAM, CPU etc, just don't allocate more than half your system resources.\
You will need to create a virtual hard disk to store the data on. When that comes up, select that option, and allocate 20GB or so.\
Then boot into the VM and go through the OS setup, and you should be all set.

# Setting up ROS
First we have to connect to the ROS repos, this is done by running there commands:
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```
Now lets get any updates for any other services that ROS may depend on.
```
sudo apt update
sudo apt upgrade
```
Finally, lets install ROS, Windows may ask for administrator permissions during this.
**THIS MAY TAKE LIKE 15 MINUTES**
```
sudo apt install ros-melodic-desktop-full
```
We also need to install a few dependencies
```
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```
Once that is done, lets test our setup by starting a ROS environment and booting into Gazebo.
```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
This adds all the ROS environment variables to your terminal.\
Finally, we can start ROS.\
This should open a gazebo window with an empty world and a small robot
```
gazebo worlds/pioneer2dx.world
```
If that doesn't work try running this in your current terminal
```
gzserver worlds/pioneer2dx.world
```
And this in a new terminal
```
gzclient
```
Now we know Gazebo is all set!

Lets now get a ROS package to help us work with underwater ROVs
```
sudo apt install ros-melodic-uuv-simulator
```
And let's test this out too
```
roslaunch uuv_gazebo_worlds empty_underwater_world.launch
```
This should open an empty world, but this time with an ocean.

Congrats! ROS is now all set up


# Useful Links
[ROS Melodic tutorials](http://wiki.ros.org/ROS/Tutorials)\
[Gazebo Tutorials](http://gazebosim.org/tutorials)\
[Virtualbox installation guide](https://www.virtualbox.org/manual/ch01.html#gui-createvm)\
[Underwater Unmanned Vehicles (UUV) Simuator Docs](https://uuvsimulator.github.io/)\
[Medium Blog on setting up ROS on windows](https://medium.com/fresnostatedx/ros-environment-setup-for-windows-without-virtualbox-8fc14faad59e#:~:text=In%20order%20to%20run%20any,apps%20directly%20from%20Ubuntu%20WSL.&text=Note%3A%20Make%20sure%20you%20start,GUI%20apps%20from%20Ubuntu%20WSL.)
