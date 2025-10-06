# Arduino Suction Gripper Control

This repository contains the code and resources for controlling a suction gripper using an Arduino microcontroller. The project includes various firmware versions and Python scripts for different control methods, offering a flexible solution for robotics and automation projects.

## Project Overview

The core of this project is an Arduino-based system for operating a suction gripper. The gripper's pump and valve are controlled through different electronic components, including servos and relays. The repository provides several Arduino sketches tailored for specific hardware setups and control logic.

Control can be managed from a host computer (like a Raspberry Pi) using different communication protocols, including:
- **Direct GPIO control** from a Raspberry Pi.
- **Serial communication** over USB.
- **I2C communication**.

## Hardware Requirements

- **Arduino Board:** (e.g., Arduino Uno, Nano)
- **Suction Gripper:** A standard robotic suction gripper with a vacuum pump.
- **Raspberry Pi:** (Optional, for GPIO or I2C control)
- **Relay Module:** For controlling the power to the suction pump.
- **Servo Motor(s):** For mechanical actuation in some of the gripper designs.
- **Jumper Wires and Breadboard**

## Firmware

This repository contains several Arduino sketches (`.ino` files), each with a specific purpose:

- **`aruduino_suction_gripper/aruduino_suction_gripper.ino`**: The primary sketch for controlling the suction gripper. It uses a servo and a digital output pin, and is controlled via the "RUN" command over serial.

- **`relay/relay.ino`**: A simpler sketch designed to control a relay connected to a pump. It accepts "RUN" and "STOP" commands via serial to turn the pump on and off.

- **`sketch_jul09a/sketch_jul09a.ino`**: A more complex sketch that controls two servo motors in a coordinated sequence, triggered by the "RUN" command over serial.

- **`orginal_slave_master_code/orginal_slave_master_code.ino`**: An early, simplified version for basic control of a device on pin 13. It is likely a prototype and less stable than the other versions.

## Control Scripts

The `arduino/` directory contains Python scripts for controlling the gripper from a Raspberry Pi:

- **`grippes_test.py`**: A script for direct control of the suction pump and an air valve using the Raspberry Pi's GPIO pins. This script does not require an Arduino.

- **`ide_gripper_test.py`**: A script that communicates with the Arduino over I2C. It sends a character ('A') to the Arduino to trigger an action. This requires the Arduino to be running a compatible I2C slave sketch.

## Getting Started

1.  **Choose a Firmware:** Select the Arduino sketch that best fits your hardware setup and upload it to your Arduino board using the Arduino IDE.

2.  **Hardware Setup:** Connect your suction gripper, relay, and/or servos to the Arduino according to the pin definitions in the chosen sketch.

3.  **Control Method:**
    *   **For Serial Control:** Use the Arduino IDE's Serial Monitor or a custom script to send commands (e.g., "RUN", "STOP") to the Arduino.
    *   **For GPIO Control (Raspberry Pi):** Connect the pump and valve directly to the Raspberry Pi's GPIO pins and run the `grippes_test.py` script.
    *   **For I2C Control:** Connect the Raspberry Pi and Arduino via their I2C pins (SDA and SCL) and run the `ide_gripper_test.py` script. Ensure the Arduino is loaded with an I2C-compatible sketch.

## Dependencies

- **Arduino:**
  - `Servo.h`: A standard Arduino library for controlling servo motors. Installable from the Arduino IDE's Library Manager.

- **Python (on Raspberry Pi):**
  - `RPi.GPIO`: For direct GPIO control.
  - `smbus2`: For I2C communication.

You can install the Python dependencies using pip:
```bash
pip install RPi.GPIO smbus2
```