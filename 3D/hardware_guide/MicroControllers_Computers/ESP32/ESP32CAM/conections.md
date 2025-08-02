
# ESP32-CAM Connections

Connecting the ESP32-CAM to other components and programming it requires a few specific connections.

## Programming Connections (using an FTDI Programmer)

To upload code to the ESP32-CAM, you need an FTDI (Future Technology Devices International) programmer, which is a USB-to-serial converter.

Here are the necessary connections:

| ESP32-CAM Pin | FTDI Programmer Pin |
| :---: | :---: |
| 5V | VCC (5V) |
| GND | GND |
| U0TXD | RXD |
| U0RXD | TXD |

**Crucial Step for Uploading:** Before you can upload a sketch, you must connect the `GPIO 0` pin to `GND`. This action puts the ESP32-CAM into flashing mode.

### Uploading Procedure:

1. Make the connections listed in the table above.
2. Connect `GPIO 0` to `GND`.
3. Connect the FTDI programmer to your computer via USB.
4. Open your programming environment (e.g., Arduino IDE).
5. Select the correct board (`AI Thinker ESP32-CAM`) and COM port.
6. Press the "Upload" button.
7. Once the upload is complete, **disconnect `GPIO 0` from `GND`**.
8. Press the onboard reset (RST) button to start running your new program.

## Powering the ESP32-CAM

While you can power the board through the FTDI programmer during development, for standalone projects, it's highly recommended to use a dedicated 5V power supply.

- **Using the 5V Pin:** Connect a stable 5V power source to the `5V` and `GND` pins. The power supply should be able to provide at least 2A, especially when the camera and Wi-Fi are active, to prevent brownouts and instability.

## MicroSD Card Connections

The ESP32-CAM has a built-in MicroSD card slot. The connections are internal, so you just need to insert a formatted MicroSD card (up to 4GB is officially supported, but larger cards may work).

The following GPIO pins are used by the MicroSD card reader:

- **GPIO 14:** CLK
- **GPIO 15:** CMD
- **GPIO 2:** Data0
- **GPIO 4:** Data1 (also used for the onboard flash LED)
- **GPIO 12:** Data2
- **GPIO 13:** Data3
