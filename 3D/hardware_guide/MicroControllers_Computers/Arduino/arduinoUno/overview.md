
# Arduino Uno Overview

The Arduino Uno is the most popular and widely used board in the Arduino family. It's a great choice for beginners and experienced users alike.

## Key Features

- **Microcontroller:** ATmega328P
- **Operating Voltage:** 5V
- **Input Voltage (recommended):** 7-12V
- **Digital I/O Pins:** 14 (of which 6 provide PWM output)
- **Analog Input Pins:** 6
- **DC Current per I/O Pin:** 20 mA
- **Flash Memory:** 32 KB
- **SRAM:** 2 KB
- **EEPROM:** 1 KB
- **Clock Speed:** 16 MHz

## Pinout

![Arduino Uno Pinout](https://content.arduino.cc/assets/Pinout-Unorev3_latest.png)

## Power

The Arduino Uno can be powered via the USB connection or with an external power supply. The power source is selected automatically.

External (non-USB) power can come either from an AC-to-DC adapter (wall-wart) or a battery. The adapter can be connected by plugging a 2.1mm center-positive plug into the board's power jack. Leads from a battery can be inserted in the Gnd and Vin pin headers of the POWER connector.

## Communication

The Arduino Uno has a number of facilities for communicating with a computer, another Arduino, or other microcontrollers.

- **Serial:** The ATmega328P provides UART TTL (5V) serial communication, which is available on digital pins 0 (RX) and 1 (TX).
- **I2C:** The board has a dedicated I2C bus, which is available on pins A4 (SDA) and A5 (SCL).
- **SPI:** The board has a dedicated SPI bus, which is available on pins 10 (SS), 11 (MOSI), 12 (MISO), and 13 (SCK).
