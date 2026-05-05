# Power Budget — Controller Subsystem

## Assumptions
- Input supply: 2S LiPo (nominal 7.4 V)  
- Regulator: MP2307DN-LF-Z stepping down to 3.3 V  
- Regulator efficiency: 90%  
- Safety margin: 25% applied to total average current  

## Component Power Analysis

Each component in the controller subsystem was evaluated using datasheet values for both idle and active current. A duty cycle was applied to estimate the average current draw for each device.

| Device | Voltage (V) | Idle Current (A) | Active Current (A) | Duty Cycle (%) | Average Current (A) |
|--------|------------|------------------|--------------------|----------------|---------------------|
| ESP32-S3-WROOM-1-N4 | 3.3 | 0.015000 | 0.400000 | 10 | 0.053500 |
| TC74A4-3.3VCTTR (Temperature Sensor) | 3.3 | 0.001000 | 0.012000 | 5 | 0.001550 |
| MP2307 Quiescent Current | 3.3 | 0.002000 | 0.002000 | 100 | 0.002000 |
| Misc (LEDs, pull-ups, UART, sensors) | 3.3 | 0.002000 | 0.020000 | 10 | 0.003800 |
| **Total Average Current** | 3.3 |  |  |  | **0.060850** |

## Power and Current Calculations

The total average current of the controller subsystem is:

\[
I_{avg} = 0.060850 \, A
\]

Applying a 25% safety margin:

\[
I_{out} = 0.060850 \times 1.25 = 0.0760625 \, A
\]

The output power at 3.3 V is:

\[
P_{out} = 3.3 \times 0.0760625 = 0.25100625 \, W
\]

Assuming a regulator efficiency of 90%, the input current from the 7.4 V battery is:

\[
I_{in} = \frac{P_{out}}{V_{in} \times \eta} = \frac{0.25100625}{7.4 \times 0.90} \approx 0.03769 \, A
\]

## Battery Runtime Estimation

Using a 2200 mAh (2.2 Ah) battery:

\[
\text{Runtime} = \frac{2200}{0.03769 \times 1000} \approx 58.37 \text{ hours}
\]

This represents an ideal estimate for the controller subsystem only.

For a target runtime of 8 hours:

\[
\text{Required Capacity} = 0.03769 \times 1000 \times 8 \approx 301.5 \, mAh
\]

In practice, a larger battery (1000–2200 mAh) is recommended to account for:
- Battery aging  
- Higher real-world duty cycles  
- Additional peripherals  
- Future system expansion  

## Analysis and Design Insights

The power budget shows that the controller subsystem has relatively low power requirements, and the selected power supply is more than sufficient to support operation with a comfortable margin. However, during testing, the voltage regulator did not function correctly due to improper capacitor placement and grounding.

This highlights an important limitation of power budgeting: while calculations can confirm that a design should work in theory, correct physical implementation is critical for achieving stable operation. In a future revision, the regulator circuit would be redesigned strictly following the datasheet recommendations, including proper capacitor selection, placement, and grounding.

The analysis also reinforces the importance of including a safety margin. The 25% margin helps account for transient current spikes, especially from the ESP32 during Wi-Fi communication, and ensures that the system remains stable under varying operating conditions.

## Design Decisions Influenced by Power Budget

- The MP2307 regulator (rated for 3 A) was retained to provide significant headroom, preventing thermal stress and ensuring stable operation during transient loads.
- The ESP32 was used as the primary processing unit to reduce the need for additional microcontrollers, minimizing idle power consumption.
- A low-power temperature sensor (TC74) was selected to keep average current draw minimal.
- Future designs should separate high-power components, such as motors or actuators, onto a different power rail to avoid introducing noise and instability into the controller subsystem.
