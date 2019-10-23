# 前提
已安装ROS2(dashing)+colcon  
# 创建一个工作空间  
在工作目录下（例：~/ros2_ws/src）  
`ros2 pkg create <pkg-name> --dependencies [deps]`  
显式创建C++包  
`ros2 pkg create <pkg-name> --dependencies [deps] --build-type ament_cmake`  
显式创建Python包  
`ros2 pkg create <pkg-name> --dependencies [deps] --build-type ament_python`

也可以在package.xml文件中修改依赖  
# 注释  
## C++包
在CMakeLists.txt中  
### 抬头：  
```
cmake_minimum_required(VERSION 3.5)
project(**project_name**)
```  
### Default to C++14
```
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()
```  
### 寻找依赖包
```
find_package(ament_cmake REQUIRED)
find_package(example_interfaces REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
```  
### 创建可执行节点和链接依赖项
```
add_executable(action_client_member_functions member_functions.cpp)
ament_target_dependencies(<executable-name> [dependencies])
```  
### 安装启动文件和节点
#### Install launch files
```
install(
  DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
```  
#### Install nodes
```
install(
  TARGETS [node-names]
  DESTINATION lib/${PROJECT_NAME}
)
```  
### 收尾
`ament_package()`
## Python包
在Python包中，用setup.py代替C++包中的CMakeLists.txt
### 首先得有个setup.cfg文件
```
[develop]
script-dir=$base/lib/<package-name>
[install]
install-scripts=$base/lib/<package-name>
```  
### setup.py
```
import os
from glob import glob
from setuptools import setup

package_name = 'my_package'

setup(
    name=package_name,
    version='0.0.0',
    # Packages to export
    packages=[package_name],
    # Files we want to install, specifically launch files
    data_files=[
        ('share/ament_index/resource_index/packages', ['resource/' + package_name]),
        # Include our package.xml file
        (os.path.join('share', package_name), ['package.xml']),
        # Include all launch files.
        (os.path.join('share', package_name, 'launch'), glob('*.launch.py'))
    ],
    # This is important as well
    install_requires=['setuptools'],
    zip_safe=True,
    author='ROS 2 Developer',
    author_email='ros2@ros.com',
    maintainer='ROS 2 Developer',
    maintainer_email='ros2@ros.com',
    keywords=['foo', 'bar'],
    classifiers=[
        'Intended Audience :: Developers',
        'License :: TODO',
        'Programming Language :: Python',
        'Topic :: Software Development',
    ],
    description='My awesome package.',
    license='TODO',
    # Like the CMakeLists add_executable macro, you can add your python
    # scripts here.
    entry_points={
        'console_scripts': [
            'my_script = my_package.my_script:main'
        ],
    },
)
```
