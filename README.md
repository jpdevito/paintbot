## ROS Setup

Put the files from the `on_remote_pc` directory into the `src` folder of a ROS workspace on your remote PC. If you're using an Ubuntu machine, these can be built using `catkin_make`.

Put the files from the `on_paintbot` directory into the `src` folder of a ROS workspace on the Turtlebot's Raspberry Pi. `catkin_make` can have issues in this environment, so instead build the files using `catkin_make_isolated`.

*Note: Make sure the workspaces that you are putting these packages in don't already have packages of the same name (e.g. don't use the `burger_ws` workspace on Dr. Otte's Turtlebots, you can make a new workspace)*

Make sure all ROS workspaces are sourced correctly. To properly source the workspace on the Turtlebot after running `catkin_make_isolated` you can add the following two lines to your `~/.bashrc` file:

`source <path_to_workspace>/devel_isolated/dynamixel_workbench_controllers/setup.bash`
`source <path_to_workspace>/devel_isolated/turtlebot3_bringup/setup.bash`

Replacing `<path_to_workspace>` with the path to your ROS workspace.


## Physical Setup

Plug the Dynamixel AX-12A through a U2D2 into one of the open USB ports on the Turtlebot’s Raspberry Pi.

Follow the device setup instructions for the U2D2 at this link:

(https://emanual.robotis.com/docs/en/software/dynamixel/dynamixel_workbench/)

The Dynamixel should be set to a baud rate of 1000000, have the name “AX-12A”, and be plugged into the port `/dev/ttyUSB0` by default. If you want to use the same files to run a Dynamixel with a different baud rate or name, or your Dynamixel is connected to a different port, modify `launch/dynamixel_workbench_controllers.launch` and/or `config/paintbot_arm.yaml` in the `dynamixel_workbench_controllers` package accordingly.

To get that information, you can run this command:

`$ rosrun dynamixel_workbench_controllers find_dynamixel <port>`

For different values of `<port>`, e.g. `/dev/ttyUSB0`, `/dev/ttyUSB1`, etc.

## Commands for Bring-Up and Teleoperation

**Run these commands on a computer that is viewed as the ROS master by the Turtlebot.**

`$ roscore`

*New terminal, ssh into Turtlebot*

`$ roslaunch turtlebot3_bringup paintbot.launch`

You will see an "incorrect status packet" error; that is fine.

If you are getting a "groupSyncRead getdata failed" error, press Ctrl-C and try the command again.

If the process gives an error and stops, try the command again.

*New terminal*

`$ roslaunch paintbot_teleop paintbot_teleop.launch`

Now you can control the Turtlebot and actuator with your keyboard!

