# Agricultural Data Logger - Hardware Repository

**Project:** Operator Aid System (OAS) Data Logger
**Version:** 2.0 (Field-Ready Prototype)
**Last Updated:** July 1, 2025

---

## 1. Project Overview

This repository contains all hardware design files, schematics, PCB layouts, and component datasheets for the **Agricultural Data Logger**. This device is engineered for robust, in-field use on agricultural vehicles (such as tractors and spray rigs), offering a common, fast, and reliable method for data collection from various sensors.

The system continuously gathers high-frequency sensor data, including high-precision GPS location, stores it locally on a microSD card, and uploads the data to a cloud server via Wi-Fi whenever a connection is available.

The hardware design prioritizes low-power operation, high-speed data throughput, and resilience in harsh vehicular environments.

---

## 2. Key Features

* **High-Performance MCU:** Utilizes the ESP32-S3-MINI-1 with dual-core processing, Wi-Fi, Bluetooth 5 (BLE), and native USB support.
* **High-Speed Data Storage:** 4-bit SDIO interface for microSD card ensures rapid data logging.
* **Precision GPS:** u-blox SAM-M10Q GNSS module supports concurrent reception from GPS, GLONASS, Galileo, and BeiDou for high sensitivity and rapid position acquisition.
* **Advanced Power Management:** Intelligent power system with ultra-low deep sleep current, using a dedicated load switch to power down peripherals (GPS, SD card) when inactive.
* **Vehicular Power Compatibility:** Direct compatibility with standard 12V-14V tractor electrical systems, including onboard voltage regulation and electrical noise/transient protection.
* **Compact & Robust Form Factor:** Components optimized for small PCB footprint within ruggedized enclosures.

---

## 3. Core Components

| Component             | Part Number / Series    | Function                   | Key Rationale                                                                       |
| --------------------- | ----------------------- | -------------------------- | ----------------------------------------------------------------------------------- |
| **Microcontroller**   | ESP32-S3-MINI-1         | Main Processor, Wi-Fi/BLE  | Native USB, dedicated SDIO pins (no eFuse required), powerful dual-core CPU.        |
| **GPS/GNSS Module**   | u-blox SAM-M10Q         | High-Precision Positioning | High sensitivity (-165 dBm), concurrent constellation support, integrated antenna.  |
| **SD Card Interface** | Standard microSD Socket | Local Data Storage         | 4-bit SDIO for high-speed logging ensures no data loss during intensive operations. |
| **Peripheral Switch** |                         | Power Gating               | Low Rds(on) load switch completely cuts power to peripherals during deep sleep.     |
| **Voltage Regulator** | TBD Buck Converter      | Power Regulation           | Steps down 12V vehicle supply to stable 3.3V for onboard electronics.               |

---

## 4. Power System Architecture

The power system is engineered for robustness and efficiency:

* **Primary Power Source:** Accepts 10-14V DC input from a vehicle auxiliary power outlet. A DC-DC buck converter regulates this down to 3.3V.
* **Input Protection:** Includes filtering and transient voltage suppression to protect electronics from vehicular electrical noise.
* **Low-Power Domain:** ESP32-S3 enters deep sleep mode to maximize battery life. Peripherals (GPS, microSD) are switched via TPS22918, reducing sleep current to microamps.
* **Peak Current:** Designed for a peak current draw of \~150mA, supporting simultaneous GPS acquisition and microSD card operations.

---

## 5. Design Evolution & Rationale

This hardware revision represents significant evolution from previous prototypes:

* **MCU Change (ItsyBitsy/PICO-ZERO → ESP32-S3-MINI-1):** Eliminated the need for risky, irreversible eFuse programming by selecting a chip with dedicated SDIO pins.
* **Storage Interface (SPI → SDIO):** Upgraded storage interface from SPI to SDIO to accommodate higher frequency data logging without bottlenecks.
* **GPS Module (Previous → SAM-M10Q):** Chosen for superior sensitivity, multiple constellation support, and low-power performance suitable for challenging field environments.
