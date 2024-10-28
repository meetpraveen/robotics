# robotics
Mashup of rpi, lego spike and irobot create ros2

# Lego build HAT program

Refer to official reference pages from [Raspberry build HAT](https://www.raspberrypi.com/documentation/accessories/build-hat.html#:~:text=Connect%20an%20external%20power%20supply,will%20power%20the%20Build%20HAT.)

First install the buildhat python package

```shell
sudo pip3 install buildhat ipython
```

Open up your favorite python editor, or if you want a scratch pad open up ipython
```shell
ipython
```

```python
from buildhat import Motor
motor_a = Motor('A')
motor_a.run_for_seconds(5)
```

# iRobot ros2 program

Turtlebot documents works with any custom mod of iRobot create with rpi. Please refer to their examples and tutorials [here](https://turtlebot.github.io/turtlebot4-user-manual/tutorials/first_node_python.html). The steps below is taken from there. For basic learning samples, refer to [iRobot Education online IDE](https://python.irobot.com/)

## Creating the map package

```
source /opt/ros/humble/setup.bash
cd ./ros2/packages/map/src
ros2 pkg create --build-type ament_python --node-name map_node map_tutorials
```

## Adding a new node

Create a new python file at `./ros2/packages/map/src/map_tutorials/<my_node>.py

With the code structure as follows

```
from irobot_create_msgs.msg import InterfaceButtons, LightringLeds

import rclpy
from rclpy.node import Node
from rclpy.qos import qos_profile_sensor_data

class MyNode(Node):
    lights_on_ = False

    def __init__(self):
        super().__init__('my_node')

def main(args=None):
    rclpy.init(args=args)
    node = MyNode()
    rclpy.spin(node)
    node.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

## Building the map package and map node

```
cd ./robotics/ros2/packages/map/
colcon build --symlink-install --packages-select map_tutorials
source install/local_setup.bash
```

## Running the node

Validate that the topics used in the class are available. Goto terminal of raspberry pi and execute this -
```
$>ros2 topic info /interface_buttons --verbose
```

```
ros2 run map_tutorials map_nod
```
