发布转换数据  
发布从父坐标系`foo`到子坐标系`bar`的静态坐标变换位移（1 2 3）姿态（0.5 0.1 -1.0）：    
`ros2 run tf2_ros static_transform_publisher 1 2 3 0.5 0.1 -1.0 foo bar`  
显示装换数据：  
`ros2 run tf2_ros tf2_echo foo bar`  

具体看`dummy_robot_bringup`包