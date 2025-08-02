# Raspberry Pi 4 Tutorials

These tutorials use Python and the `gpiozero` library to interact with hardware.

## Tutorial 1: Reading a Temperature and Humidity Sensor (DHT11/DHT22)

This project reads environmental data from a popular DHT sensor and prints it to the console.

**Hardware Needed:**
- 1 x Raspberry Pi 4
- 1 x DHT11 (blue) or DHT22 (white) sensor
- Jumper Wires

**Circuit:**
-   **DHT Pin 1 (VCC):** Connect to 3.3V on the Raspberry Pi.
-   **DHT Pin 2 (Data):** Connect to GPIO 4 on the Raspberry Pi.
-   **DHT Pin 4 (GND):** Connect to a GND pin on the Raspberry Pi.
(Pin 3 is not used).

**Software Setup:**
You need to install the Adafruit CircuitPython DHT library.

```bash
sudo apt-get update
sudo apt-get install python3-pip
sudo pip3 install adafruit-circuitpython-dht
sudo apt-get install libgpiod2
```

**Code (`temp_reader.py`):**
```python
import time
import board
import adafruit_dht

# Initialize the dht device, with data pin connected to:
dhtDevice = adafruit_dht.DHT22(board.D4) # Use DHT22 for DHT22, or DHT11 for DHT11

while True:
    try:
        # Print the values to the serial port
        temperature_c = dhtDevice.temperature
        temperature_f = temperature_c * (9 / 5) + 32
        humidity = dhtDevice.humidity
        print(
            "Temp: {:.1f} F / {:.1f} C    Humidity: {}%".format(
                temperature_f, temperature_c, humidity
            )
        )

    except RuntimeError as error:
        # Errors happen fairly often, DHT's are tricky that way!
        print(error.args[0])
        time.sleep(2.0)
        continue
    except Exception as error:
        dhtDevice.exit()
        raise error

    time.sleep(2.0)

```

**How it Works:**
The `adafruit_circuitpython_dht` library handles the complex timing required to read data from the DHT sensor. The script initializes the sensor on the specified GPIO pin and then enters a loop, reading the temperature and humidity every 2 seconds.

---

## Tutorial 2: Controlling a DC Motor with an L298N Driver

This project shows how to control the speed and direction of a simple DC motor.

**Hardware Needed:**
- 1 x Raspberry Pi 4
- 1 x L298N Motor Driver
- 1 x DC Motor
- An external power supply for the motor (e.g., a 9V battery or a 5V-12V power adapter). **Do not power the motor from the Pi!**
- Jumper Wires

**Circuit:**
1.  Connect the L298N's `VCC` and `GND` to your external power supply.
2.  Connect the motor to the `OUT1` and `OUT2` terminals on the L298N.
3.  Connect the L298N's `IN1` to Raspberry Pi GPIO 24.
4.  Connect the L298N's `IN2` to Raspberry Pi GPIO 23.
5.  Connect the L298N's `ENA` (Enable A) to Raspberry Pi GPIO 25.
6.  **Crucially, connect one of the Raspberry Pi's GND pins to the L298N's GND pin.** This creates a common ground, which is essential for the circuit to work.

**Code (`motor_control.py`):**
```python
from gpiozero import Motor, PWMOutputDevice
from time import sleep

# The Motor class uses two pins for direction
motor = Motor(forward=24, backward=23)

# The PWMOutputDevice is used for speed control
speed_control = PWMOutputDevice(25)

print("Motor test starting...")

try:
    while True:
        print("Full speed forward")
        motor.forward()
        speed_control.value = 1.0  # Full speed (0.0 to 1.0)
        sleep(2)

        print("Half speed forward")
        speed_control.value = 0.5
        sleep(2)

        print("Full speed backward")
        motor.backward()
        speed_control.value = 1.0
        sleep(2)

        print("Stopping")
        motor.stop()
        sleep(2)

except KeyboardInterrupt:
    print("\nExiting program.")
    motor.stop()

```

**How it Works:**
The `gpiozero` `Motor` class simplifies motor control. It uses one pin for forward and another for backward. The `PWMOutputDevice` is used on the L298N's "Enable" pin to control the motor's speed. A `value` of 1.0 is full speed, and 0.0 is stopped.

