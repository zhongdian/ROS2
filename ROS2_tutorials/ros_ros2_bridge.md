This package provides a network bridge which enables the exchange of messages between ROS 1 and ROS 2.

The bridge is currently implemented in C++ as at the time the Python API for ROS 2 had not been developed. Because of this its support is limited to only the message/service types available at compile time of the bridge. The bridge provided with the prebuilt ROS 2 binaries includes support for common ROS interfaces (messages/services), such as the interface packages listed in the ros2/common_interfaces repository and tf2_msgs. See the documentation for more details on how ROS 1 and ROS 2 interfaces are associated with each other. If you would like to use a bridge with other interfaces (including your own custom types), you will have to build the bridge from source (instructions below), after building and sourcing your custom types in separate ROS 1 and ROS 2 workspaces. See the documentation for an example setup.

For efficiency reasons, topics will only be bridged when matching publisher-subscriber pairs are active for a topic on either side of the bridge. Note that before rostopic echo would work with bridged topics, a subscriber must already exist, in order for echo to determine the message type and then to create its own subscriber. You can use the --bridge-all-2to1-topics option to bridge all ROS 2 topics to ROS 1 so that tools such as rostopic list and rqt will see the topics even if there are no matching ROS 1 subscribers. Run ros2 run ros1_bridge dynamic_bridge -- --help for more options.

该软件包提供了一个网桥，可以在ROS 1和ROS 2之间交换消息。

该桥目前是用C ++实现的，因为还没有开发出Python 2的Python API。因此，它的支持仅限于桥的编译时可用的消息/服务类型。设置有预建ROS 2二进制桥包括用于共同ROS接口（消息/服务），诸如中列出的接口包的支持ros2 / common_interfaces库和tf2_msgs。有关ROS 1和ROS 2接口如何相互关联的更多详细信息，请参阅文档。如果您想将桥接器与其他接口（包括您自己的自定义类型）一起使用，则必须在单独的ROS 1和ROS 2工作空间中构建和获取自定义类型后，从源代码构建桥接器（下面的说明）。看到示例设置的文档。

出于效率原因，只有当桥接器两侧的主题的匹配发布者 - 订阅者对处于活动状态时，才会桥接主题。请注意，在rostopic echo使用桥接主题之前，必须已存在订户，以便echo确定消息类型，然后创建自己的订户。您可以使用该--bridge-all-2to1-topics选项将所有ROS 2主题桥接到ROS 1，以便即使没有匹配的ROS 1订阅者rostopic list，rqt也可以查看主题等工具。运行ros2 run ros1_bridge dynamic_bridge -- --help以获取更多选项。
https://github.com/ros2/ros1_bridge/blob/master/README.md

# 安装ros2
* 导入ros2环境设置:`. /opt/ros/dashing/setup.bash`  
* 下载ros1_bridge源码到workspace/src:`git clone -b dashing https://github.com/zhongdian/ros1_bridge.git`
* 下载缺少的配置文件到workspace/src:`git clone https://github.com/zhongdian/ros_bridge_file.git`  

* 在workspace目录下编译  
* 用colcon编译除ros1_bridge的其他包：
`colcon build --symlink-install --packages-skip ros1_bridge`

* 配置ros1环境：`source /opt/ros/melodic/setup.bash`

* 配置ros2环境： `. /opt/ros/dashing/local_setup.bash`

* ~~如果有一个ROS1覆盖环境： `. <install-space-to-ros1-overlay-ws>/setup.bash`~~

* ~~如果有一个ROS2覆盖环境： `. <install-space-to-ros2-overlay-ws>/local_setup.bash`~~

* 再编译ros1_bridge: `colcon build --symlink-install --packages-select ros1_bridge --cmake-force-configure`差不多需要十分钟  

**注意：如果编译报错：not found launch_testing_ament_cmake ,去github上下载ros2/launch里面的文件到workspace/src中：`git clone https://github.com/ros2/launch.git`，从头开始编译，即可解决**


* shell A:  
配置ros1环境： `. /opt/ros/melodic/setup.bash`  
启动roscore: `roscore` (-p 11311)记住ROS_MASTER_URI:11311  

* shell B:  
~~配置ros1环境： `. /opt/ros/melodic/setup.bash`~~  
~~配置ros2环境： `. /opt/ros/dashing/setup.bash`~~  
导入桥所在包的设置环境：`source ~/workspace/install/local_setup.bash`  
启动桥： `export ROS_MASTER_URI=http://localhost:11311`  
       `ros2 run ros1_bridge dynamic_bridge`  

配置完成。

# 实例
* **实例1a：ROS 1 talker and ROS 2 listener**

shell C:  
配置ros1环境： `. /opt/ros/melodic/setup.bash`  
运行ros1节点： `rosrun rospy_tutorials talker`    

shell D:  
配置ros2环境：`. /opt/ros/dashing/setup.bash`  
运行ros2节点： `ros2 run demo_nodes_cpp listener`  

* **实例1b：ROS 2 talker and ROS 1 listener**

shell C：  
配置ros1环境： `. /opt/ros/melodic/setup.bash`  
运行ros1节点： `rosrun roscpp_tutorials listener`  

shell D:  
配置ros2环境：`. /opt/ros/dashing/setup.bash`  
运行ros2节点： `ros2 run demo_nodes_py talker`  

* **实例2：run the bridge and exchange images**

shell C：  
配置ros1环境： `. /opt/ros/melodic/setup.bash`  
运行ros1节点： `rqt_image_view /image`  

shell D:  
配置ros2环境：`. /opt/ros/dashing/setup.bash`  
运行ros2节点： `ros2 run image_tools cam2image`  

shell E:  
配置ros1环境： `. /opt/ros/melodic/setup.bash`  
发布消息： `rostopic pub -r 1 /flip_image std_msgs/Bool "{data: true}"`  
         `rostopic pub -r 1 /flip_image std_msgs/Bool "{data: false}"`  

* **实例3： run the bridge for AddTwoInts service**

shell C:  
配置ros1环境： `. /opt/ros/melodic/setup.bash`  
~~export ROS_MASTER_URI=http://localhost:11311~~  
运行ros1节点： `rosrun roscpp_tutorials add_two_ints_server`  

shell D:  
配置ros2环境：`. /opt/ros/dashing/setup.bash`  
运行ros2节点： `ros2 run demo_nodes_cpp add_two_ints_client`  


