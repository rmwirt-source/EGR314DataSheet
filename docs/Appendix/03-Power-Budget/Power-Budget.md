---
title: Power Budget
---

# Power Budget — Controller Subsystem

**Assumptions**  
- Input supply: **2S LiPo (nominal 7.4 V)**  
- Regulator: **MP2307DN-LF-Z** stepping to **3.3 V**  
- Regulator efficiency assumed **η = 90%**  
- Required safety margin: **25%** on total average current

## Component table (copy/paste)

| Device | V (V) | Idle I (A) | Active I (A) | Duty active (%) | Avg I (A) |
|---|---:|---:|---:|---:|---:|
| ESP32-S3-WROOM-1-N4 | 3.3 | 0.015000 | 0.400000 | 10 | 0.053500 |
| TC74A4-3.3VCTTR (temp) | 3.3 | 0.001000 | 0.012000 | 5 | 0.001550 |
| MP2307 quiescent (Iq) | 3.3 | 0.002000 | 0.002000 | 100 | 0.002000 |
| Misc (LEDs, pullups, UART, sensors) | 3.3 | 0.002000 | 0.020000 | 10 | 0.003800 |
| **TOTAL (average)** | 3.3 |  |  |  | **0.060850** |

## Margin and power conversion (digit-by-digit)

1. Total average current (Iavg) = **0.060850 A**  
2. Add 25% safety margin: Iout_with_margin = Iavg × 1.25 = **0.0760625 A**  
3. Output power Pout = Vout × Iout_with_margin = 3.3 × 0.0760625 = **0.25100625 W**  
4. Assumed regulator efficiency η = 0.90  
5. Input voltage Vin = 7.4 V  
6. Input current from battery Iin = Pout / (Vin × η)  
   = 0.25100625 / (7.4 × 0.90)  
   = 0.25100625 / 6.66  
   = **0.037688626126126126 A**

## Battery run time example

- Example battery: **2200 mAh (2.2 Ah)**  
- Battery runtime (hours) = Capacity (mAh) / (Iin × 1000)  
  = 2200 / (0.037688626126126126 × 1000)  
  ≈ **58.373 hours**

## Required battery capacity for a target runtime

- Target runtime = **8 hours** (example)  
- Required capacity mAh = Iin × 1000 × target_hours  
  = 0.037688626126126126 × 1000 × 8  
  = **301.509 mAh** → recommend at least **400–500 mAh** in practice to allow margin and degradation

## Short written explanation (copy/paste)

Total controller average current (including 25% safety margin) is **0.0760625 A** at 3.3 V which corresponds to an input draw of **~0.03769 A** from a 2S LiPo assuming 90% regulator efficiency. A 2200 mAh pack would theoretically run the controller subsystem alone for roughly **58 hours** under these conservative estimates. For an 8 hour mission you only need about **0.30 Ah (≈302 mAh)** in theory but pick a larger capacity (typical 1000–2200 mAh) to account for battery ageing, higher duty cycles, additional peripherals, and any possible future motor loads.

**Design decisions influenced:**  
- Kept the MP2307 (3 A rated) because regulator headroom is trivial cost and prevents thermal stress during Wi-Fi bursts.  
- Offloaded processing to the ESP32 to remove a second MCU and reduce idle power overhead.  
- Used a low-BOM temp sensor (TC74) to keep average current very low.  
- If motors or actuators get added to this board later, move them to a separate power rail and re-run this budget.
