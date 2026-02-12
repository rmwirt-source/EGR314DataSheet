---
title: Module's Selected Major Components
---

## Module's Selected Major Components

The controller module is responsible for receiving user input, executing control algorithms, communicating over the team daisy-chain UART network, and interfacing between the Sensor and Actuator subsystems. Wireless controller input and laptop-based HMI functionality are enabled through an ESP32 companion module.

---

## Power Management

### Candidate A — MP2307DN-LF-Z 3.3V Synchronous Buck Regulator (Selected)

<img src="MP2307DN-LF-Z.webp" width="300">

* 3A synchronous buck regulator  
* DigiKey: https://www.digikey.com/en/products/detail/monolithic-power-systems-inc/MP2307DN-LF-Z/5292007  
* Datasheet: https://www.monolithicpower.com/en/documentview/productdocument/index/version/2/document_type/Datasheet/lang/EN/sku/MP2307/document_id/503/

| Pros | Cons |
| --- | --- |
| 3 A output headroom | Requires external inductor |
| Meets switching regulator requirement | Careful layout needed |
| Surface mount package | |

**Rationale:** Provides stable 3.3V rail with sufficient current for PIC and ESP32.

---

### Candidate B — TI TPS54331 Buck Regulator

* Product: https://www.ti.com/product/TPS54331  
* Datasheet: https://www.ti.com/lit/ds/symlink/tps54331.pdf

| Pros | Cons |
| --- | --- |
| Robust TI reference designs | Different layout and components required |
| 3 A output capability | Slightly higher cost |

---

### Candidate C — AMS1117-3.3 Linear Regulator

* Product example: https://www.analog.com/en/products/ams1117.html

| Pros | Cons |
| --- | --- |
| Very simple to implement | Inefficient for battery use |
| Low cost | High heat dissipation |

---

## Power Input

### Candidate A — Barrel Jack Connector (Selected)

<img src="BarrelJack.webp" width="300">

| Pros | Cons |
| --- | --- |
| Reliable lab power input | Needs protection circuitry |
| Strong mechanical support | |

**Rationale:** Standard connector supporting required bus jumpers.

---

### Candidate B — DC Jack + Schottky Diode + TVS

| Pros | Cons |
| --- | --- |
| Reverse polarity protection | Extra voltage drop |
| Increased robustness | More components |

---

### Candidate C — Battery Connector + Protection IC

| Pros | Cons |
| --- | --- |
| Integrated battery safety | More complex PCB design |
| Cleaner battery integration | Higher BOM cost |

---

## Daisy-Chain Communication

### Candidate A — 2x4 IDC Ribbon Cable Connectors (Selected)

<img src="CableConnectors.webp" width="300">

| Pros | Cons |
| --- | --- |
| Required team standard | Must maintain exact pin mapping |
| Carries UART + power | |

**Rationale:** Implements required 8-wire daisy-chain interface.

---

### Candidate B — JST-SH Connectors

| Pros | Cons |
| --- | --- |
| Compact connectors | Less standardized |
| Easier to debug individually | More wiring clutter |

---

### Candidate C — USB-UART Bridge for Debug

| Pros | Cons |
| --- | --- |
| Easy laptop debugging | Not suitable as main bus interface |
| Helpful during development | Extra component |

---

## Sensor Interface

### Candidate A — BNO055 Absolute Orientation Sensor (Selected)

<img src="BNO055.jpg" width="300">

* Product Overview: https://learn.adafruit.com/adafruit-bno055-absolute-orientation-sensor/overview  
* Datasheet: https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bno055-ds000.pdf

| Pros | Cons |
| --- | --- |
| Fused yaw/pitch/roll output | Requires calibration handling |
| Reduces firmware complexity | Slightly higher cost |

**Rationale:** Provides processed orientation data directly via I2C.

---

### Candidate B — ICM-20948 IMU

| Pros | Cons |
| --- | --- |
| Modern 9-DoF sensor | Requires custom fusion algorithm |
| Lower power modes | More firmware complexity |

---

### Candidate C — MPU-9250

| Pros | Cons |
| --- | --- |
| Widely supported libraries | Older sensor generation |
| Low cost | Requires sensor fusion |

---

## Controller Microcontroller

### Candidate A — PIC18F47K42 (Selected)

<img src="PIC18F47K42.webp" width="300">

* Product Page: https://www.microchip.com/en-us/product/PIC18F47K42  
* DigiKey: https://www.digikey.com/en/products/detail/microchip-technology/PIC18F47K42T-I-MV/7561728

| Pros | Cons |
| --- | --- |
| Course-approved PIC | No Bluetooth capability |
| Strong peripheral set | 8-bit architecture |

**Rationale:** Primary MCU for control and communication.

---

### Candidate B — PIC18F47Q10

| Pros | Cons |
| --- | --- |
| Similar peripheral support | Different footprint options |
| Good Microchip support | |

---

### Candidate C — STM32F103

| Pros | Cons |
| --- | --- |
| 32-bit performance | Different toolchain |
| More computational headroom | Not PIC-based |

---

## Wireless Companion

### Candidate A — ESP32-S3-WROOM-1-N4 (Selected)

<img src="ESP32.webp" width="300">

* DigiKey: https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1-N4/16162639  
* Datasheet: https://www.espressif.com/sites/default/files/documentation/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf

| Pros | Cons |
| --- | --- |
| Bluetooth HID for DualSense | Adds secondary module |
| WiFi for laptop HMI | Slight power increase |

**Rationale:** Handles wireless controller pairing and laptop communication.

---

### Candidate B — ESP32-WROOM-32

| Pros | Cons |
| --- | --- |
| Large community support | Older BLE stack |
| Lower cost | HID host more limited |

---

### Candidate C — RN-52 Bluetooth Module

| Pros | Cons |
| --- | --- |
| Simple integration | Not designed for HID host |
| Standalone module | Limited flexibility |

---

## Programming Tool

### Candidate A — MPLAB SNAP (Selected)

<img src="SNAP.png" width="300">

* Product Page: https://www.microchip.com/en-us/development-tool/PG164100

| Pros | Cons |
| --- | --- |
| Fully supported in MPLABX | Requires ICSP header |
| Reliable debugging tool | |

---

### Candidate B — PICkit 4

| Pros | Cons |
| --- | --- |
| Faster programming | Higher cost |
| Official Microchip tool | |

---

### Candidate C — Third-Party Programmer

| Pros | Cons |
| --- | --- |
| Lower cost | Not officially supported |
| Available quickly | Potential compatibility issues |

---

## Final Selection Summary

Selected components balance performance, modularity, cost, and course requirements. The final configuration includes:

- MP2307DN-LF-Z switching regulator  
- Barrel jack power input  
- 2x4 IDC daisy-chain interface  
- BNO055 IMU  
- PIC18F47K42 microcontroller  
- ESP32-S3-WROOM-1-N4 wireless companion  
- MPLAB SNAP programmer  

This configuration satisfies course requirements while maintaining modular system architecture.
