
# Potentiometers

A potentiometer is a three-terminal variable resistor. It acts as a voltage divider and is commonly used to provide a variable analog signal to a microcontroller, for example, to control volume, brightness, or the position of a servo motor.

## How a Potentiometer Works

Inside a potentiometer, there is a resistive track and a sliding contact, or **wiper**. As you turn the knob, the wiper moves along the track.

It has three pins:

1.  **Pin 1 (CCW - Counter-Clockwise):** One end of the resistive track.
2.  **Pin 2 (Wiper):** The middle pin, connected to the sliding contact.
3.  **Pin 3 (CW - Clockwise):** The other end of the resistive track.

![Potentiometer Diagram](https://www.build-electronic-circuits.com/wp-content/uploads/2013/09/potentiometer-schematic-symbol-and-breadboard-layout.png)

## Using a Potentiometer as a Voltage Divider

This is the most common way to use a potentiometer with a microcontroller.

1.  **Connect the outer pins to power:**
    -   Connect Pin 1 to Ground (GND).
    -   Connect Pin 3 to your voltage source (e.g., 5V or 3.3V).

2.  **Connect the center pin to an analog input:**
    -   Connect Pin 2 (the wiper) to an analog input pin on your microcontroller (e.g., A0 on an Arduino).

### What Happens?

-   When the knob is turned all the way to the GND side (Pin 1), the wiper is close to GND, and the voltage on the analog pin will be close to 0V. The microcontroller will read a value close to 0.
-   When the knob is turned all the way to the VCC side (Pin 3), the wiper is close to VCC, and the voltage on the analog pin will be close to 5V. The microcontroller will read its maximum analog value (e.g., 1023 for a 10-bit ADC on an Arduino).
-   At any position in between, the wiper picks up a voltage that is proportional to its position along the resistive track, providing a smooth range of analog values.

## Reading the Value

You use the `analogRead()` function on a microcontroller to read the voltage from the wiper pin.

**Arduino Example:**

```cpp
// Connect the potentiometer's center pin to A0
int potPin = A0;

void setup() {
  Serial.begin(9600);
}

void loop() {
  // Read the analog value (from 0 to 1023)
  int potValue = analogRead(potPin);

  // Print the value to the Serial Monitor
  Serial.println(potValue);

  delay(100); // Wait a bit before the next reading
}
```

## Types of Potentiometers

-   **Linear Taper:** The resistance changes linearly as you turn the knob. If you turn the knob 50% of the way, the resistance is 50% of the total. These are used for most sensor control applications.
-   **Logarithmic (Audio) Taper:** The resistance changes logarithmically. This is used for audio applications (like volume controls) because human hearing is also logarithmic.

## Using a Potentiometer as a Rheostat

A potentiometer can also be used as a simple two-terminal variable resistor (called a rheostat). You do this by using only the wiper (Pin 2) and one of the outer pins (Pin 1 or 3). In this configuration, it can be used to control the current in a circuit, for example, to vary the brightness of an LED.
