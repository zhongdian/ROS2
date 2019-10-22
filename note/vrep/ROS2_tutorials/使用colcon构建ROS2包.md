# 准备工作

## 安装
安装colcon  
`sudo apt install python3-colcon-common-extensions`  
安装ROS2  

# 基础

## 创建一个工作空间
`mkdir -p ~/ros2_example_ws/src`  
`cd ~/ros2_example_ws`  
或者  
`ros2 pkg create ros2_example_ws`
## 添加一些源代码
`git clone https://github.com/ros2/examples src/examples`
## 构建工作空间
在工作空间的根目录上编译  
`colcon build --symlink-install`
## 测试
对构建的软件包进行测试  
`colcon test  
## 源环境
使用编译的软件包前，必须将其导入配置环境  
`. install/setup.bash`