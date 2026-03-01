---
title: Module Requirements
---

## Module Requirements

This table defines the functional and technical requirements for the Controller Module of Team 301’s rover system. The controller module is responsible for receiving controller input from a host device, transmitting structured control packets over Wi Fi, and generating output signals that command rover subsystems.

These requirements establish measurable performance constraints that guide hardware selection, firmware development, communication architecture, and testing. Each requirement includes a minimum acceptable threshold, a target performance level, and whether it is considered a stretch objective.

| **Requirement Description** | **Measure of Threshold** | **Target Measure** | **Stretch (Y/N)** |
|-----------------------------|---------------------------|--------------------|:-----------------:|
| Wi Fi enabled microcontroller | ESP32 capable of connecting to a 2.4 GHz Wi Fi network | ESP32 supports stable TCP or UDP communication for continuous packet transfer | No |
| Logic operating voltage | Operates from regulated 3.3 V supply ±10% | Operates from regulated 3.3 V supply ±5% with stable communication | No |
| Wireless link update rate | Minimum 10 packets per second | ≥ 50 packets per second for responsive control | Yes |
| Controller compatibility | Supports one USB game controller connected to a laptop | Supports both Xbox and PlayStation controllers | No |
| End to end control latency | Functional response under 250 ms | Near real time response under 100 ms | Yes |
| Firmware packet handling | Correctly receives and parses incoming control packets | Implements filtering and validation to improve stability | Yes |
| Output signal generation | Generates digital output signals based on received data | Outputs include configurable mapping for flexibility | Yes |
| Maximum average current draw | ≤ 250 mA during active operation | ≤ 200 mA during active operation | Yes |
| Power source flexibility | Operates via USB 5 V input to onboard 3.3 V regulation | Supports regulated battery input | No |
| Message structure definition | Packets include button and axis values | Packets include timing, source ID, and error checking | Yes |
| System identification | Module uses fixed network address | Address configurable in firmware | Yes |
| Status indication | At least one LED indicates power | Separate LEDs indicate power and Wi Fi connection state | Yes |
