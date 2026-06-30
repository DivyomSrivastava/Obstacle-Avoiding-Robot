Obstacle Avoiding Car using Arduino Uno

An autonomous robot built with Arduino Uno, an ultrasonic sensor mounted on a servo, and an L298N motor driver. It scans the path ahead in real time and decides to move forward, turn, or reverse based on detected obstacles.

Features


Real-time obstacle detection using ultrasonic sensing
Servo-mounted sensor scans left/right to find the clearer path
Auto reverse + U-turn when both sides are blocked
Re-checks path after turning to confirm it's clear


Components Used

Arduino Uno, HC-SR04 Ultrasonic Sensor, SG90 Servo Motor, L298N Motor Driver, 4x BO Gear Motors, Robot Chassis, Battery Pack, Jumper Wires.

Working Principle

The ultrasonic sensor measures distance via echo timing (distance = duration × speed of sound / 2). If the front is clear, the car moves forward. If an obstacle is detected within the threshold, it stops, reverses, sweeps the servo to check left and right distances, then turns toward the side with more space (or U-turns if both are blocked). It re-verifies clearance after turning before resuming.

Methodology


Measure front distance continuously.
Move forward if clear; else stop and reverse.
Sweep servo left → right to measure side clearances.
Turn toward the more open side (or U-turn if both blocked).
Re-check distance after turning; correct if still obstructed.
Repeat.


Assembly Overview

Motors connect to the L298N driver, which is controlled by the Arduino (ENA/ENB for speed, IN1–IN4 for direction). The servo is mounted at the front with the ultrasonic sensor on top, allowing it to sweep and scan. Arduino and driver share a common ground, powered by a separate battery pack. (Circuit diagram to be added.)

Software Implementation

Written in Arduino C++ using the Servo library. Core functions: getDistance() for sensing, forward()/backward()/leftTurn()/rightTurn()/stopMotors() for motion control, and avoidObstacle() for the decision-making logic that drives the whole behavior.
