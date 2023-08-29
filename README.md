# cras\_relative\_positional\_controller

A simple action-based controller that executes a relative change of robot pose without any feedback, just issuing proper `cmd_vel` commands to the robot.

Each pose change request has maximum velocity specified, and this controller just these maximum velocity commands until the position is changed enough.

Please note that this controller doesn't use feedback. So if you instruct it to go 1 meter forward with max. velocity 0.1 m/s, it just issues a 0.1 m/s velocity command for 10 seconds and then stops. If the robot hits a wall in the meantime, this controller won't know and care.


## Nodes

### relative\_position\_controller

This node starts the action server (on topics derived from the resloved name of this node).

#### Published topics

- `~cmd_vel` (`geometry_msgs/Twist`): Velocity commands for the robot.

#### Action server

- `<NODE_NAME>` (`cras_relative_positional_controller/RelativeMove`): The action for moving the robot.

#### Parameters

- `max_lin_vel` (`float`, default 1.0 m/s): Maximum linear velocity (this caps velocities requested in the action).
- `max_ang_vel` (`float`, default pi/2 rad/s): Maximum angular velocity (this caps velocities requested in the action).
- `max_age` (`float`, default 3.0 s): If the received goal is older than this number of seconds, it will be rejected (this prevents executing stale/delayed actions).
 
