# Obstacle Avoiding Car using Arduino Uno

An autonomous obstacle-avoiding robot built with Arduino Uno, an ultrasonic sensor mounted on a servo, and an L298N motor driver. The car continuously scans the path ahead, detects obstacles in real time, and intelligently decides whether to turn left, right, or reverse and U-turn based on available space.

## Features

- Real-time obstacle detection using ultrasonic sensing
- Servo-mounted sensor to scan left and right before deciding direction
- Smart decision-making: compares left vs right clearance and picks the path with more space
- Reverse and U-turn handling when both sides are blocked
- Re-validation after turning to confirm the new path is actually clear
- Fully autonomous — no remote or manual control required

## Components Used

| Component | Quantity |
|---|---|
| Arduino Uno | 1 |
| HC-SR04 Ultrasonic Sensor | 1 |
| SG90 Servo Motor | 1 |
| L298N Motor Driver Module | 1 |
| BO Motors (DC Gear Motors) | 4 (2 pairs) |
| Robot Chassis with Wheels | 1 |
| Battery Pack (7.4V–12V) | 1 |
| Jumper Wires | As required |

## Working Principle

The ultrasonic sensor measures distance by emitting a sound pulse and timing how long it takes to bounce back from an object. This distance is calculated using the standard formula `distance = (duration × speed of sound) / 2`.

The Arduino continuously checks the distance to the nearest obstacle directly ahead. If the path is clear (distance greater than a defined threshold), the car moves forward. If an obstacle is detected within the threshold, the car stops, reverses slightly, and triggers the servo to sweep the ultrasonic sensor left and right to measure clearance on both sides. Based on which side has more open space, the car turns in that direction; if both sides are blocked, it performs a U-turn. After turning, it re-checks the distance to confirm the new path is safe before resuming forward motion.

## Methodology

1. Initialize all pins, attach the servo, and center it to face forward.
2. Continuously measure front distance using the ultrasonic sensor.
3. If distance > threshold → move forward.
4. If distance ≤ threshold → stop, reverse briefly, then:
   - Sweep servo to scan left, measure distance.
   - Sweep servo to scan right, measure distance.
   - Return servo to center.
5. Compare left and right readings:
   - Both blocked → reverse turn (U-turn).
   - Left more open → turn left.
   - Right more open → turn right.
6. After turning, re-measure distance to confirm clearance; if still blocked, correct by turning the opposite way.
7. Repeat the loop continuously.

## Assembly Overview

- Mount the two BO motor pairs on the chassis and connect them to the L298N driver's two output channels.
- Connect the L298N's ENA/ENB to PWM pins and IN1–IN4 to digital pins on the Arduino for speed and direction control.
- Mount the servo motor at the front of the chassis and attach the ultrasonic sensor on top of the servo horn so it can rotate to scan the surroundings.
- Connect the ultrasonic sensor's TRIG and ECHO pins to digital pins on the Arduino.
- Power the Arduino and motor driver using a separate battery pack, ensuring a common ground between the Arduino, battery, and L298N.
- (Circuit diagram to be added — see `circuit-diagram` in this repository.)

## Software Implementation

The firmware is written in Arduino C++ using the built-in `Servo` library for sensor sweeping and direct digital/PWM control for the L298N driver.

Key functions:
- `getDistance()` — triggers the ultrasonic sensor and calculates distance from echo duration.
- `forward()`, `backward()`, `leftTurn()`, `rightTurn()`, `stopMotors()` — control motor direction and speed via the L298N.
- `avoidObstacle()` — core decision-making routine that reverses, scans both sides, compares distances, and executes the appropriate turn.
- `loop()` — continuously checks the front distance and calls either `forward()` or `avoidObstacle()`.

The full source code is available in [`obstacle_avoiding_car.ino`](./obstacle_avoiding_car.ino).

## Future Improvements

- Add Bluetooth/Wi-Fi module for manual override and remote monitoring
- Implement PID-based speed control for smoother turns
- Add a buzzer/LED indicator for obstacle alerts
- Map and log obstacle data for path optimization

## Author

Built as a hands-on robotics and embedded systems project demonstrating sensor integration, real-time decision-making, and motor control with Arduino.
