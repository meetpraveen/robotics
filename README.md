# robotics
Mashup of rpi, lego spike and irobot create ros2

# Building the map package

```
source /opt/ros/humble/setup.bash
cd ./ros2/packages/map/src
ros2 pkg create --build-type ament_python --node-name map_node map_tutorials
```

# Adding a new node

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

