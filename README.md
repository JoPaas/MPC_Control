# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Overview
This Model Predictive Controller takes a trajectory and controls a vehicle with arbitrary actuator delay to follow the trajectory with minimal cross track error.

## Project Rubric
### The Model
The vehicle state consists of position, course angle, velocity and cross track, as well as course angle error in relation to the target trajectory.
The output consists of steering angle and acceleration to control the cars lateral and longitudinal dynamics.

Here's a [link to my video result](https://github.com/Nervehurter/MPC_Control/blob/master/output_mpc.mp4)

The estimated trajectory over _N_ timesteps with _delta t_ as step size is calculated using single track model equations. In comparison to the [result of the PID control project](https://github.com/Nervehurter/PID_Control/blob/master/output.mp4), the MPC controls the vehicle much smoother eventhough the velocity is almost doubled.

### Timestep Length and Elapsed Duration (N & dt)
N was set to 10 and dt to 0.1, resulting in an outlook of one second. This was chosen by trial and on the educated guess that any motion after one second in the future would be too inaccurate to really improve the solution of the optimization.

### Polynomial Fitting and MPC Preprocessing
To make both calculations and visualization easier, the current trajectory was transformed in vehicle coordinated with the first point coinciding with the vehicle position and course angle. Then a polynomial of 3rd order is fitted.

### Model Predictive Control with Latency
To account for actuation latency the current vehicle state is extrapolated to the future by _latency t_. This way the returned actuation command is valid for _latency t_ seconds in the future. With this I was able to turn the latency up to 0.5s, at which point the trajectory matching fails. With the given 100ms latency the vehicle performs well.
