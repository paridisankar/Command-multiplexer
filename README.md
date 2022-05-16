# Command-multiplexer

Introduction  


The cmd_vel_mux package can infer its purpose from the name, that is, to select the speed (In electronics, a multiplexer or mux is a device that selects one of several analog or digital input signals and forwards the selected input into a single line). This function is sometimes useful. For example, when the robot encounters an emergency when autonomous navigation, it needs to switch to manual control mode. At this time, the control of the robot needs to be switched from the node of autonomous navigation to the steering wheel, handle, keyboard, emergency stop switch, etc. control node.  

If there are multiple nodes that want to control the motion of the robot, the multiplexer (cmd_vel_mux) allows all these commands to be used in parallel and can be prioritized, with higher priority preempting lower priority tasks. For example, when a robot navigates autonomously, there may be the following 4 priority tasks (usually set the priority of autonomous behavior to the lowest):

k+3 (highest priority): safety controller     

k+2: keyboard teleop    

k+1: android teleop (Android remote control)     

k: (lowest priority): navi stack teleop (navigation pack autonomous control)


In general, the navi package controls the robot most of the time. However, the commands of the navi package can be overridden by triggering commands through the Android remote control app or keyboard remote control. If both commands are given, the remote commands from the keyboard will take precedence. When the collision or drop sensor sends an alarm signal and triggers the command of the safety controller, all the above speed commands will be rewritten, so as to ensure the safety of the robot when it moves autonomously. 

Principle introduction  The core node in the twist_mux function package is twist_mux, and its input and output are as follows:

The input on the left is multiple topics of type geometry_msgs::Twist. After the selection of twist_mux, the only topic of geometry_msgs::Twist is output. The topic entered below is the lock topic of the user's dynamic configuration selection mechanism. The message type of the topic is Bool. Just like the lock, there are only two states: open and closed. The concept of lock here can be understood as: by restricting input sources with different priorities, the effect of controlling the output is achieved.      


Install  Download the source code on github: https://github.com/yujinrobot/yujin_ocs      


File analysis in param  example.yaml file
