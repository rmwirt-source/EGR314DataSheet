---
title: Controller Table for the ESP32
---

| ESP Info                                      | Answer |
| --------------------------------------------- | ------ |
| Model                                         | ESP32-S3-WROOM-1-N4 |
| Product Page URL                              | [Espressif Product Page](https://www.espressif.com/en/products/modules/esp32-s3-wroom-1) |
| ESP32-S3-WROOM-1-N4 Datasheet URL             | [Module Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf) |
| ESP32 S3 Datasheet URL                        | [ESP32-S3 Datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3_datasheet_en.pdf) |
| ESP32 S3 Technical Reference Manual URL       | [ESP32-S3 TRM](https://www.espressif.com/sites/default/files/documentation/esp32-s3_technical_reference_manual_en.pdf) |
| Vendor link                                   | [DigiKey Listing](https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1-N4/16162639) |
| Code Examples                                 | [ESP-IDF Examples](https://github.com/espressif/esp-idf) |
| External Resources URL(s)                     | [Bluepad32 Library](https://github.com/ricardoquesada/bluepad32) |
| Unit cost                                     | ~$6–8 USD |
| Absolute Maximum Current for entire IC        | ~500 mA peak during WiFi transmit |
| Supply Voltage Range                          | 3.0V – 3.6V (Nominal 3.3V) |
| Absolute Maximum current (for entire IC)      | ~500 mA peak |
| Maximum GPIO current (per pin)                | 40 mA (absolute max, recommended <20 mA) |
| Supports External Interrupts?                 | Yes |
| Required Programming Hardware, Cost, URL      | USB programming built-in (no external programmer required) |

---

| Module         | # Available | Needed | Associated Pins (or * for any) |
| -------------- | ----------- | ------ | ------------------------------ |
| UART           | 3+         | 1      | TX/RX to PIC |
| external SPI   | Multiple   | 0      | * |
| I2C            | 2          | 0–1    | * |
| GPIO           | 40+        | ~4–6   | * |
| ADC            | 20+        | 0–1    | * |
| LED PWM        | 8+        | 0–2    | * |
| Motor PWM      | 8+        | 0      | * |
| USB Programmer | Native USB | 1      | USB D+/D- |
