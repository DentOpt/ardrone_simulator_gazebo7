ModifiedTUM_simulator
=============
Author: Jan Dentler    
Date: 25.10.2018   
Email: jan.dentler@uni.lu


The AR.Drone 2.0 simulator is configured to subscribe control commands under the topic "/cmd_vel".

The AR.Drone 2.0 pose  published under "/pose"


Launch gazebo scenario from commandline:

    roslaunch cvg_sim\_gazebo ardrone_testworld.launch 
    
Launch drone (Takeoff) from commandline:
    
    rostopic pub -1 /ardrone/takeoff std_msgs/Empty
    
Move drone from commandline:
    


Control AR.Drone 2.0 in with denmpc:
either:

    rosrun denmpc scenario_ardrone_pose_tracking_node #To track center of UAV
 
 or:
 
    rosrun denmpc scenario_ardrone_sensor_tracking_node #To track with sensor constraint
 
 and:
 
    #Send desired pose
    rostopic pub /desiredpose geometry_msgs/PoseStamd '{header: {stamp: now, frame_id: "map"}, pose: {position: {x: 0.0, y: 0.0, z: 2.0}, orientation: {x: 0.0, y: 0.0, z: 0.0, w: 1.0}}}'




tum_simulator on Indigo and Gazebo 7
=============

These packages are used to simulate the flying robot Ardrone in ROS environment using gazebo simulator. Totally they are 4 packages. Their functions are descript as below:

1. cvg_sim_gazebo: contains object models, sensor models, quadrocopter models, flying environment information and individual launch files for each objects and pure environment without any other objects.

2. cvg_sim_gazebo_plugins: contains gazebo plugins for the quadrocopter model. quadrotor_simple_controller is used to control the robot motion and deliver navigation information, such as: /ardrone/navdata. Others are plugins for sensors in the quadrocopter, such as: IMU sensor, sonar sensor, GPS sensor.

3. message_to_tf: is a package used to create a ros node, which transfers the ros topic /ground_truth/state to a /tf topic.

4. cvg_sim_msgs: contains message forms for the simulator.

Some packages are based on the tu-darmstadt-ros-pkg by Stefan Kohlbrecher, TU Darmstadt.

This package depends on ardrone_autonomy package and gazebo7 so install these first.

How to install the simulator:

1. Install gazebo7 and ardrone_autonomy package

2. Create a workspace for the simulator

    ```
    mkdir -p ~/ardrone_simulator/src
    cd  ~/ardrone_simulator/src
    catkin_init_workspace
    ```
2. Download package

    ```
    git clone https://github.com/iolyp/ardrone_simulator_gazebo7
    ```
3. Build the simulator

    ```
    cd ..
    catkin_make
    ```
4. Source the environment

    ```
    source devel/setup.bash
    ```
How to run a simulation:

1. Run a simulation by executing a launch file in cvg_sim_gazebo package:

    ```
    roslaunch cvg_sim_gazebo ardrone_testworld.launch
    ```

How to run a simulation using ar_track_alvar tags:

1. Move the contents of  ~/ardrone_simulator/src/cvg_sim_gazebo/meshes/ar_track_alvar_tags/ to  ~/.gazebo/models

2. Run simulation

    ```
    roslaunch cvg_sim_gazebo ar_tag.launch
    ```
