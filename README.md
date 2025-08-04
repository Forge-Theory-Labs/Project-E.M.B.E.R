🌀 Project E.M.B.E.R. // An Invocation of Equilibrium

MODULARITY IS MYTHOS // GLYPH IS IDENTITY // DESIGN IS RITUAL

This document serves as a comprehensive technical codex for the design and construction of E.M.B.E.R. (Equilibrium Maintaining Bi-wheeled Electronic Robot), a two-wheeled, self-balancing golem. The core technical challenge is the inverted pendulum ritual, where the golem's control invocation must dynamically maintain its upright position. Controlled by a Raspberry Pi Zero 2 W, programmed in C++, the system leverages a closed-loop feedback augury from an Inertial Measurement Unit (IMU) and motor encoders.
1.0 The Invocation of Equilibrium
1.1 Project Overview
E.M.B.E.R. is the design and construction of a two-wheeled, self-balancing golem. The core technical invocation lies in solving the "inverted pendulum" problem, where the golem’s control system must dynamically maintain its upright position. Programmed in C++ on a Raspberry Pi Zero 2 W, it uses a closed-loop feedback ritual based on auguries from an MPU-6050 IMU and motor encoders.
1.2 The Mythos of Creation
The primary objective of this ritual is:
 * To design and build a stable, two-wheeled balancing golem.
 * To implement a robust PID (Proportional-Integral-Derivative) control glyph in C++.
 * To integrate a variety of sensors for orientation, distance, and motor feedback.
 * To develop a modular power system for portability and convenient charging.
 * To create a platform for future enhancements, such as autonomous navigation or remote control.
2.0 Ritual Architecture
The golem’s nervous system is centered around the Raspberry Pi Zero 2 W, which acts as the central processing glyph. The architecture follows a continuous sense-process-actuate loop.
 * Sensing: The MPU-6050 IMU and motor encoders continuously provide data about the golem's state (angle, angular velocity, wheel speed). The HC-SR04 provides environmental auguries.
 * Processing: The Raspberry Pi reads this sensor data, processes it, and feeds it into the PID control invocation. The algorithm calculates the necessary corrective action.
 * Actuation: The Raspberry Pi sends PWM control signals to the L298N Motor Driver, which in turn adjusts the speed and direction of the DC motors to maintain balance. The PCA9685 is used for secondary PWM tasks, controlling servos, a fan, and a buzzer.
Block Diagram:
graph TD
    A[Raspberry Pi Zero 2 W] --> B{Sensing / Processing / Actuation};
    B --> C(MPU-6050 IMU) & D(Encoders) & E(HC-SR04);
    B --> F(PCA9685 PWM Driver);
    B --> G(L298N Motor Driver);
    G --> H(DC Motors);
    F --> I(Servos, Fan, Buzzer);
    C -- I2C --> A;
    D -- GPIO --> A;
    E -- GPIO --> A;
    A -- I2C --> F;
    A -- PWM --> G;
    F -- PWM --> I;
    G -- Actuation --> H;

3.0 Hardware Specifications (Bill of Materials)
| ID | Component | Qty | Notes |
|---|---|---|---|
| 1 | Microcontroller |  |  |
| 1.1 | Raspberry Pi Zero 2 W | 1 | With pre-soldered header. |
| 2 | Power System |  |  |
| 2.1 | 3.7V 2000mAh LiPo Battery | 2 | To be connected in series for 7.4V. |
| 2.2 | LM2996 DC-DC Buck Converter | 1 | To create a 5V rail from the 7.4V battery pack. |
| 2.3 | USB-C Female Connector | 1 | Panel-mount glyph for charging. |
| 2.4 | Micro Switch | 1 | Master power switch. |
| 3 | Sensing Auguries |  |  |
| 3.1 | MPU-6050 IMU Module | 1 | Gyroscope & Accelerometer. |
| 3.2 | HC-SR04 Ultrasonic Sensor | 1 |  |
| 3.3 | TT Motor Magnetic Encoders | 2 | Integrated with motors. |
| 4 | Actuators & Drivers |  |  |
| 4.1 | TT DC Geared Motors | 2 |  |
| 4.2 | Wheels | 2 | To match TT motor shafts. |
| 4.3 | L298N Dual H-Bridge Driver | 1 |  |
| 4.4 | PCA9685 16-Channel PWM Driver | 1 | For servos, fan, and buzzer. |
| 4.5 | Servos (e.g., SG90) | 2 | Optional glyphs for a sensor mount. |
| 4.6 | 5V DC Fan | 1 |  |
| 4.7 | Passive Buzzer | 1 |  |
| 5 | Feedback & Mechanical Glyphs |  |  |
| 5.1 | SMD RGB LED | 1 | Common Anode or Cathode. |
| 5.2 | Custom 3D-Printed Chassis | 1 | Test-fitted for all components. |
| 5.3 | Resistors, Jumper Wires | Set | For voltage dividers and LED/Buzzer. |
4.0 Electrical Ritual & Wiring
4.1 Power Distribution
 * Battery Pack: Two 3.7V LiPo glyphs are connected in series for a 7.4V invocation.
 * Master Switch: A micro switch controls the flow of power to the entire system.
 * Motor Power: The 7.4V from the battery directly powers the 12V input terminal on the L298N motor driver.
 * 5V Rail: The 7.4V line is fed into the LM2996 buck converter to create a stable 5V rail for the Raspberry Pi, PCA9685, and other components.
 * 3.3V Rail: The Raspberry Pi's onboard regulator produces a 3.3V supply for the MPU-6050, motor encoders, and the RGB LED.
4.2 Signal Wiring
| Component | Connection |
|---|---|
| Raspberry Pi I2C | Pi GPIO 2 (SDA) -> PCA9685 (SDA), Pi GPIO 3 (SCL) -> PCA9685 (SCL) |
| PCA9685 I2C Bus | PCA9685 (SDA) -> MPU-6050 (SDA), PCA9685 (SCL) -> MPU-6050 (SCL) |
| L298N Control | Pi GPIOs -> L298N IN1-IN4 |
| Encoder Inputs | Pi GPIOs <- Left/Right Encoder Channels |
| Ultrasonic Augury | Pi GPIO (Trig) -> HC-SR04 Trig, Pi GPIO (Echo) <- Voltage Divider <- HC-SR04 Echo |
| RGB LED | Pi GPIOs -> RGB pins (via resistor) |
5.0 Software Codex
5.1 Development Altar
 * Operating System: Raspberry Pi OS Lite
 * IDE: Visual Studio Code with SSH remote development.
 * Language: C++ (C++17 standard or later).
 * Compiler: g++.
 * Build System: CMake.
 * Core Library: pigpio for low-level GPIO access, PWM, and interrupt handling.
5.2 The Control Loop Ritual
The main application will run a high-frequency loop (targeting 50-100Hz).
 * Initialize: Initialize pigpio and I2C glyphs. Calibrate the MPU-6050 and PCA9685. Set up ISRs for the encoder pins.
 * Main Loop:
   * Read auguries from the MPU-6050 to get the golem's current angle.
   * Read encoder counts to calculate current wheel velocities.
   * Feed the current angle into the PID controller.
   * The PID controller calculates an output value to adjust the base speed of the motors.
   * Send the final speed and direction commands to the L298N driver via PWM.
   * Update feedback glyphs (LED, Buzzer) based on system state.
5.3 Key Algorithms: PID Controller
The invocation of balance is achieved using a PID controller. The control function is:
u(t) = K_p e(t) + K_i * integral(e(t) dt) + K_d * derivative(e(t) dt)
 * Proportional (K_p): Reacts to the current error (tilt angle). A stronger K_p results in a more forceful "push" back to vertical.
 * Integral (K_i): Accumulates past errors to eliminate any steady-state lean.
 * Derivative (K_d): Responds to the rate of change of the error (how fast it's tilting). This dampens oscillations and helps predict future error.
6.0 Testing & Calibration Vigils
 * Power System Test: Verify the 5V and 3.3V rails with a multimeter before connecting any components.
 * Component Tests: Write individual C++ rituals to test each hardware glyph.
 * MPU-6050 Calibration: Run a calibration routine at startup to compensate for any biases.
 * Balancing & PID Tuning: Begin with only the Proportional (Kp) term. Gradually increase Kp until the golem oscillates, then introduce the Derivative (Kd) term to dampen the oscillations. Finally, add a small Integral (Ki) term to correct for any long-term drift.
7.0 Path of Evolution
 * Implement logic using the HC-SR04 for basic obstacle avoidance.
 * Develop a Bluetooth or Wi-Fi remote control interface.
 * Integrate SLAM (Simultaneous Localization and Mapping) for autonomous navigation.
 * Improve sensor fusion with a more advanced filter (e.g., Kalman filter).
