---
layout: post
title: Closed-loop driving assist for skid steer robots
---

Problem: I like fast robots

Problem: Fast robots are often difficult to control

Problem: I like fixing things in software.

Solution: Closed-loop driving.

There are certain maneuvers you perform as a driver to compensate for the behavior of the robot - pull back once you've hit your target to counteract inertia, sharply increase power at the beginning of the move to "kick" the robot into drive, react to other robots trying to turn your robot, etc. Using commonly available sensors, we can automatically do these compensations without the driver having to think twice. This makes the robot's drivetrain significantly more controllable, predictable, and intuitive to drive. 

A robot's motion can be described in one of two vectors - fwd/rev, and cw/ccw turning. This post will talk about closing the loop for cw/ccw turning but similar concepts can be used for fwd/rev.

# Setup

We'll be looking at the setup used on Gryffingear's offseason robot, [Nagini](https://www.youtube.com/watch?v=0BoCybF3fTw)

The relevant hardware setup is below:
* Drivetrain geared for 18ft/sec linear speed.
* Cross the Road Electronics [Pigeon IMU](http://www.ctr-electronics.com/gadgeteer-imu-module-pigeon.html)

Below is the code used on the robot. It is a P loop on the yaw rate of the drivetrain. It converts the driver's turning input into a yaw rate(turning speed) setpoint that a P controller will work to follow. 

~~~
double kSt = -0.00125;
double kP = 1.750;
double input = drivetrain.getRawRate() * kSt;

turning = kP * (turning - input);
~~~
{: .language-java}

`kSt` is a unit conversion to convert the data from the yaw rate sensor(gyro) to +/- 1.0 that the drive functions expect. In our setup, with the drivetrain in a full speed spin, we saw that the maximum yaw rate was about 800 degrees per second. The units on `kSt` are 1 / deg/sec, so 1/800 = 0.00125. This value is negative to counteract inertia's effect on robot turning. 

`kP` is a tuning constant. The higher this value, the more aggressive the turn assist loop behaves.

`input` is the drivetrain's yaw rate measurement scaled to +/- 1.0

`turning` is the turning command output. A simple P controller on the turning setpoint and yaw rate setpoint. 

`[insert video of performance]`

# Benefits

Overall, this technique has allowed our drivetrain to behave in a more predictable and intuitive manner. This can be ported to other mobile robotics applications. I plan on doing something similar on a combat robot drivetrain I've been working on. 


# Observed Issues

At Madtown Throwdown [SF1-2](https://www.thebluealliance.com/match/2017mttd_sf1m2), we encountered an issue where either `turning` or `input` weren't updating so we were stuck in a full turn condition until we were able to reboot the robot code. It worked as intended at the beginning of the match and again after the reboot, but we are unable to identify the root-cause of this failure mode at this time. One potential improvement would be to check if either value is updating as expected and to disable the control loop if necessary. A failure mode like this on most other robots could be catastrophic. 
