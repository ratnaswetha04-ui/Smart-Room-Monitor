# Smart Room Monitor : IoT-Based Real-Time Environmental Monitoring System

 Ratna Swetha | 3rd Year ECE, Geethanjali College of Engineering and Technology

## Overview

Developed a real-time room monitoring system using ESP32 that integrates multiple sensors to track motion, distance, and air quality. Sensor data is displayed locally on a 16x2 LCD and simultaneously transmitted to the ThingSpeak cloud for remote monitoring and visualisation.

---
# Summary
 Wanted to bridge the gap between embedded systems knowledge and IoT cloud integration — having worked with ESP32 before but never transmitted live sensor data to a cloud platform.

 Design and implement a multi-sensor IoT system capable of real-time local display and cloud logging, simulated and validated before deploying on physical hardware.

- Integrated PIR, Ultrasonic, and MQ-2 sensors on ESP32, managing simultaneous sensor reads without blocking delays using `millis()` based timing
- Implemented I2C communication protocol for 16x2 LCD with cycling display logic across 3 data screens every 3 seconds
- Established WiFi connectivity and configured ThingSpeak API for cloud data push every 15 seconds using HTTP POST requests
- Validated the full system on the Wokwi simulator before deploying on real hardware, reducing hardware debugging time significantly

 Successfully deployed a fully functional IoT room monitor with a 
 live ThingSpeak dashboard showing real-time graphs for motion, distance, and gas levels — all sensors performing as expected on physical hardware.

---

## Technical Stack

| Category | Details |
|---|---|
| Microcontroller | ESP32 Dev Module |
| Communication Protocols | I2C (LCD), UART (Serial Debug), HTTP (ThingSpeak) |
| Cloud Platform | ThingSpeak (MathWorks) |
| IDE | Arduino IDE |
| Simulation | Wokwi Simulator |
| Libraries | LiquidCrystal_I2C, ThingSpeak, WiFi.h |

---

## Hardware

| Component | Purpose |
|---|---|
| ESP32 Dev Board | Main microcontroller + WiFi |
| HC-SR501 PIR Sensor | Motion detection |
| HC-SR04 Ultrasonic Sensor | Distance measurement |
| MQ-2 Gas Sensor | Air quality / gas detection |
| 16x2 LCD with I2C Module | Local real-time display |

---

## Key Implementation Details

**Non-blocking timing** — Used `millis()` instead of `delay()` to handle LCD refresh (every 3s) and cloud push (every 15s) simultaneously without freezing sensor reads.

**ADC Configuration** — MQ-2 connected to GPIO 34 (ADC1) on ESP32, which gives a 12-bit resolution (0–4095) for more precise gas level readings compared to the standard 10-bit Arduino ADC.

**I2C LCD** — Configured I2C bus on GPIO 21 (SDA) and GPIO 22 (SCL) with custom characters for motion and distance icons, cycling across 3 screens.

**WiFi Reconnection Handling** — Added a connection attempt limit with offline fallback mode so the system continues local LCD even if WiFi fails.

---

## ThingSpeak Dashboard

Live data visualisation at ThingSpeak with 3 channels:
- **Field 1** → Motion (binary: 0 or 1)
- **Field 2** → Distance (cm)
- **Field 3** → Gas Level (raw ADC value with classification)

---

## Development Workflow

1. Designed the circuit and identified the pin mapping
2. Tested each sensor individually with isolated test sketches
3. Simulated full system on **Wokwi** before touching hardware
4. Deployed on a real ESP32 and validated all sensors
5. Confirmed ThingSpeak cloud data transmission
6. Documented and pushed to GitHub

---

## Future Improvements

- Add DHT22 for temperature and humidity monitoring
- Implement buzzer alert when gas levels exceed threshold
- Push notifications to mobile when motion is detected
- Build a custom web dashboard instead of ThingSpeak
- Add deep sleep mode for battery-powered deployment


*3rd Year ECE Project — Geethanjali College of Engineering and Technology*
*Exploring Embedded Systems and IoT Cloud Integration*
