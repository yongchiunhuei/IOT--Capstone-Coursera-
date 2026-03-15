# 🥷 Shinobi Post Retrieval Rover: IoT Autonomous System
**University of California, Irvine | Programming for the Internet of Things**

![Status](https://img.shields.io/badge/Shinobi-Verified-black)
![License](https://img.shields.io/badge/Security-Master_Ninja-red)
![Platform](https://img.shields.io/badge/Platform-Raspberry_Pi-orange)

## 1. Project Overview
The **Shinobi Post Retrieval Rover** is an autonomous IoT solution designed for the "Aachen-Sanctuary." Its primary mission is the secure detection and notification of mail/package delivery. This project demonstrates the integration of mobile robotics with cloud-based telemetry and real-time edge processing.

* **Problem:** Manual mail checking is inefficient and lacks real-time security.
* **Solution:** A rover that monitors the post-box environment, detects proximity changes (delivery), and broadcasts encrypted status updates via MQTT.

---

## 2. System Architecture
The rover operates on a three-tier "Ninja" architecture:
* **The Brain (Edge):** Raspberry Pi 4 processing sensor data in real-time.
* **The Stealth Link (Network):** JSON payloads transmitted via **MQTT** over a secured WiFi bridge.
* **The Scroll (Application):** A remote monitoring dashboard for the Master Ninja Architect to track retrieval status.

---

## 3. Hardware Requirements
| Component | Ninja Designation | Purpose |
| :--- | :--- | :--- |
| **Raspberry Pi 4** | The Sensei | Core logic and gateway |
| **HC-SR04** | The Scout | Ultrasonic distance for obstacle/post detection |
| **DHT22** | The Climate Guard | Monitoring storage conditions (Temp/Humidity) |
| **L298N Driver** | The Kinetic Link | Controlling the rover's DC motors |
| **Buzzer** | The Alarm | Local audio feedback for system status |

---

## 4. Software Setup & Dependencies
The "Shinobi" logic is written in **Python 3.10**.

### Deployment
```bash
# Update the system
sudo apt-get update && sudo apt-get upgrade -y

# Install core IoT communication and hardware libraries
pip install paho-mqtt adafruit-circuitpython-dht RPi.GPIO
