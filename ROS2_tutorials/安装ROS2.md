[官网](https://index.ros.org/doc/ros2/)

## 设置语言环境

~~~
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
~~~  

## 安装源  

~~~
sudo apt update && sudo apt install curl gnupg2 lsb-release
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
~~~  

或者  
将`https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc`文件保存到本地，再 `sudo apt-key add ros.asc`。[ros.asc文件](https://github.com/zhongdian/ROS2/blob/master/ROS2_tutorials/ros.asc)。  
将存储库添加到源列表中  
~~~
sudo sh -c 'echo "deb [arch=amd64,arm64] http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
国内源：
sudo sh -c 'echo "deb [arch=amd64,arm64] http://mirrors.tuna.tsinghua.edu.cn/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
~~~  

## 安装ROS2

更新缓存：`sudo apt update`  
桌面安装（仿真+教程）：`sudo apt install ros-dashing-desktop`  
基础安装：`sudo apt install ros-dashing-ros-base`  

## 环境设置

安装命令行自动补全工具：`sudo apt install python3-argcomplete`  
导入设置环境：`source /opt/ros/dashing/setup.bash`或`echo "source /opt/ros/dashing/setup.bash" >> ~/.bashrc`  

## 安装colcon

`sudo apt install python3-colcon-common-extensions`  

## 安装其他RMW实现

OpenSplit：`sudo apt install ros-dashing-rmw-opensplice-cpp`  
RTI Connext：`sudo apt install ros-dashing-rmw-connext-cpp`
