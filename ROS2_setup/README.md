# Sourcing Environment

Instead of sourcing the `setup.bash` file every time we open a new terminal, we can append the sourcing line in the `.bashrc` file with the following steps:

1. Open the `.bashrc` file:
    ```bash
    gedit ~/.bashrc
    ```
    This command will open the `.bashrc` file.

2. Append the following line at the end of the `.bashrc` file:
    ```bash
    source /opt/ros/jazzy/setup.bash
    ```

3. Save the file and exit.

To check if this works, try running the `ros2 run` command in a new terminal. If done correctly, it will show an error asking for other parameters. If it didn't identify the `ros2` command, you should recheck if the environment is sourced correctly.

# Nodes

Let's first try running inbuilt nodes to get a fair idea. For that:

1. Open a new terminal and run the following command to start a talker node:
    ```bash
    ros2 run demo_nodes_cpp talker
    ```

2. In another terminal, run the command for the listener node:
    ```bash
    ros2 run demo_nodes_cpp listener
    ```

You should now see the message from the talker being received by the listener.

3. On another terminal, try running `rqt_graph` to see a graph:
    ```bash
    rqt_graph
    ```
    (Try refreshing the page if only the talker node is visible in the chart).

You should be able to see two nodes: talker and listener over the topic "chatter".

## Installing Turtlesim

For a more interactive dive into nodes, try installing `turtlesim`:

1. Run the following command to install the `turtlesim` package:
    ```bash
    sudo apt-get install ros-jazzy-turtlesim
    ```

2. Create a random turtle in a blue environment:
    ```bash
    ros2 run turtlesim turtlesim_node
    ```

3. Control the turtle with arrow keys and letters:
    ```bash
    ros2 run turtlesim turtle_teleop_key
    ```

# Workspace Setup

Start with these commands to install `colcon`:

1. Update the package list:
    ```bash
    sudo apt update
    ```

2. Install `colcon` common extensions:
    ```bash
    sudo apt install python3-colcon-common-extensions
    ```

To enable auto-completion of `colcon` command lines, source the `arg-complete` bash file:

```bash
source /usr/share/colcon_cd/function/colcon_cd-argcomplete.bash
```

We can use the same approach as sourcing the ROS environment by permanently sourcing this bash file in the `.bashrc` file:

```bash
source ~/.bashrc
```

This will ensure that every new terminal will automatically source all the paths included in it.

## Creating a Workspace

1. Create a new workspace directory named `ros2_ws`:
    ```bash
    mkdir ros2_ws
    cd ros2_ws
    mkdir src
    ```

    (The `src` name is fixed by default, use only that to be recognized).

2. If you run the `ls` command, you can only see the `src` folder.

3. Inside `ros2_ws` (not in `src`), run the command:
    ```bash
    colcon build
    ```
    It should show `0 packages finished` as we are just starting.

4. On checking with `ls` again in the workspace, you can see three additional folders: `build`, `install`, and `log`.

To be able to make custom ROS2 nodes, we have to source the setup file in the `install` folder:

```bash
source ~/ros2_ws/install/setup.bash
```

We can append the sourcing line again in the `.bashrc` file:

```bash
echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

# Python Package Creation

Navigate to `src` in the ROS2 workspace and create a package:

```bash
cd ~/ros2_ws/src
ros2 pkg create <package-name> --build-type ament_python --dependencies rclpy
```

We can now use the `code .` command to open the present working path in VS Code if it is already installed:

```bash
code .
```

# Node Creation

In the `src` folder, navigate to your package and open it. There will be a directory with the same name as the package. Navigate to that and create your node by following these commands:

1. Navigate to your package directory:
    ```bash
    cd ~/ros2_ws/src/<package-name>/<package-name>/
    ```

2. Create a new node file:
    ```bash
    touch <node>.py
    ```

3. Now, you should see two files, one is `__init__.py` and the other is the node you created (`<node>.py`). Check with `ls`.

4. Make the file executable:
    ```bash
    chmod +x <node>.py
    ```

    The color of the node will now change from white to blue on checking with `ls`.

5. Use `code .` to open this path in VS Code:
    ```bash
    code .
    ```

6. Install the ROS extension and others if recommended.

Edit your node file as follows:

```python
from rclpy.node import Node
import rclpy

class MyNode(Node):

    def __init__(self):
        super().__init__("first_node")
        self.counter_ = 0
        self.create_timer(1.0, self.timer_callback)

    def timer_callback(self):
        self.get_logger().info("Hello ROS2, " + str(self.counter_))
        self.counter_ += 1

def main(args=None):
    rclpy.init(args=args)
    node = MyNode()
    rclpy.spin(node)
    rclpy.shutdown()

if __name__ == '__main__':
    main()
```

Append the console script entry in `setup.py` (a file in the package):

```python
entry_points={
    'console_scripts': [
        "<node-name-to-be-displayed-in-terminal> = <package-name>.<node>:main"
    ],
},
```

We can run this node as usual after rebuilding using `colcon` and then sourcing the `.bashrc` file, and then using the run command:

1. Navigate to the workspace root:
    ```bash
    cd ~/ros2_ws/
    ```

2. Build the package with symlink install:
    ```bash
    colcon build --symlink-install
    ```

3. Source the `.bashrc` file:
    ```bash
    source ~/.bashrc
    ```

4. Run the node:
    ```bash
    ros2 run <package-name> <node-name-to-be-displayed-in-terminal>
    ```

Using `--symlink-install` will consider the current version of the file automatically, avoiding the need to repeatedly use `colcon build`.
