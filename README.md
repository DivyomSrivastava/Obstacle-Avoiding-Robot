# Obstacle Avoiding Car using Arduino Uno

An autonomous obstacle-avoiding robot built with Arduino Uno, an ultrasonic sensor mounted on a servo, and an L298N motor driver. The car continuously scans the path ahead, detects obstacles in real time, and intelligently decides whether to turn left, right, or reverse and U-turn based on available space.

## ✨ Features

- Real-time obstacle detection using ultrasonic sensing
- Servo-mounted sensor to scan left and right before deciding direction
- Smart decision-making: compares left vs right clearance and picks the path with more space
- Reverse and U-turn handling when both sides are blocked
- Re-validation after turning to confirm the new path is actually clear
- Fully autonomous — no remote or manual control required

## 🔩 Components Used

| Component | Quantity |
|---|---|
| Arduino Uno | 1 |
| HC-SR04 Ultrasonic Sensor | 1 |
| SG90 Servo Motor | 1 |
| L298N Motor Driver Module | 1 |
| BO Motors (DC Gear Motors) | 4 (2 pairs) |
| Robot Chassis with Wheels | 1 |
| 11.1V Li-Po Battery Pack | 1 |
| Jumper Wires | As required |

## ⚙️ Working Principle

The ultrasonic sensor measures distance by emitting a sound pulse and timing how long it takes to bounce back from an object. This distance is calculated using the standard formula `distance = (duration × speed of sound) / 2`.

The Arduino continuously checks the distance to the nearest obstacle directly ahead. If the path is clear (distance greater than a defined threshold), the car moves forward. If an obstacle is detected within the threshold, the car stops, reverses slightly, and triggers the servo to sweep the ultrasonic sensor left and right to measure clearance on both sides. Based on which side has more open space, the car turns in that direction; if both sides are blocked, it performs a U-turn. After turning, it re-checks the distance to confirm the new path is safe before resuming forward motion.

### Navigation Logic

```
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
```

## 🛠 Methodology

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

## 🔌 Block Diagram

```
<img width="2720" height="2480" alt="obstacle_car_block_diagram" src="https://github.com/user-attachments/assets/9234e9f1-c6ba-4260-a0fb-3cc784db4030" />

```

The entire system runs on an **11.1V battery pack**, stepped down via a buck converter to power the Arduino Uno and logic circuitry. The Arduino reads input from the ultrasonic sensor (positioned via the servo) and sends direction commands to the L298N motor driver, which drives the two DC motor pairs directly from the 11.1V supply.

## 📷 Circuit Diagram

*(Add circuit diagram image here)*

## 🤖 Robot Image

*(Add robot image here)*

## 💻 Software Implementation

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
