# JetBot Setup Guide

Návod na inštaláciu softvérového vybavenia pre JetBot na Jetson Nano.

## Aktualizácia systému

```bash
sudo apt update
sudo apt upgrade
```

## Inštalácia ROS Melodic

Pridanie repozitárov a inštalácia ROS:

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt install curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt update
sudo apt install ros-melodic-desktop-full
```

Automatické načítanie ROS:

```bash
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## ROS nástroje a závislosti

```bash
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential python3-catkin-tools python3-pip
sudo rosdep init
rosdep update
```

## Vytvorenie workspace

```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin_make
```

## JetBot balíky

### JetBot ROS
```bash
cd ~/catkin_ws/src
git clone https://github.com/waveshare/jetbot_ros.git
cd ~/catkin_ws && catkin_make
```

### JetBot Pro
```bash
cd ~/catkin_ws/src
git clone https://github.com/waveshare/jetbot_pro.git
cd ~/catkin_ws && catkin_make && source ~/catkin_ws/devel/setup.bash
```

## Kamera

```bash
sudo apt-get install gstreamer1.0-tools libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev
cd ~/catkin_ws/src
git clone https://github.com/peter-moran/jetson_csi_cam.git
git clone https://github.com/ros-drivers/gscam.git
cd gscam
sed -e "s/EXTRA_CMAKE_FLAGS = -DUSE_ROSBUILD:BOOL=1$/EXTRA_CMAKE_FLAGS = -DUSE_ROSBUILD:BOOL=1 -DGSTREAMER_VERSION_1_x=On/" -i Makefile
cd ~/catkin_ws && catkin_make && source ~/catkin_ws/devel/setup.bash
```

## LIDAR

```bash
cd ~/catkin_ws/src
git clone https://github.com/Slamtec/rplidar_ros.git
cd ~/catkin_ws && catkin_make && source ~/catkin_ws/devel/setup.bash
```

## Navigačné balíky

```bash
sudo apt-get install ros-melodic-robot-pose-ekf
sudo apt-get install ros-melodic-gmapping
sudo apt-get install ros-melodic-hector-slam
sudo apt-get install ros-melodic-slam-karto
sudo apt-get install ros-melodic-cartographer-ros
sudo apt-get install ros-melodic-navigation
sudo apt-get install ros-melodic-teb-local-planner
sudo apt-get install ros-melodic-audio-common
```

## Python knižnice

```bash
sudo pip3 install jetson-stats
sudo pip3 install traitlets
sudo pip3 install jupyterlab
sudo pip3 install opencv-python
```

Aplikácia by mala byť pripravená na použitie.

Následne stačí spustiť server.ipynb a aplikácia je spustená.

V konzole je vypísaná IP adresa kde ablikácia beží.
