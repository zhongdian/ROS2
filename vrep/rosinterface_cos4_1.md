# 准备
1.下载rosinterface插件源代码，`branch： melodic`,`tag: v4.1`到`sim_ros_interface`文件夹中; `https://github.com/CoppeliaRobotics/simExtROSInterface/tree/melodic`   
2.升级cmake到3.16以上，按照`https://apt.kitware.com/`说明去做;  
3.安装·`xsltproc`:`sudo apt install xsltproc`。

# 编译
1.编译自定义消息包。并且导入环境；  
`source devel/setup.bash`  
2.将`coppeliasim 4.1`的根目录导入环境中;  
`export COPPELIASIM_ROOT_DIR=~/cos`  
3.创建文件夹`cos_ws/src`,将`sim_ros_interface`文件夹复制粘贴到其中;  
4.向`meta`里面添加自定义消息的路径。如报错可删去`msg`再试;  
5.修改`cmakelist.txt`和`package.xml`文件,使其包含自定义的消息包；    
6.`catkin_make`  
