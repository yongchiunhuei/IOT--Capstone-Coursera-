'''
Shinobi Post Retrieval Rover: IoT Autonomous SystemUniversity of California, Irvine | Programming for the Internet of Things1. Project OverviewThe Shinobi Post Retrieval Rover is an autonomous IoT solution designed for the "Aachen-Sanctuary." Its primary mission is the secure detection and notification of mail/package delivery. This project demonstrates the integration of mobile robotics with cloud-based telemetry and real-time edge processing.Problem: Manual mail checking is inefficient and lacks real-time security.Solution: A rover that monitors the post-box environment, detects proximity changes (delivery), and broadcasts encrypted status updates via MQTT.2. System ArchitectureThe rover operates on a three-tier "Ninja" architecture:The Brain (Edge): Raspberry Pi 4 processing sensor data in real-time.The Stealth Link (Network): JSON payloads transmitted via MQTT over a secured WiFi bridge.The Scroll (Application): A remote monitoring dashboard for the Master Ninja Architect to track retrieval status.3. Hardware RequirementsComponentNinja DesignationPurposeRaspberry Pi 4The SenseiCore logic and gatewayHC-SR04The ScoutUltrasonic distance for obstacle/post detectionDHT22The Climate GuardMonitoring storage conditions (Temp/Humidity)L298N DriverThe Kinetic LinkControlling the rover's DC motorsBuzzerThe AlarmLocal audio feedback for system status4. Software Setup & DependenciesThe "Shinobi" logic is written in Python 3.10.Deployment:Bash# Install core IoT communication and hardware libraries
pip install paho-mqtt adafruit-circuitpython-dht RPi.GPIO
Configuration:MQTT Broker: mqtt.eclipseprojects.ioTopic: sanctuary/rover/post5. Circuit Schematic (Pin Mapping)The rover’s nervous system is mapped using BCM numbering:Ultrasonic (Scout): Trig: GPIO 23 | Echo: GPIO 24Climate (DHT22): Data: GPIO 4Alarm (Buzzer): Output: GPIO 18Drive Motors (L298N): ENA: GPIO 12 | IN1: GPIO 17 | IN2: GPIO 276. Operation Logic & Core CodeThe rover executes a non-blocking loop designed for "Silent Surveillance."Logic Flow:Surveillance: Polls Ultrasonic sensor. If $d < 10cm$, a delivery is detected.Environmental Check: Monitors for overheating ($T > 30°C$).Encapsulation: Serializes data into a JSON packet.Exfiltration: Publishes to the cloud topic upon status change.Integrated Motor Control Module:Pythonimport RPi.GPIO as GPIO

# Motor Pin Setup
ENA, IN1, IN2 = 12, 17, 27
GPIO.setup([ENA, IN1, IN2], GPIO.OUT)
pwm = GPIO.PWM(ENA, 100) # Speed control
pwm.start(0)

def shinobi_move_forward(speed=50):
    """Command the rover to move toward the post-box."""
    GPIO.output(IN1, GPIO.HIGH)
    GPIO.output(IN2, GPIO.LOW)
    pwm.ChangeDutyCycle(speed)

def shinobi_stop():
    """Halt all movement immediately."""
    GPIO.output(IN1, GPIO.LOW)
    GPIO.output(IN2, GPIO.LOW)
    pwm.ChangeDutyCycle(0)
7. About the AuthorChiun Huei 1981 Master Ninja Architect University of California, Irvine (UCI) - IoT Specialized StudiesLocation: Aachen-Sanctuary, GermanyDocumentation strictly for the Shinobi Rover Project. Verified March 2026.
'''
