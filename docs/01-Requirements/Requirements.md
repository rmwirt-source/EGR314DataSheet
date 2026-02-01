---
title: Module's Requirements
---

## Module Requirements
This table outlines the functional and technical requirements for the controller module of the system. The controller module is responsible for receiving user input from a handheld game controller, transmitting that input wirelessly, and providing control signals to the rover during operation. Defining these requirements helps ensure the module meets minimum functionality while also identifying target performance goals and optional stretch features that may be implemented if time allows. These requirements guide hardware selection, communication design, and testing throughout development.


| **Requirement Description** | **Measure of<br>Threshold** | **Target<br>Measure** | **Stretch<br>Requirement<br>(Y-N)** |
|-----------------------------|-----------------------------|-----------------------|:----------------------------------:|
| Wi Fi enabled microcontroller | An ESP32 that can successfully connect to a Wi Fi network | An ESP32 that supports reliable TCP or UDP communication | No |
| Wireless link architecture | Controller input is sent from a laptop to the ESP32 over Wi Fi at a basic update rate | Controller input is transmitted using UDP or WebSocket at a higher, more responsive update rate | No |
| Controller compatibility | One supported Xbox or PlayStation controller connected to the laptop | Both Xbox and PlayStation controllers supported on the laptop | No |
| Controller input latency | User input results in a visible response within a noticeable but usable time | User input results in a near real time response | No |
| Module power during testing | Module operates while powered through a USB connection | Module can operate using a battery with appropriate voltage regulation | No |
| Firmware functionality | Incoming control data is received and used to set output signals | Control inputs are mapped and filtered to improve responsiveness and usability | No |
| Test and verification | Basic manual testing confirms that controller inputs affect system behavior | Repeatable tests are used to measure responsiveness and consistency | No |
| Message format | Control data is sent in a simple, readable format containing button and axis values | Control messages include additional information such as timing or ordering data | Yes |
| Physical user interface | A single indicator shows whether the module is powered and active | Multiple indicators show power and wireless connection status | Yes |
| Security | No authentication is required during initial testing | A simple authentication method is used to limit unintended connections | Yes |
