# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program
   
## Write up

As taught by the course material and walkthrough. I broke the problem of car driving in three sub sections.

Predict -> Behave -> Drive

### Predict

The code can be found in `main.cpp` from line 179 to 257.
The target of the function is to use data from sensor motion and let the model of the following.
* Is present lane occupied by a car ahead.
* Is left lane free for a switch.
* Is right lane free for a switch.

For this, I use frenet coordinate system. The flow of function is as follows.
* For each car identified in sensor motion
   * identify in which lane it is present.
   * identify if it blocks any lane.
   * mark that lane as blocked if calculated that way.

A corner case that I handled was what happens when the lap is completed. In this case difference in s vector is in magnitude of lap length. Hence this has been taken care in line 204 to 210.

### Behave

The code can be found in `main.cpp` from line 260 to 293.
The target of the function if to use the predection from predict function and then determine switching of lane/changing speed.

The high level logic of function is.
* Check if present lane is blocked.
* If present lane is blocked
   * Check if any lane change is possible. If yes then change lane.
   * If lane change is not possible, slow down.
* If present lane is not blocked. Speed up.

This is a very crude logic, however it makes the car complete the laps as required by project.


### Drive

One we know which car to drive in, things get very easy. The entire driving logic is present from line 294 to 394 in `main.cpp`
The method used is as follows.
* Crudely layout the checkpoints to be followed by car. This is done in `main.cpp` from line 298 to 349.
* Generate a spline curve using above crude points and get a smooth curve. Line 352 to 353 in `main.cpp`
* Generate fine points and push it to msgJson. `main.cpp` line 368 to 394.

*** 
