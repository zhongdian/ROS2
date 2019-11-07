[官网](http://wiki.ros.org/Installation/Ubuntu?distro=melodic)

## 存储库添加源列表

官网  
~~~
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
~~~
科大
~~~
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
~~~
清华
~~~
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
~~~

## 设置秘钥

`sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654`  

## 安装ROS

`sudo apt update`    
桌面版完全版（仿真+2D/3D模拟）：`sudo apt install ros-melodic-desktop-full`  
桌面版（仿真）：`sudo apt install ros-melodic-desktop`    
基本版：`sudo apt install ros-melodic-ros-base`  

## 检查ROS依赖

`sudo rosdep init`  
失败则：  
1:`sudo apt-get install ca-certificates`  
2:`sudo c_rehash /etc/ssl/certs`和`sudo -E rosdep init`  
~~3：`wget https://raw.github.com/ros/rosdistro/master/rosdep/sources.list.d/20-default.list`~~  
`rosdep update`

## 导入设置环境

`source /opt/ros/melodic/setup.bash`或`echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc`
