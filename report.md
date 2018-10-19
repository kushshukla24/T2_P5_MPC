# **Model Predictive Control for Self Driving Car** 

---

**MPC Project**

The autonomous part of the self-driving cars is to predict the trajectory and control itself through steering and speed actuators.

The goal of this project is to navigate the track (provided through Udacity Simulator) autonomously with MPC controller.


[//]: # (Image References)

[image1]: kinematic_equations.png "Equations"
[video1]: ./Videos/12.gif "Proportional"

---
## MPC Controller

**MPC** stands for **Model-Predictive-Control**. The **MPC Controller** has the ability to predict the future state of the vehicle and take control actions accordingly.

## Model
In this project, we implement a kinematic model, which descibes the vehicle state through following parameters:
- position expressed through x and y co-ordinate (x,y), 
- orientation angle through angle (psi), 
- velocity (v),
- cross-track error (cte),
- orientation error (epsi).

 and outputs the actuator controls through acceleration (a) and steering angle (delta).
 
The model combines the state and actuator controls from previous time step to anticipate the current timestep state based on the equations below:

![alt text][image1]

## Number of Timestep and Spacing between the Timesteps
The values **N** (number of timesteps) and **dt** (spacing between the timesteps) are important parameters that leads to decide ***T = N * dt*** prediction horizon of the vehicle. For this project, we chose N = 10 and dt = 0.1, with following pointers in mind:

- large dt result in less frequent actuations, which in turn could result in the difficulty in following a continuous reference trajectory (so called discretization error)
- despite the fact that having a large T could benefit the control process, consider that predicting too far in the future does not make sense in real-world scenarios.
- large T and small dt lead to large N. As mentioned above, the number of variables optimized is directly proportional to N, so will lead to an higher computational cost.

## Polynomial Fitting and MPC Preprocessing
The simulator provides the waypoints co-ordinates in the global reference system. As a preprocessing step, we transformed the waypoints to vehicle co-ordinate system. This approach helped the process of fitting the polynomial to the waypoints.

## Model Predictive Control with Latency
To deal with the latency, which is 100ms equivalent to our dt, the state of the vehicle is predicted one timestep ahead before feeding it to the solver.

## MPC in Action
![alt text][video1]

Credits:
https://github.com/ndrplz/self-driving-car/tree/master/project_10_MPC_control

