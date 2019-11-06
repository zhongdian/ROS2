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
将`https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc`文件保存到本地，再 `sudo apt-key add ros.asc`