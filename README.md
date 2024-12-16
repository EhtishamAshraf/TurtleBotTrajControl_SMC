# TurtleBot 8-Shape Trajectory Tracking Using FBTC and FBSMC
This repository contains a ROS-based implementation for comparing Flatness-Based Trajectory Control (FBTC) and Flatness-Based Sliding Mode Control (FBSMC) for trajectory tracking on a TurtleBot. The robot is tasked with following an 8-shaped trajectory, and the performance of both control strategies is analyzed using logged data.

### Features
- **ROS Package**: `trajectory_control_pkg`
- **Simulation and Hardware**: The repo provides the code which works in Gazebo Simulation as well as Real world
- **Control Algorithms**:
  - **FBTC**: A control method utilizing differential flatness for trajectory planning and tracking.
  - **FBSMC**: A robust control approach combining sliding mode control with flatness for enhanced disturbance rejection.
- **Trajectory Tracking**:
  - The robot follows an 8-shaped trajectory in both simulation and the physical world.
  - Robot pose data is logged for post-processing and analysis.
- **Data Analysis**:
  - Pose data is saved to an Excel file for further evaluation.
  - Visual comparisons are provided to illustrate the reference trajectory versus the actual trajectory for both FBTC and FBSMC.

![Turtlebot3](https://github.com/EhtishamAshraf/TurtleBotTrajControl_SMC/blob/7057946c40d2ec66b5d0790165a0b60bdfc86f61/2-Hardware_Data/Images/Robot_1.png)

## Demo Videos
### FBTC
You can watch the demo video of Trajectory following with FBTC by clicking on the below image
[![Watch the video](https://github.com/EhtishamAshraf/TB3_slam_with_virtual_obstacles/blob/2adfd5ad148a105782329a14557024fdacdf6fbb/src/slam_lane_tracking_pkg/Image/6-Navigation.png)](https://youtu.be/Ury2mBSe-fI)
### FBSMC
You can watch the demo video of Trajectory following with FBSMC by clicking on the below image
[![Watch the video](https://github.com/EhtishamAshraf/TB3_slam_with_virtual_obstacles/blob/2adfd5ad148a105782329a14557024fdacdf6fbb/src/slam_lane_tracking_pkg/Image/6-Navigation.png)](https://youtu.be/VayJJ_5sFE0)

## Gazebo World
For this project, empty Gazebo world is used as shown below
![Turtlebot3](https://github.com/EhtishamAshraf/TurtleBotTrajControl_SMC/blob/7218680308a7305bf3b7cf842722acf0856db109/2-Hardware_Data/Images/Gazebo_world.png)

### Note
Details about cloning the repository are given at the end of this readme file

# 8-shape Trajectory Following
The trajectory is mathematically defined using parametric equations to create a smooth figure-eight path. Two controllers are used for this purpose: 
1.  Flatness-Based Trajectory Controller (FBTC)
2.  Flatness-Based Sliding Mode Controller (FBSMC)
   
The robot starts at a predefined position (X = 0, Y = 0, heading angle = ) and follows the trajectory using real-time velocity commands generated by the controllers. Both methods are compared in terms of tracking accuracy, robustness, and computational efficiency. Data collected during the execution, including actual poses and errors, are logged in an Excel file for analysis. 
Results are visualized as plots, showing the reference trajectory, the robot's actual path with both controllers. The project demonstrates effective trajectory tracking, with comparisons highlighting the strengths of each control method for handling nonlinear dynamics.

### Mathematical Formulation of the Desired Trajectory
The 8-shaped trajectory is generated using parametric equations, defining the desired position, velocity, and acceleration at any given time \( t \). These values are used for accurate trajectory tracking by the controllers.

#### Target Trajectory
The desired position of the robot along the $x$- and $y$-axes is defined as:
- $x_{\text{target}} = A \cdot \sin(\omega \cdot t)$
- $y_{\text{target}} = B \cdot \sin(2 \cdot \omega \cdot t)$

**Variables:**
- $A$: Amplitude constant that defines the size of the trajectory along the $x$-axis.
- $B$: Amplitude constant that defines the size of the trajectory along the $y$-axis.
- $\omega$: Angular velocity that controls the speed of traversal.
- $t$: Time variable.

#### First Derivative (Velocity)
The velocity components along the $x$- and $y$-axes are given by:
- $\dot{x}_{\text{target}} = A \cdot \omega \cdot \cos(\omega \cdot t)$
- $\dot{y}_{\text{target}} = 2 \cdot B \cdot \omega \cdot \cos(2 \cdot \omega \cdot t)$

These represent the desired linear velocities of the robot.

#### Second Derivative (Acceleration)
The acceleration components for the trajectory are derived as:
- $\ddot{x}_{\text{target}} = -A \cdot \omega^2 \cdot \sin(\omega \cdot t)$
- $\ddot{y}_{\text{target}} = -4 \cdot B \cdot \omega^2 \cdot \sin(2 \cdot \omega \cdot t)$

These values are used to refine control inputs and ensure smooth motion tracking.

##### Purpose
These equations are implemented in the trajectory tracking code, allowing the controllers (e.g., FBTC and FBSMC) to calculate the necessary control inputs for precise 8-shaped trajectory following by the TurtleBot. The dynamic computation of motion parameters ensures accuracy and robustness during real-time execution.

## Flatness-Based Trajectory Controller (FBTC)
FBTC is a control approach that leverages the differential flatness property of dynamic systems. In FBTC, the system’s states and inputs are expressed in terms of flat outputs and their derivatives. This method allows for the generation of feasible trajectories and simplifies the design of control laws, as trajectory planning and tracking can be decoupled. FBTC is particularly effective for systems like mobile robots, where precise trajectory tracking, such as following an 8-shaped path, is required.

## Flatness-Based Sliding Mode Controller (FBSMC)
FBSMC combines the principles of flatness-based control with sliding mode control (SMC) to achieve robust trajectory tracking. While flatness-based control simplifies trajectory planning, sliding mode control enhances robustness by handling uncertainties and disturbances. In FBSMC, a sliding surface is defined based on the flat outputs, ensuring that the system states converge to the desired trajectory even in the presence of external disturbances or model uncertainties. This approach is well-suited for applications requiring both precision and robustness, such as mobile robots navigating complex paths.

# Robot's Pose data
While the robot is following the 8 shape trajectory, its position and orientation data are continuously recorded in a .csv file. This stored data is later utilized to do the comparison of FBTC and FBSMC.
The table below displays some of the logged data obtained from the real Turtlebot3 while the FBSMC controller was in operation. This data includes various parameters such as time, position, orientation, velocity, and angular velocity, which are essential for analyzing the performance of the trajectory-following task.

| Time (s) | x                    | y                     | Theta (radians)       | Theta (degrees) | Linear Velocity (v)                  | Angular Velocity (Omega)            |
|----------|----------------------|-----------------------|-------------|-----------------|--------------------|------------------|
| 0.133758 | 0.0011067477753385901 | -7.501553045585752e-05 | -1.1332132763832972 | -64.92833802495501 | 0.08943836647059063 | 0.03092362431270873 |
| 0.167218 | 0.0011067477753385901 | -7.501553045585752e-05 | -1.1331551730380127 | -64.92500894849462 | 0.08943591655312741 | -0.07375626358991658 |
| 0.200366 | 0.0011067477753385901 | -7.501553045585752e-05 | -1.1331551730380127 | -64.92500894849462 | 0.0894329523006337 | -0.07304968071611222 |
| 0.233720 | 0.0011067477753385901 | -7.501553045585752e-05 | -1.133194195079014 | -64.927244746752  | 0.08942943015010942 | -0.07189733229306967 |
| 0.267050 | 0.0011067477753385901 | -7.501553045585752e-05 | -1.1332190638622996 | -64.92866962307588 | 0.08942536992247803 | -0.07001932135079737 |


# Running the Simulation
Run the following commands on a new terminal:
  ```bash
  source devel/setup.bash
  roslaunch trajectory_control_pkg trajectory_following.launch
  ```
* Remember to run the above commands inside the workspace

# MATLAB-Based Comparison of Controllers

As part of this project, a detailed performance comparison was conducted between the two implemented controllers: **FBTC (Flatness-Based Trajectory Control)** and **FBSMC (Flatness-Based Sliding Mode Control)**. The analysis was carried out using MATLAB to evaluate key performance metrics based on trajectory tracking accuracy, robustness, and response to disturbances.

### Performance Metrics Evaluated
1. Tracking Accuracy:
   - The deviation of the actual robot trajectory from the reference 8-shaped trajectory was computed for both controllers.
   - The plots in MATLAB are created using the logged data from hardware.

2. Robustness to Disturbances:
   - The controllers were tested under external disturbances.
   - FBSMC showed better disturbance rejection due to its inherent robustness from sliding mode control.


### Key Observations
- **FBTC**:
  - Provided smooth and precise tracking under nominal conditions.
  - Less effective in the presence of external disturbances.

- **FBSMC**:
  - Demonstrated strong robustness to disturbances, maintaining trajectory tracking even under adverse conditions.
  - Introduced chattering due to sliding mode behavior.

### MATLAB Visualization
The following plots were generated using MATLAB for both controllers:
1. Trajectory Tracking:
   - Overlay of the reference trajectory and the actual trajectory for FBTC and FBSMC.
2. Control Inputs:
   - Visualization of linear and angular velocities applied by the controllers.
3. Comparison of $\theta$ (Heading Angle):
   - Comparison of the robot's heading angle ($\theta$) over time using both controllers

#### Quantitative Comparison between FBTC and FBSMC

| **Metric**                   | **FBTC** | **FBSMC** |
|------------------------------|----------|-----------|
| **IAE**                      | 8.2070   | 6.0114    |
| **RMSE**                     | 0.2855   | 0.2228    |
| **Average Error (avgp)**     | 0.0118   | 0.0144    |


These results showcase the trade-offs between the two controllers and provide insights into selecting the appropriate control method based on application requirements.

# Hardware Testing
![Setup](https://github.com/EhtishamAshraf/TurtleBotTrajControl_SMC/blob/7218680308a7305bf3b7cf842722acf0856db109/2-Hardware_Data/Images/Experimental%20Setup.jpg)

Before transitioning to real hardware testing with the TurtleBot, ensure that all necessary setup steps are completed. This section provides an overview of key configurations and usage instructions.

1.  Turn on the Turtlebot3.
2.  Connect your laptop and TurtleBot3 to the same Wi-Fi network.
    * Verify the TurtleBot's IP address via SSH
    * If you would like to use a new wifi which hasn't been configured in turtlebot3 so far then follow the following steps:
      1.  Open the following file and add the new wifi and password: `sudo nano -ET4 /etc/netplan/50-cloud-init.yaml`
      
3.  ROS Network Setup:      
  A. Open the `.bashrc` File:
   - Use the `nano` editor to open the `.bashrc` file on both the TurtleBot and your laptop:
     ```bash
     nano ~/.bashrc
     ```

  B. Update the ROS Environment Variables:
   - Add the following lines to the `.bashrc` file **on the TurtleBot**:
     ```bash
     export ROS_MASTER_URI=http://<pc-ip>:11311
     export ROS_HOSTNAME=<turtlebot-ip>
     ```
   - Add the following lines to the `.bashrc` file **on the laptop**:
     ```bash
     export ROS_MASTER_URI=http://<pc-ip>:11311
     export ROS_HOSTNAME=<pc-ip>
     ```

   Replace the placeholders:
   - `<pc-ip>`: The IP address of your laptop.
   - `<turtlebot-ip>`: The IP address of your TurtleBot.

  C. Save and Exit:
   - Press `CTRL+O` to save the changes and `CTRL+X` to exit the editor.

  D. Source the Updated `.bashrc` File:
   - Run the following command to apply the changes:
     ```bash
     source ~/.bashrc
     ```
## Running ROS on TurtleBot3 and Laptop

1. Run `roscore` on the Laptop (ROS Master):
   - On your laptop, start the ROS core:
     ```bash
     roscore
     ```

2. SSH into the TurtleBot:
   - From your laptop, SSH into the TurtleBot:
     ```bash
     ssh ubuntu@<turtlebot-ip>
     ```
   - Replace `<turtlebot-ip>` with the TurtleBot's IP address and enter the password when prompted.

3. Launch TurtleBot Bringup:
   - On the TurtleBot, launch the bringup file to initialize the robot:
     ```bash
     roslaunch turtlebot3_bringup turtlebot3_robot.launch
     ```

4. Test Communication:
   - Verify the TurtleBot is communicating with your laptop:
     ```bash
     rostopic list
     ```

---

#### Checking TurtleBot Movement

Once the above steps are completed, you can test your TurtleBot's hardware functionality:

1. Test Using Teleop:
   - On your laptop, run the teleoperation node to control the TurtleBot manually:
     ```bash
     rosrun turtlebot3_teleop turtlebot3_teleop_key.launch
     ```

2. Hardware Testing:
   - Run your trajectory nodes or the test scripts provided in the repository for straight-line or circular movement to ensure proper functioning of the TurtleBot.

After following these steps, the TurtleBot should be fully configured and operational in the real-world environment!

# Running the Hardware
After following the steps 1 - 3 of the section *Running ROS on TurtleBot3 and Laptop*, run the following command (on a new terminal) to run FBTC and FBSMC respectively.
  ```bash
  rosrun trajectory_control_pkg FBTC_8_shape.py
  ```
  ```bash
  rosrun trajectory_control_pkg FBSMC_8_shape.py
  ```

# Check Robot Movement
The `trajectory_control_pkg` also includes three essential nodes to verify the robot's proper connection and functionality. These nodes allow you to test straight-line movement, circular movement, and adjust the robot's heading angle. These features help ensure the robot is correctly connected and responding as expected before running more complex control algorithms.

The figure below illustrates the circular trajectory followed by the robot during its movement:

#### Parametric Equations for Circular Trajectory
For the robot to follow a circular trajectory, the desired position along the $x$- and $y$-axes is given by the following parametric equations:

- ${\text{XdesPos}} = \text{radius} \cdot \cos(\text{omega} \cdot t)$  
- ${\text{YdesPos}} = \text{radius} \cdot \sin(\text{omega} \cdot t)$  

The velocity components along the $x$- and $y$-axes are calculated as:

- $Vx = -\text{radius} \cdot \text{omega} \cdot \sin(\text{omega} \cdot t)$  
- $Vy = \text{radius} \cdot \text{omega} \cdot \cos(\text{omega} \cdot t)$  

##### Explanation:
- Radius: Determines the size of the circular path.
- Angular Velocity: Controls how quickly the robot moves along the circular trajectory.
- $time (t)$: Represents the time variable.


# Clone the repository
Create a folder in your laptop and run the following commands
```bash
sudo apt-get update
```
```bash
sudo apt-get install git
```
```bash
git clone https://github.com/EhtishamAshraf/TurtleBotTrajControl_SMC.git
```
```bash
cd TrajectoryFollowing_ws
```
Run the below commands in root folder of the workspace
```bash
catkin_make 
```
```bash
source devel/setup.bash 
```
Navigate to the src folder inside the package and make the Python files executable by running the following command:
```bash
chmod +x *.py
```
There are multiple Python scripts located in the src folder:
1. This script is responsible for trajectory tracking with FBTC while simultaneously saving the robot's pose data.
```bash
FBTC_8_shape.py
```
2. This script is responsible for trajectory tracking with FBSMC while simultaneously saving the robot's pose data.
```bash
FBSMC_8_shape.py
```

