为了使colcon能够找到launch文件，我们需要在python包中修改setup.py文件。  
~~~
import os
from glob import glob
from setuptools import setup

package_name = 'my_package'

setup(
    # Other parameters ...
    data_files=[
        # ... Other data files
        # Include all launch files. This is the most important line here!
        (os.path.join('share', package_name), glob('launch/*.launch.py'))
    ]
)
~~~
C++包则只需要在Cmakelist.txt文件中添加一段代码即可  
~~~
# Install launch files.
install(DIRECTORY
  launch
  DESTINATION share/${PROJECT_NAME}
)
~~~
launch.py样例  
~~~
import launch
import launch.actions
import launch.substitutions
import launch_ros.actions


def generate_launch_description():
    return launch.LaunchDescription([
        launch.actions.DeclareLaunchArgument(
            'node_prefix',
            default_value=[launch.substitutions.EnvironmentVariable('USER'), '_'],
            description='Prefix for node names'),
        launch_ros.actions.Node(
            package='demo_nodes_cpp', node_executable='talker', output='screen',
            node_name=[launch.substitutions.LaunchConfiguration('node_prefix'), 'talker']),
    ])
~~~