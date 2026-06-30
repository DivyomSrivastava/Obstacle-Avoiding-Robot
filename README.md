# Obstacle-Avoiding-Robot
📖 Project Overview

This project demonstrates a 4WD autonomous obstacle-avoiding robot built using an Arduino Uno, L298N motor driver, HC-SR04 ultrasonic sensor, and an SG90 servo motor. The robot continuously monitors the path ahead and navigates around obstacles by scanning both the left and right directions to determine the safest route.


✨ Features

Autonomous obstacle detection and avoidance.
4WD differential drive system.
Real-time distance measurement using an ultrasonic sensor.
Servo-based left and right environmental scanning.
Intelligent path selection based on available space.
Automatic reverse before changing direction.
Modular and easy-to-understand Arduino code.
Low-cost and expandable design.


🛠 Methodology

The robot continuously moves forward while measuring the distance to obstacles using the ultrasonic sensor.

When an object is detected within the predefined threshold (15 cm), the robot:

Stops immediately.
Moves backward slightly.
Rotates the ultrasonic sensor to scan the left and right sides.
Compares the measured distances.
Turns toward the direction with more free space.
Continues moving forward.

This process repeats continuously, allowing the robot to navigate autonomously.


🔩 Components Used
| Component                 |   Quantity  |
| ------------------------- | :---------: |
| Arduino Uno               |      1      |
| L298N Motor Driver        |      1      |
| HC-SR04 Ultrasonic Sensor |      1      |
| SG90 Servo Motor          |      1      |
| BO DC Gear Motors         |      4      |
| Robot Chassis             |      1      |
| Wheels                    |      4      |
| Li-ion Battery Pack       |      1      |
| Jumper Wires              | As Required |


⚙️ Working Principle

The Arduino continuously receives distance measurements from the ultrasonic sensor. When no obstacle is detected, the robot moves forward.

If an obstacle is detected within the set distance, the robot reverses slightly and scans both sides using the servo-mounted ultrasonic sensor. After comparing the available space on the left and right, it turns toward the clearer path and resumes forward movement.

This simple decision-making process enables autonomous navigation in indoor environments.


💻 Software Implementation

The robot is programmed using the Arduino IDE in Embedded C++.

Main Software Modules:
1. Motor Control
2. Ultrasonic Distance Measurement
3. Servo Position Control
4. Obstacle Detection
5. Path Selection Logic
6. Autonomous Navigation

Navigation Logic

Move Forward
      │
Obstacle Detected?
      │
 ┌────┴────┐
 │         │
No        Yes
 │         │
 ▼         ▼
Continue  Stop
           │
           ▼
     Reverse Slightly
           │
           ▼
     Scan Left & Right
           │
           ▼
   Select Clearer Path
           │
           ▼
      Turn & Continue


      
