# Smart-Home-IoT-Control-System
Raspberry Pi based IoT Smart Room Control System with DHT11 sensing, PWM servo ventilation, keypad local control, ThingSpeak HTTP telemetry, and MQTT coordination.
## Overview
This project implements a Raspberry Pi–based IoT Smart Room Control System that integrates:
 Environmental sensing (DHT11 temperature & humidity)
 LED control using PWM
 Local control via 4×4 matrix keypad
 Push button event-driven control
 Automated ventilation using SG90 servo motor
 Cloud telemetry using ThingSpeak (HTTP)
 Device coordination using MQTT protocol
The system supports both local control and remote communication, demonstrating real-world IoT architecture.
# Features
## Environmental Monitoring
Reads temperature (°C) and humidity (%) from DHT11
Displays ISO timestamped readings
Sensor read interval: 2 seconds
Example output:
2025-05-24T14:32:05 | T=24.0°C | RH=52%
## LED Control (PWM Based)
GPIO17 used for LED control
PWM frequency: 100 Hz
Duty cycle controls brightness
Controlled via:
Keypad ('A' → ON, 'B' → OFF)
Push button (toggle, event-driven)
## Automated Ventilation (Servo Control)
SG90 servo motor on GPIO18
PWM frequency: 50 Hz
Temperature-based automation:
Condition	Action
T > 28°C	Open vent (90°)
T < 22°C	Close vent (0°)
Manual override via keypad:
'0' → Open vent
'1' → Close vent
## ThingSpeak Cloud Telemetry (HTTP)
Uploads temperature and humidity every 20 seconds
Uses Write API Key authentication
Data fields:
field1 → Temperature
field2 → Humidity
Implements:
HTTP GET requests
Response validation
Network error handling
## MQTT Coordination
MQTT broker: Local or public (HiveMQ)
Topic-based communication
Subscriber-based event handling
## Implemented features:
Network-wide safe mode (#2468#)
Remote humidity-based LED control
Publish/Subscribe architecture
## Hardware Components
Raspberry Pi
DHT11 sensor (GPIO4)
SG90 Servo motor (GPIO18)
LED + 330Ω resistor (GPIO17)
Push button (GPIO27, pull-up)
4×4 matrix keypad
Optional 5V fan (GPIO23 via transistor)
External 5V supply (servo/fan)
Common ground connection
## GPIO Pin Mapping (BCM Mode)
Component	GPIO
LED	17
Push Button	27
DHT11	4
Servo	18
Fan	23
Keypad Rows	5, 6, 13, 19
Keypad Columns	12, 16, 20, 21
## Communication Protocols Used
HTTP (ThingSpeak)
Used for cloud telemetry
Client-server architecture
API key authentication
MQTT
Publish/Subscribe model
Broker-based communication
Event-driven callback (on_message)
## Concepts Demonstrated
GPIO input/output configuration
Internal pull-up resistors
Matrix keypad scanning (polling)
Event-driven programming (interrupts)
PWM signal generation
Servo angle control via duty cycle
Cloud communication via HTTP
MQTT publish/subscribe model
Error handling and system robustness
## How to Run
Install dependencies:
pip install adafruit-circuitpython-dht requests paho-mqtt
Enable GPIO and I2C if required.
Run the desired script:
python3 task2_local_control.py

## Academic Context
This project was developed as part of:
HTU – Special Topics (IoT Solution System)
Learning Outcomes covered:
LO1: Hardware assembly and configuration
LO2: Raspberry Pi and Python IoT programming
LO3: IoT communication protocols (HTTP & MQTT)

## Future Improvements
Add mobile app dashboard
Implement TLS-secured MQTT (port 8883)
Add local database backup
Implement hysteresis to avoid servo oscillation

Integrate additional sensors
