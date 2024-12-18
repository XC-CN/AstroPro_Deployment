# Astro-Pro-ORB_SLAM2

## 1.安装SDK
基于奥比中光Ai开放平台文档：https://vcp.developer.orbbec.com.cn:9001/project-2/doc-83/
### （1）安装依赖
```
sudo apt install libgflags-dev  ros-$ROS_DISTRO-image-geometry ros-$ROS_DISTRO-camera-info-manager\
ros-$ROS_DISTRO-image-transport ros-$ROS_DISTRO-image-publisher libgoogle-glog-dev libusb-1.0-0-dev libeigen3-dev
```
### （2）安装libuvc
```
git clone https://github.com/libuvc/libuvc.git
cd libuvc
mkdir build && cd build
cmake .. && make -j4
sudo make install
sudo ldconfig
```
安装完留下的文件（相当于安装包）可以删除，libuvc已经安装到系统中。

## 2.配置ROS工作空间
新建工作空间
`mkdir -p ~/ros_ws/src`

将本仓库中的文件OpenNI_SDK_ROS_v1.1.4_20220927_e5a9dc_Linux.zip解压并放入src文件夹中

编译：
```
cd ~/ros_ws
catkin_make
```

安装libusb rules
```
cd ~/ros_ws
source ./devel/setup.bash
roscd astra_camera
./scripts/create_udev_rules
sudo udevadm control --reload && sudo  udevadm trigger
```

## 3.启动相机并测试
在terminal 1
```
source ./devel/setup.bash 
roslaunch astra_camera astra.launch
```
在terminal 2
```
source ./devel/setup.bash
rviz
```

设置Rviz，使得深度随颜色变化
![image](https://github.com/user-attachments/assets/72652ef8-cf56-4039-831e-dc6de0033642)
具体更改选项：

1.Add\
/camera/depth/points/PointClouds2

2.修改左侧选项\
Fixed Frame: camera_depth_frame
Color Transformer: AxisColor


