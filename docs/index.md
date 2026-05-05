---
title: Welcome
---

<center>
<font size="6">Rylee Wirt – Controller Module Datasheet</font><br>
as part of<br>
<font size="8">EGR 314 M.E.G.</font><br>
for<br>
<font size="5">M.E.G.</font><br>

**Submission: May 4, 2026**
</center>

---

## Introduction

This datasheet documents the complete design and implementation of the Controller Module developed for Team 301’s EGR 314 rover project. The purpose of this document is to provide a clear and technical overview of the electrical design, component selection, communication architecture, power requirements, and schematic development of the module.

The controller module serves as the primary command interface within the rover system. It processes user input, formats structured communication packets, and transmits commands to other distributed modules over the team communication bus. The design is built around an ESP32 microcontroller operating at 3.3 V logic to ensure reliable digital communication and system integration.

This datasheet allows a reader to understand not only what was built, but why design decisions were made and how the module satisfies system requirements.

---

## Project Summary

Team 301 is developing a distributed rover system composed of multiple independent but interconnected modules. Each subsystem is responsible for a defined role within the overall rover architecture and communicates through a shared message structure.

The controller module functions as the central command node. It generates structured command messages that coordinate motor control, sensor interaction, and overall rover behavior. Proper voltage regulation, defined signal routing, and consistent packet formatting are critical to ensure stable operation across all modules.

This document focuses specifically on the controller subsystem. For complete system level documentation, architecture diagrams, and team level integration details, visit the Team 301 website:

https://asu-egr314-301-s-2026.github.io/EGR314-Team301/

---

## My Contribution

My responsibility on Team 301 was the complete design and documentation of the Controller Module. This includes:

- Defining functional and electrical requirements  
- Designing the block diagram and system interface  
- Selecting and justifying hardware components  
- Developing the schematic  
- Creating and analyzing the power budget  
- Documenting the electrical architecture  

This datasheet is organized to guide readers through each stage of the design process:

- **Requirements** define what the module must accomplish.  
- **Block Diagram** illustrates signal flow, communication paths, and power distribution.  
- **Component Selection** explains why specific hardware was chosen.  
- **BOM** lists materials used in the design.  
- **Schematic** shows the detailed electrical implementation.  
- **Power Budget** analyzes current draw and system power needs.  

Together, these sections demonstrate how the controller module integrates into the rover system and satisfies both functional and electrical design constraints.
