# 前提
已安装ROS2(dashing)+colcon  
# 创建一个工作空间  
在工作目录下（例：~/ros2_ws/src）  
`ros2 pkg create <pkg-name> --dependencies [deps]`  
显示创建C++包  
`ros2 pkg create <pkg-name> --dependencies [deps] --build-type ament_cmake`  
显示创建Python包  
`ros2 pkg create <pkg-name> --dependencies [deps] --build-type ament_python`

也可以在package.xml文件中修改依赖  
# 注释  
## C++包
见[网址](https://index.ros.org/doc/ros2/Tutorials/Developing-a-ROS-2-Package/)
