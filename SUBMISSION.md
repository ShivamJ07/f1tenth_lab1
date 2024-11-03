# Lab 1: Intro to ROS 2

## Written Questions

### Q1: During this assignment, you've probably ran these two following commands at some point: ``source /opt/ros/foxy/setup.bash`` and ``source install/local_setup.bash``. Functionally what is the difference between the two?

* `source /opt/ros/foxy/setup.bash`: This command sets up the environment for ROS 2 Foxy by adding ROS 2 binaries and packages to your system's environment path. It enables ROS 2 commands globally, giving access to ROS 2 packages installed in the system-wide directory (`/opt/ros/foxy`).
* `source install/local_setup.bash`: This command sets up the environment for your specific workspace, allowing ROS 2 to recognize any packages you've built locally within this workspace. It enables you to run or launch packages that exist in the `install` directory of your workspace without interfering with the system-wide ROS 2 setup.

### Q2: What does the ``queue_size`` argument control when creating a subscriber or a publisher? How does different ``queue_size`` affect how messages are handled?

The `queue_size` argument defines the number of messages that can be stored in the queue if the subscriber or publisher cannot process them immediately. It controls the Quality of Service (QoS) for the message flow, particularly for cases when the subscriber or publisher operates at different rates than the message production.

* A **smaller queue_size** means fewer messages will be stored. If new messages arrive when the queue is full, older messages will be discarded. This is useful for time-sensitive data where only the most recent messages are important (e.g., real-time sensor data).
* A **larger queue_size** allows more messages to be buffered before any are dropped, which is useful for applications where each message is important and needs to be processed even if there's a delay (e.g., logging data).

Choosing the right `queue_size` depends on the application’s requirements for real-time data versus historical data reliability.

### Q3: Do you have to call ``colcon build`` again after you've changed a launch file in your package? (Hint: consider two cases: calling ``ros2 launch`` in the directory where the launch file is, and calling it when the launch file is installed with the package.)

* **When calling `ros2 launch` from the source directory (e.g., `launch/` folder):** You do **not** need to call `colcon build` again. ROS 2 can directly access the modified launch file if you run the launch command from the source directory, as it does not require the launch file to be installed.
* **When calling `ros2 launch` after installing the package:** You **do** need to call `colcon build` again if you want to use the updated launch file. This rebuilds the package and copies the updated launch file into the `install` directory. If you skip `colcon build`, the installed version of the launch file remains outdated.
