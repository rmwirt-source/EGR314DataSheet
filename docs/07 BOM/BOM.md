---
title: Bill of Materials
---

# Bill of Materials — Controller Subsystem

## Overview

This document lists all components required for the Controller Subsystem PCB.  
All components present in the schematic are included, including power regulation, protection, debugging hardware, connectors, and expansion interfaces.

Quantities reflect:
- One PCB assembly
- Recommended spares for fragile or critical components
- Common passive components sourced from Peralta workshop stock

The subsystem operates from a 12V input and regulates to 3.3V using a switching buck converter (MP2307).

---

## Complete Bill of Materials

| Ref | Qty | Description | Value | Package | Manufacturer | MPN | Vendor | Notes |
|-----|-----|------------|--------|----------|--------------|------|--------|-------|
| U1 | 1 | ESP32-S3-WROOM-1 | 3.3V MCU Module | SMD Module | Espressif | ESP32-S3-WROOM-1 | Peralta Stock | Main microcontroller |
| U2 | 1 | Temperature Sensor | TC74A4-3.3VCTTR | SOT-23-5 | Microchip | TC74A4-3.3VCTTR | Peralta Stock | I2C temperature sensor |
| U3 | 2 | Switching Regulator | MP2307DN-LF-Z | SOIC-8-EP | Monolithic Power Systems | MP2307DN-LF-Z | DigiKey | 3.3V buck converter |
| L1 | 5 | Power Inductor | 10uH ≥3A | 4x4mm SMD | Bourns | SRN4018-100M | DigiKey | Buck regulator inductor |
| C1 | 1 | Capacitor | 0.01uF | 0805 | Generic | — | Peralta Stock | Decoupling |
| C2 | 1 | Capacitor | 0.1uF | 0805 | Generic | — | Peralta Stock | Decoupling |
| C3 | 1 | Capacitor | 3.9nF | 0805 | Generic | — | Peralta Stock | Compensation |
| C4, C5 | 2 | Capacitor | 0.1uF 50V | 0805 | Generic | — | Peralta Stock | Input filtering |
| C6 | 1 | Capacitor | 0.1uF 50V | 0805 | Generic | — | Peralta Stock | Bootstrap |
| C7 | 1 | Capacitor | 22uF 16V | 1206 | Generic | — | Peralta Stock | Regulator output |
| C8 | 1 | Capacitor | 22uF 25V | 1210 | Generic | — | Peralta Stock | Input bulk |
| D1 | 1 | LED | Red | 0805 | Generic | — | Peralta Stock | Status indicator |
| D2 | 1 | LED | Green | 0805 | Generic | — | Peralta Stock | Status indicator |
| D3, D4 | 5 | USB ESD Protection | USBLC6-2SC6 | SOT-23-6 | STMicroelectronics | USBLC6-2SC6 | DigiKey | USB D+/D- protection |
| F1 | 5 | Fuse | 2A Slow Blow | 1206 | Littelfuse | 0467002.NR | DigiKey | Input protection |
| J1 | 1 | Programming Header | 1x6 2.54mm | SMD Header | Generic | — | Peralta Stock | Debug access |
| J2 | 1 | Upstream Header | 2x4 2.54mm | SMD Header | Generic | — | Peralta Stock | Team interface |
| J3 | 1 | Downstream Header | 2x4 2.54mm | SMD Header | Generic | — | Peralta Stock | Team interface |
| J4 | 1 | Micro USB Connector | USB Micro-B | SMD | Molex | 105017-0001 | Peralta Stock | Programming & power |
| R1, R8 | 2 | Resistor | 1kΩ | 0805 | Generic | — | Peralta Stock | LED limiting |
| R2 | 1 | Resistor | 26.1kΩ | 0805 | Generic | — | Peralta Stock | Feedback network |
| R3–R11 | 6 | Resistor | 10kΩ | 0805 | Generic | — | Peralta Stock | Pull-ups & biasing |
| R6–R14 | 5 | Resistor | 22Ω | 0805 | Generic | — | Peralta Stock | USB termination |
| SW1–SW3 | 3 | Pushbutton | Momentary | SMD | Generic | — | Peralta Stock | EN & GPIO control |
| TP1–TP6 | 6 | Test Points | 1.5mm Pad | SMD | Generic | — | Peralta Stock | Debug access |

---

## Debug and Expansion Hardware

This subsystem includes:

- Test points for USB D+, USB D−, 12V input, and inter-module connections
- Pushbuttons for EN and GPIO control
- USB interface for programming
- Upstream and downstream headers for team communication
- Surface mount fuse for input protection

These additions support safe bring-up, debugging, and future expansion.

---

## Purchasing Summary

The following components were ordered from DigiKey:

- MP2307DN-LF-Z
- SRN4018-100M
- USBLC6-2SC6
- 0467002.NR

Common passive components, connectors, and MCU modules are sourced from Peralta stock.

---

## Design Notes

The MP2307 switching regulator and 10uH inductor were selected to support peak ESP32 current draw while maintaining efficiency and thermal performance. USB ESD protection devices were added to protect the microcontroller from electrostatic discharge through the USB interface.
