
# ESP32-CAM Overview

The ESP32-CAM is a small, low-cost development board that combines an ESP32-S microcontroller with a 2-megapixel OV2640 camera. It's an excellent choice for projects that require video streaming, image capture, or computer vision.

## Key Features

- **Microcontroller:** ESP32-S
- **Camera:** OV2640 (2MP)
- **Flash Memory:** 4MB
- **RAM:** 520KB SRAM + 4MB PSRAM
- **Wi-Fi:** 802.11 b/g/n
- **Bluetooth:** v4.2 BR/EDR and BLE
- **GPIO:** 9 available GPIO pins
- **Storage:** MicroSD card slot (up to 4GB)
- **Power:** 5V input

## Pinout

![ESP32-CAM Pinout](https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/03/esp32-cam-pinout-ai-thinker.png?w=712&quality=100&strip=all&ssl=1)

## Getting Started

To use the ESP32-CAM, you'll need an FTDI programmer to upload code. The board does not have a built-in USB-to-serial converter.

**Important:** Before uploading code, you must connect the `GPIO 0` pin to `GND`. This puts the board into flashing mode. After the code is uploaded, disconnect `GPIO 0` from `GND` and press the reset button to run the new sketch.

## Powering the ESP32-CAM

The board can be powered through the 5V pin. It's recommended to use an external 5V power supply that can provide at least 2A, especially when using the camera, as it can be power-hungry.
