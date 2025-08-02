
# Raspberry Pi Basic Examples (Python)

These examples use the `gpiozero` library, which is a friendly and intuitive way to interact with the GPIO pins on a Raspberry Pi.

## 1. Blinking an LED

This is the fundamental "Hello, World!" of physical computing.

**Hardware:**
- 1 x LED
- 1 x 330Ω Resistor
- Connect the longer leg (anode) of the LED to GPIO pin 17.
- Connect the shorter leg (cathode) to the resistor, and the other end of the resistor to a Ground (GND) pin.

**Code (`blink.py`):**
```python
from gpiozero import LED
from time import sleep

# Initialize the LED on GPIO pin 17
led = LED(17)

print("LED will blink. Press Ctrl+C to exit.")

try:
    while True:
        led.on()  # Turn the LED on
        sleep(1)  # Wait for 1 second
        led.off() # Turn the LED off
        sleep(1)  # Wait for 1 second
except KeyboardInterrupt:
    print("\nExiting program.")
    led.off() # Ensure LED is off when program exits
```

**To Run:**
```bash
python blink.py
```

## 2. Reading a Button Press

This example shows how to get digital input from a push button.

**Hardware:**
- 1 x Push Button
- Connect one leg of the button to GPIO pin 2.
- Connect the other leg to a Ground (GND) pin.

**Code (`button_test.py`):**
```python
from gpiozero import Button
from time import sleep

# Initialize the Button on GPIO pin 2
# The internal pull-up resistor is enabled by default
button = Button(2)

print("Press the button. Press Ctrl+C to exit.")

try:
    while True:
        if button.is_pressed:
            print("Button is pressed")
        else:
            print("Button is not pressed")
        sleep(0.1)
except KeyboardInterrupt:
    print("\nExiting program.")
```

**To Run:**
```bash
python button_test.py
```

## 3. Button-Controlled LED

This combines the previous two examples.

**Hardware:**
- Same as the LED and Button examples above.

**Code (`button_led.py`):**
```python
from gpiozero import LED, Button
from signal import pause

led = LED(17)
button = Button(2)

print("Press the button to turn the LED on/off. Press Ctrl+C to exit.")

# The following lines link the button's state to the LED's state
# button.when_pressed = led.on
# button.when_released = led.off

# A more direct way to do the same thing:
led.source = button.values

# pause() keeps the script running until you exit with Ctrl+C
pause()
```

**To Run:**
```bash
python button_led.py
```

