MediBoX: Smart Medical Box System



MediBoX is an IoT-based smart medical box system built on the ESP32 microcontroller. It monitors environmental conditions (light and temperature) to control a servo motor, manages medication reminders through alarms, and provides remote configuration via MQTT. The system features an OLED display for user interaction, a buzzer for alarm notifications, and push buttons for menu navigation. This project is simulated using the Wokwi ESP32 Simulator, allowing for rapid prototyping and testing.

Table of Contents





Features



Hardware Requirements



Software Requirements



Setup Instructions



Usage



Screenshots



Contributing



License

Features





Environmental Monitoring: Reads light intensity (LDR) and temperature (DHT22) to adjust a servo motor’s position for optimal storage conditions.



Alarm System: Configurable alarms for medication reminders with buzzer and LED notifications, supporting snooze and stop functionality.



User Interface: OLED display (SSD1306) for time, temperature, and menu navigation; push buttons for setting time, alarms, and system controls.



MQTT Integration: Publishes average light intensity and subscribes to configuration updates (e.g., sample interval, temperature thresholds) via MQTT broker (HiveMQ).



Wi-Fi and NTP: Connects to Wi-Fi for internet access and synchronizes time using NTP for accurate alarm scheduling.



Wokwi Simulation: Fully simulated on Wokwi’s ESP32 simulator for testing without physical hardware.

Hardware Requirements





ESP32 Dev Module: Core microcontroller for processing and connectivity.



LDR (Light Dependent Resistor): Connected to pin 4 for light intensity measurement.



DHT22 Sensor: Connected to pin 12 for temperature and humidity readings.



Servo Motor: Connected to pin 18 for controlling the medical box mechanism.



SSD1306 OLED Display (128x64): Connected via I2C (pins SDA/SCL) for user interface.



Buzzer: Connected to pin 5 for alarm notifications.



LED: Connected to pin 15 for visual alarm indication.



Push Buttons: Four buttons (OK, Cancel, Up, Down) connected to pins 32, 34, 33, and 35 for menu navigation.



Breadboard and Jumper Wires: For circuit assembly.

Software Requirements





Arduino IDE or PlatformIO for programming the ESP32.



Libraries:





WiFi.h (built-in for ESP32)



ESP32Servo.h for servo control



PubSubClient.h for MQTT communication



DHTesp.h for DHT22 sensor



Wire.h for I2C communication



Adafruit_GFX.h and Adafruit_SSD1306.h for OLED display



Wokwi Simulator: For testing and simulation (https://wokwi.com/projects/431206882518972417).



Node-RED: For creating a dashboard and MQTT flows to monitor and control the system.



MQTT Broker: HiveMQ public broker (broker.hivemq.com, port 1883) for MQTT communication.

Setup Instructions





Clone the Repository:

git clone https://github.com/your-username/medibox.git
cd medibox



Set Up Wokwi Simulation:





Open the project in Wokwi: MediBoX Wokwi Project.



Ensure the diagram.json matches the pin definitions in the code (LDR: pin 4, DHT22: pin 12, Servo: pin 18, etc.).



Upload the provided medibox.ino file to the Wokwi code editor.



Install Arduino Libraries:





Install the required libraries in Arduino IDE or PlatformIO:

platformio lib install "ESP32Servo"
platformio lib install "PubSubClient"
platformio lib install "DHTesp"
platformio lib install "Adafruit GFX Library"
platformio lib install "Adafruit SSD1306"



Configure Wi-Fi and MQTT:





Update the ssid and password in medibox.ino to match your Wi-Fi credentials (default uses Wokwi’s guest network: Wokwi-GUEST, no password).



Replace mqtt_client_id with a unique ID (e.g., MediBoX_ESP32_12345).



Ensure the MQTT broker settings point to broker.hivemq.com (port 1883).



Set Up Node-RED:





Install Node-RED locally or use a cloud instance.



Import the Node-RED flow (see node-red-flow.json in the repository, if provided).



Configure MQTT nodes to subscribe to medibox/ldr/average and publish to configuration topics (medibox/config/ts, medibox/config/tu, etc.).



Set up a Node-RED dashboard to visualize sensor data and control parameters.



Run the Simulation:





In Wokwi, press the "Play" button to start the simulation.



Verify the OLED display shows time and status, and test button interactions for menu navigation.



Deploy on Hardware (Optional):





Assemble the circuit as per the Wokwi schematic.



Upload the code to your ESP32 using Arduino IDE or PlatformIO.



Test the physical setup with the same Wi-Fi and MQTT configurations.

Usage





Power On: The ESP32 connects to Wi-Fi, synchronizes time via NTP, and initializes the servo to the default angle (30°).



Sensor Monitoring: The system samples light (LDR) every 5 seconds (configurable) and temperature (DHT22), updating the servo position every 120 seconds based on average light and temperature.



Alarms: Two alarms (default at 22:05 and 22:06) trigger a buzzer and LED, with a "MEDICINE TIME!" display. Press OK to snooze (adds 5 minutes) or Cancel to stop.



Menu Navigation:





Press OK to enter the menu.



Use Up/Down to navigate options (Set UTC Offset, Set Alarm 1/2, Enable/Disable Alarms, View Alarms, Delete Alarm).



Press OK to select, Cancel to exit.



Node-RED Dashboard: Access the dashboard (e.g., http://<node-red-ip>:1880/ui) to view real-time light and temperature data and adjust system parameters via MQTT.

Screenshots

Node-RED Dashboard



Displays real-time sensor data and system controls.

Wokwi Simulation with Code



Shows the ESP32 circuit and code editor in Wokwi.

Node-RED Connections



Illustrates the MQTT flow for sensor data and configuration.

Contributing

Contributions are welcome! To contribute:





Fork the repository.



Create a new branch (git checkout -b feature/your-feature).



Make changes and commit (git commit -m "Add your feature").



Push to the branch (git push origin feature/your-feature).



Open a pull request.

Please ensure your code follows the existing style and includes comments for clarity.

License

This project is licensed under the MIT License. See the LICENSE file for details.
