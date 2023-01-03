#ExperimentalRoboticsAssignment2

The Repository consists of packages required for the Assignment 2 of Experimental Robotics labarotary course.ths assignment is the continuation of the first assignment of this course which will be available in this link https://github.com/Aathee1103/ExperimentalRobotics-Assignment1-.The last assignment's goal was to develop an software architecture for the surveillance robot with the hep of ontolgy to know the location of the robot.Also,identify the external stimulus like an battery-low.the aim of this assignment is to develop an practical simuation of the ideas developed in the first assignment.In this assignment,initially there exists an world in gazebo developed by professor Carmine Recchiuto with aruco makers and rooms.

# Aim of th Assigment:
- Develop and robot urdf model and spawn in the environment in the position x = -6.0, y = 11.0.
- Scan the aruco markers by rotating the robotic arm mounted on the link chassis of robot.
- Survey the rooms with the ontology conceptdeveloped in the previous assignment,when the stimulus battery-low arrives the rbot should reach room E to get recharged.

# 1.Robot Model and description:
![Screenshot 2023-01-02 173837](https://user-images.githubusercontent.com/80621864/210327492-c46c3c08-2bb1-4b4c-a9cc-250e743da056.jpg)
- The above image shows how the robot model is built.the robot has 2 wheels which is a continuous joint which is controlled with differentia drive controller.it has also a robotic arm which includes a base with continuous join,two revolute joint,one fixed joint and one prismatic joint.
- Acamera is attached in the prismatic joint to scan the the aruco markers which is done with the help of **aruco ros** package,where marker publisher node publishes atandard message of topic named as **/scan_marker** and the finite state machine subcribes to the publisher to get the semantic infromation of the map by calling the **marker_server** service node.
# 2.Scanning aruco markers:
![Scanning_marker](https://user-images.githubusercontent.com/80621864/210329002-6ae2f9cb-6f9e-43e7-9bef-7d61fc5bf4fa.gif)
The video shows how the robotic arm is used to scan the markers with the help of robotic arm.the robotic arm is rotated by publishing to the topic **/robot4/joint1_position_controller/command**(This command is for the joint 1,similary done for all other joints).the marker_server service is called to get the response where the detals of the rooms is provided where the marker id is the request provided.

# 3.Working:
![](../overall_working.gif)


To start, you are provided with this package, which contains:
- the definition of a custom message and a custom service
- a simulation environment representing the "house" to be monitored
- a node that implements a service: it requires the id (marker) detected by the robot and it replies with the information about the corresponding room (name of the room, coordinates of the center, connections with other rooms)
- A launch file, which starts Gazebo with the simulation environment, and the service node (assignment.launch).

You have to:
- Add a robot to the environment;
- Integrate (if needed, modify it) the architecture that you have developed in the first assignment to the given scenario.

In particular, the robot will have to:
- Be spawned in the initial position x = -6.0, y = 11.0
- Build the "semantic" map of the environment by detecting, without moving the base of the robot, all seven markers that are present around it, by calling the provided service node. Try to "scan" the environment in a comprehensive way, possibly exploring different solutions related to the robot's model. 
- Start the patrolling algorithm by relying on autonomous navigation strategies (mapping/planning) and on the information collected and stored in the ontology during the previous step.
- When a room is reached, perform a complete scan of the room (by rotating the base or the camera).


