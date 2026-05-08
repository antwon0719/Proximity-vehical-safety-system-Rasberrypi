# Proximity-Based Vehicle Safety System

Embedded vehicle safety prototype using ultrasonic sensing, servo scanning, and real-time LED/buzzer feedback built with a Raspberry Pi Pico and MicroPython.

**Status:** Completed  
**Context:** Northeastern University Cornerstone Engineering Project (Team-based)  
**My Role:** Embedded programming, LED feedback logic, hardware integration, debugging  

---

## Overview

This project is a microcontroller-based vehicle safety system designed to improve driver awareness in confined environments. The system uses ultrasonic sensors mounted on servo motors to scan the surrounding area and provide real-time visual and audio alerts when nearby objects are detected.

The project combines embedded programming, hardware integration, and enclosure prototyping into a fully functional prototype.

---

## What it does

The system continuously scans the area around a vehicle using ultrasonic sensors attached to rotating servo motors. The Raspberry Pi Pico processes the distance data and determines if nearby objects are within predefined danger thresholds.

As objects get closer:
- LED brightness increases
- Buzzer alert frequency increases

This creates a real-time warning system that improves environmental awareness and collision avoidance.

---

## Demo Video

[Project Demo Video](PASTE-YOUR-VIDEO-LINK-HERE)

---

## Hardware

| Component | Quantity | Purpose |
|---|---|---|
| Raspberry Pi Pico | 1 | Main microcontroller |
| Ultrasonic Sensors | 2 | Distance detection |
| Servo Motors | 2 | Rotates sensors for wider scanning |
| LEDs | Multiple | Visual alert system |
| Buzzer | 1 | Audio warning system |
| Breadboard + Wiring | — | Circuit connections |

---

## Software architecture

```text
[Ultrasonic Sensors] → [Distance Processing + Threshold Logic] → [LED + Buzzer Output]
                                      ↓
                              [Servo Scan Control]
```

- Ultrasonic sensors collect distance measurements
- Raspberry Pi Pico processes real-time sensor data
- Threshold logic determines warning intensity
- Servo motors rotate sensors for wider detection coverage
- LEDs and buzzer provide visual and audio feedback

---

## Development Progress

### Early LED Testing

Initial LED brightness testing using MicroPython before sensor integration.

![LED Test](docs/led_test.jpg)

---

### Sensor + LED Integration

Combined ultrasonic sensor data with LED output logic.

![Sensor Setup](docs/sensor_setup.jpg)

---

### Wiring Setup

Initial breadboard prototype integrating sensors, servos, buzzer, and LED system.

![Wiring](docs/wiring.jpg)

---

### Enclosure Prototype

Early enclosure iteration for mounting hardware components.

![Enclosure V1](docs/enclosure_v1.jpg)

---

### Updated Enclosure

Redesigned enclosure with servo openings and buzzer placement.

![Enclosure V2](docs/enclosure_v2.jpg)

---

### Final Prototype

Completed prototype with integrated scanning and alert system.

![Final Build](docs/final_build.jpg)

---

## Key files

- `main.py` — Main control loop and full system integration
- `sensor.py` — Distance measurement logic
- `led.py` — LED brightness and threshold logic
- `servo.py` — Servo scanning control
- `buzzer.py` — Audio alert logic
- `config.py` — Threshold values and constants

---

## My specific contributions

### Primary responsibility: LED feedback system + threshold logic

- Programmed LED brightness control using MicroPython
- Designed a system where LED brightness increases as objects get closer
- Implemented threshold-based feedback using real-time distance sensor data
- Tested multiple LED configurations (constant, blinking, variable brightness)
- Integrated LED system with sensor and servo functionality
- Helped debug hardware/software inconsistencies

### Engineering decisions

- Avoided blinking LED due to overstimulation when combined with buzzer
- Chose brightness-based feedback for smoother user experience

### Collaboration work

- Worked with teammates to merge separate code components
- Assisted with hardware integration and debugging

---

## Example code (LED brightness logic)

```python
from picozero import DistanceSensor, LED
from time import sleep

dist = DistanceSensor(echo=14, trigger=15)
led = LED(15)

while True:
    distance_cm = dist.distance * 100

    if distance_cm < 100:
        brightness = max(0, min(1, 1 - (distance_cm / 100)))
        led.value = brightness
    else:
        led.off()

    sleep(0.1)
```

---

## Results

The system successfully detected nearby objects and provided real-time visual and audio alerts.

### Metrics

- Detection range: ~5 cm to 150 cm
- Response time: < 1 second per scan cycle
- Reliable short-range detection performance
- Functional real-time scanning prototype

---

## Known limitations

- Ultrasonic sensors can be inconsistent on angled/soft surfaces
- Sensor interference occasionally occurred during simultaneous scans
- Servo placement occasionally caused sensor collisions
- Environmental interference affected long-distance accuracy

---

## Challenges and what I did about them

### Challenge 1 — Inconsistent sensor readings

Sensor values fluctuated due to signal noise and timing inconsistencies.

**Solution:**  
Implemented averaging and delays between sensor measurements to improve stability.

---

### Challenge 2 — Sensor interference

Multiple sensors occasionally interfered with one another during scanning.

**Solution:**  
Sequential scanning logic was implemented to reduce overlap.

---

### Challenge 3 — Hardware integration

It was difficult determining whether issues were caused by hardware or software.

**Solution:**  
Components were tested individually before full system integration.

---

### Challenge 4 — LED feedback usability

Blinking LEDs became distracting when combined with buzzer alerts.

**Solution:**  
Replaced blinking with distance-based brightness control.

---

## What I learned

- Embedded programming with MicroPython
- Real-time sensor processing
- Hardware/software debugging
- Servo motor integration
- Team collaboration during engineering design
- Importance of iterative prototyping and testing

---

## Getting started

### Requirements

- Raspberry Pi Pico
- MicroPython firmware
- Thonny IDE
- Ultrasonic sensors
- Servo motors
- LEDs
- Buzzer

---

## Setup

```bash
git clone https://github.com/YOUR-USERNAME/proximity-vehicle-safety-system.git

cd proximity-vehicle-safety-system
```

1. Upload code to Raspberry Pi Pico using Thonny
2. Connect hardware according to wiring setup
3. Run `main.py`

---

## Running it

- Power the Raspberry Pi Pico
- System automatically begins scanning
- LED brightness and buzzer frequency respond to nearby objects

---

## Repository structure

```text
/src        # Source code
/docs       # Images/videos/documentation
/hardware   # Wiring diagrams and hardware info
README.md   # Project documentation
