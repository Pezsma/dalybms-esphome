# Daly BMS Monitor with ESPHome and ESP32-S3 via RS485

This project provides an ESPHome configuration for monitoring a Daly Battery Management System (BMS) using an ESP32-S3 microcontroller. Communication is handled over an RS485 bus using the Modbus protocol.

The configuration reads various parameters from the BMS, such as individual cell voltages, temperatures, total voltage, current, state of charge (SOC), and detailed fault statuses, making them available for integration into home automation platforms like Home Assistant.

---

## Features ✨

- **Real-time Monitoring**: Reads key metrics from the Daly BMS every 10 seconds.
- **Comprehensive Data**: Fetches individual cell voltages, temperatures, total pack voltage, current, and SOC.
- **Detailed Fault Reporting**: Decodes the BMS fault registers to provide clear binary sensors for specific alarms (e.g., cell over-voltage, over-temperature, etc.).
- **Textual Status**: Provides human-readable sensors for charge/discharge status, balancing state, and battery chemistry.
- **Easy Integration**: Designed for seamless use with Home Assistant via the ESPHome API.
- **Robust Connectivity**: Includes WiFi configuration with a fallback access point for easy setup and recovery.
- **Web Interface**: A local web server on the ESP32 provides direct access to sensor states.

---

## Hardware Requirements Hardware 🛠️

- **ESP32-S3 Development Board**: This configuration is specifically for an `esp32-s3-devkitc-1`.
- **Daly BMS**: A Daly BMS model that supports communication via RS485.
- **RS485 to TTL Converter**: A module to interface between the ESP32's UART (TTL logic levels) and the RS485 bus. 

---

## Wiring 🔌

You need to connect the ESP32-S3 to the RS485-to-TTL converter, which is then connected to the Daly BMS.

1.  **Connect ESP32-S3 to RS485 Converter:**
    -   ESP32 **GND** → RS485 Module **GND**
    -   ESP32 **3.3V/5V** → RS485 Module **VCC** (check your module's voltage requirement)
    -   ESP32 **GPIO 6** (RX) → RS485 Module **RO** (Receiver Out)
    -   ESP32 **GPIO 7** (TX) → RS485 Module **DI** (Driver In)



---

## Software Setup ⚙️

1.  **Install ESPHome**: If you haven't already, install ESPHome. The easiest way is through the Home Assistant Add-on store.
2.  **Create a `secrets.yaml` file**: In your ESPHome configuration directory, create a file named `secrets.yaml` to store your WiFi credentials securely. Add the following content:
    ```yaml
    wifi_ssid: "YOUR_WIFI_SSID"
    wifi_password: "YOUR_WIFI_PASSWORD"
    ```
3.  **Add the Configuration**: Copy the `esps3.yaml` file from this repository into your ESPHome configuration directory.
4.  **Compile and Upload**: Open the ESPHome dashboard, find your new device, and click "Install". Choose your preferred method to flash the firmware onto your ESP32-S3 board for the first time (e.g., via USB). Subsequent updates can be done Over-The-Air (OTA).

---

## Configuration 🔧

While the provided configuration should work for many setups, you might need to adjust a few parameters in the YAML file:

- **Board Type**: If you are using a different ESP32-S3 board, change the `board` value:
  ```yaml
  esp32:
    board: esp32-s3-devkitc-1
