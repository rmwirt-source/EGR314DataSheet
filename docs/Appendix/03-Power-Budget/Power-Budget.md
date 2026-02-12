---
title: Power Budget
---

## Power Budget — Controller Subsystem

**Assumptions and notes**

- Input supply chosen for this budget: **2S LiPo (nominal 7.4 V)**.  
- Primary DC-DC regulator: **MP2307DN-LF-Z** configured for **3.3 V output**.  
- Converter efficiency assumed: **90%** (typical for a synchronous buck under moderate load).  
- All values are worst-case or conservative estimates. Intermediate and average numbers are listed where appropriate.  
- Required safety margin: **25%** on calculated operating current (per course checklist).

---

## Devices considered (controller board only)

| Device | Voltage (V) | Worst-case current (A) | Notes |
| ------ | -----------:| ---------------------:| ----- |
| ESP32-S3-WROOM-1-N4 (WiFi tx peak) | 3.3 | 0.400 | Peak WiFi transmit bursts; use worst-case for budgeting |
| PIC18F47K42 (active) | 3.3 | 0.030 | Active MCU typical ~10–30 mA; use 30 mA for conservative worst-case |
| BNO055 IMU (breakout) | 3.3 | 0.012 | Datasheet typical current ≈ 10–12 mA |
| Miscellaneous (LEDs, pullups, UART transceivers, sensors) | 3.3 | 0.020 | Allowance for LEDs, level shifters, logic, etc. |
| **Total (worst-case)** | 3.3 | **0.462** | Sum of above currents |

---

## Add 25% safety margin (course requirement)

- Total worst-case current = 0.462 A  
- Total with 25% margin = 0.462 A × 1.25 = **0.5775 A**

So the regulator must be sized to supply **≥ 0.5775 A at 3.3 V** continuously, with headroom for bursts.

---

## Output power and input current calculation (digit-by-digit)

1. Output voltage Vout = **3.3 V**  
2. Output current with margin Iout = **0.5775 A**  
3. Output power Pout = Vout × Iout = 3.3 × 0.5775 = **1.90575 W**

4. Assumed regulator efficiency η = **0.90**  
5. Input voltage Vin = **7.4 V (2S LiPo nominal)**

6. Input current Iin = Pout / (Vin × η)  
   = 1.90575 W / (7.4 V × 0.90)  
   = 1.90575 / 6.66  
   = **0.28615 A** (≈ 286.15 mA)

---

## Battery sizing and run time estimate

- Example battery chosen: **2S LiPo, 2200 mAh** (a common small pack).  
- Worst-case input current drawn from battery ≈ **0.28615 A**.

Battery life (hours) = Capacity (mAh) / (Iin × 1000)  
= 2200 mAh / (286.15 mA)  
≈ **7.69 hours**

Notes
- This is a conservative worst-case continuous estimate including the 25% safety margin on output current and a conservative efficiency assumption.  
- Short WiFi TX bursts will draw high current momentarily; average system current may be much lower, giving longer real-world run time.  
- If a larger motor load or other high-current peripherals are later added to this board, re-evaluate the rail and battery sizing.

---

## Power rail summary (recommended)

| Rail | Source/Regulator | Nominal voltage | Max required current (with 25% margin) | Suggested regulator rating |
| ---- | ---------------- | --------------: | -------------------------------------: | -------------------------: |
| 3.3 V (logic) | MP2307DN-LF-Z (synchronous buck) | 3.3 V | 0.5775 A | Use MP2307 (3 A rating) — provides ample headroom |
| Bus / actuator power | External / actuator board | per team (not on controller) | n/a | Actuator board handles motor power rails |

**Rationale:** MP2307 is rated for multiple amps. Using a 3 A rated buck provides comfortable headroom for transient events and future peripheral additions without needing a regulator change.

---

## Recommended protection and input components

- Input transient suppression: **TVS diode** sized for 2S LiPo voltage.  
- Input fuse: **PTC resettable fuse** sized slightly above expected Iin (for example 0.5 A hold or 1 A depending on safety policy).  
- Bulk and decoupling capacitors per MP2307 datasheet and ESP32 layout guidelines.  
- Layout considerations: follow MP2307 reference layout exactly for loop area minimization and place ESP32 module keep-out and antenna clearance per Espressif datasheet.

---

## Alternate scenarios (quick notes)

1. **If supply is a 9 V barrel**  
   - Vin increases, input current decreases slightly for same Pout. Recompute Iin using Vin = 9 V. Regulator still fine.

2. **If bus power supplies 5 V**  
   - Use same calculation with Vin = 5 V and η = 0.90. Expect higher Iin and slightly lower battery life for given capacity.

3. **If board will also power motors**  
   - Recompute per-motor current and move motor power to a separate rail and regulator sized for motor current. Controller PCB should not route high motor currents unless explicitly designed for it.

---

## References

- MP2307 datasheet and layout recommendations: [Monolithic Power Systems MP2307 datasheet](https://www.monolithicpower.com/en/documentview/productdocument/index/version/2/document_type/Datasheet/lang/EN/sku/MP2307/document_id/503/)  
- ESP32-S3 typical current characteristics: Espressif datasheet and examples (peak WiFi transmit currents).  
- BNO055 datasheet for IMU current draw: Bosch Sensortec BNO055 datasheet.

