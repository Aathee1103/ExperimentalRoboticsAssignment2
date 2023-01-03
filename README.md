#ExperimentalRoboticsAssignment2

The Repository consists of packages required for the Assignment 2 of Experimental Robotics labarotary course.ths assignment is the continuation of the first assignment of this course which will be available in this link https://github.com/Aathee1103/ExperimentalRobotics-Assignment1-.The last assignment's goal was to develop an software architecture for the surveillance robot with the hep of ontolgy to know the location of the robot.Also,identify the external stimulus like an battery-low.the aim of this assignment is to develop an practical simuation of the ideas developed in the first assignment.In this assignment,initially there exists an world in gazebo developed by professor Carmine Recchiuto with aruco makers and rooms.

# Aim of th Assigment:
- Develop and robot urdf model and spawn in the environment in the position x = -6.0, y = 11.0.
- Scan the aruco markers by rotating the robotic arm mounted on the link chassis of robot.
- Survey the rooms with the ontology conceptdeveloped in the previous assignment,when the stimulus battery-low arrives the rbot should reach room E to get recharged.

# 1.Robot Model and description:
![Screenshot 2023-01-02 173837](https://user-images.githubusercontent.com/80621864/210327492-c46c3c08-2bb1-4b4c-a9cc-250e743da056.jpg)
- The above image shows how the robot model is built.the robot has 2 wheels which is a continuous joint which is controlled with differentia drive controller.it has also a robotic arm which includes a base with continuous join,two revolute joint,one fixed joint and one prismatic joint.the robot description is done in the robot_urdf folder which consists of two files **robot4.xacro** and **robot4.gazebo** where the links,joint and controlled have been mentioned.
- Acamera is attached in the prismatic joint to scan the the aruco markers which is done with the help of **aruco ros** package,where marker publisher node publishes atandard message of topic named as **/scan_marker** and the finite state machine subcribes to the publisher to get the semantic infromation of the map by calling the **marker_server** service node.
- Same planners and controller action servers are used which has been already used in the first asssignment.additionally move_base is used in this assignment.
# 2.Scanning aruco markers:
![Scanning_marker](https://user-images.githubusercontent.com/80621864/210329002-6ae2f9cb-6f9e-43e7-9bef-7d61fc5bf4fa.gif)
- The video shows how the robotic arm is used to scan the markers with the help of robotic arm.the robotic arm is rotated by publishing to the topic **/robot4/joint1_position_controller/command**(This command is for the joint 1,similary done for all other joints).the marker_server service is called to get the response where the detals of the rooms is provided where the marker id is the request provided.the marker pblisher node is startded using the command **rosrun aruco_ros marker_publisher /image:=/camera3/image_raw** .
 
 ![Screenshot 2023-01-02 180429](https://user-images.githubusercontent.com/80621864/210336742-064c7aab-8e30-464b-8688-a6a060db3ac2.jpg)

 - Once the Scanning of markers is completed,the robot will go to the location **E** to upload the map.




# 3.Working:
- The working of the assignment has been shown in the **overall_woking.gif**.where the robot is moving in the environment with the help of move_base goal given to it.gmapping pachage is also used to develop the map for the robot,collison avoidance or obstacle avoidance are using these two packages.with the help of Rviz we can visualize ho the robot s building the map,setting the target accordingly.also local and global cost map is provided with the help of gmapping and move_base package.the robot is also equiped with a laser in its front to know where the obstacles are there develop the map according to that.once the robot reaces the room or the corridor it rotates to monitor before going to another target.
 
 ![Screenshot 2023-01-02 181656](https://user-images.githubusercontent.com/80621864/210332988-5821e92e-08bd-4581-bc94-04bd05a43d87.jpg)

- when the robot's batter is low the goals are cancelled and reaches the location **E** to get charged.
 
 ![Screenshot 2023-01-02 210032](https://user-images.githubusercontent.com/80621864/210333447-ccbed254-9c15-4adc-b152-d38f96fd508a.jpg)

- The above image shows the changes between the states,sam set of states has been used with respect to the last assignment,but additionall a state called as **SCANNING** has been added befre loading the map.


 ![robot_monitor](https://user-images.githubusercontent.com/80621864/210334112-1a7d4831-0b80-4f6c-98f5-f2c6cbbe8c81.gif)

- The video shows how the robot is rotated when it reaches the room or an corridor,tis is done by publishing to the topic  **/cmd_vel** and provided an ngle to rotate.

# 4.Installation and Running the project:
```
$cd ros_ws/src/git clone https://github.com/Aathee1103/ExperimentalRoboticsAssignment2
$cd ros_ws/ catkin_make to build the workspace.
$roslaunch assignment2 mb2.launch where the launch file launches the gmapping,move_base packages and spawns the robot in the world.
$open another tab and run the command rosrun aruco_ros marker_publisher /image:=/camera3/image_raw to run marker_publisher node.
$rosrun smach_viewer smach_viewer.py to visualize the change in states.
```
In the mb2.launch file assignment.launch,gmapping.launch,move_base.launch has been added.




