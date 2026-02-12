---
title: Appendix - Controller Table for the PIC
---

| PIC Info                                      | Answer |
| --------------------------------------------- | ------ |
| Model                                         | PIC18F47K42 |
| Product Page URL                              | [Microchip Product Page](https://www.microchip.com/en-us/product/PIC18F47K42) |
| Datasheet URL(s)                              | [PIC18F27/47K42 Datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/PIC18(L)F27-47K42-Data-Sheet-40002043F.pdf) |
| Application Notes URL(s)                      | [Microchip Application Notes](https://www.microchip.com/en-us/product/PIC18F47K42#document-table) |
| Vendor link                                   | [DigiKey Listing](https://www.digikey.com/en/products/detail/microchip-technology/PIC18F47K42T-I-MV/7561728) |
| Code Examples                                 | [Microchip Code Examples](https://github.com/microchip-pic-avr-examples) |
| External Resources URL(s)                     | [Microchip Developer Help](https://microchipdeveloper.com/) |
| Unit cost                                     | ~$5–7 USD (varies by quantity) |
| Absolute Maximum Current for entire IC        | 300 mA total device current (see datasheet) |
| Supply Voltage Range                          | 1.8V – 5.5V (Nominal 3.3V) |
| Absolute Maximum current (for entire IC)      | 300 mA |
| Maximum GPIO current (per pin)                | 25 mA per pin (absolute max) |
| Supports External Interrupts?                 | Yes |
| Required Programming Hardware, Cost, URL      | MPLAB SNAP (~$35) [SNAP Tool](https://www.microchip.com/en-us/development-tool/PG164100) |
| Works with MPLabX?                            | Yes |
| Works with Microchip Code Configurator?       | Yes |

---

| Module | # Available | Needed | Associated Pins (or * for any) |
| ---------- | ----------- | ------ | ------------------------------ |
| GPIO       | 35+        | ~6–10  | * |
| ADC        | 35 channels | 1      | RA0 (battery sense) |
| UART       | 2 EUSART   | 2      | TX1/RX1 (Bus), TX2/RX2 (ESP32) |
| SPI        | 2 MSSP     | 0–1    | * |
| I2C        | 2 MSSP     | 1      | SDA/SCL (IMU) |
| PWM        | 5+ CCP     | 0–2    | * |
| ICSP       | 1          | 1      | MCLR, PGEC, PGED |
