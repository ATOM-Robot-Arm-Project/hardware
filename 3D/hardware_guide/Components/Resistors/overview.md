
# Resistors

A resistor is a fundamental passive electronic component that creates resistance in the flow of electric current. Its purpose is to limit current, divide voltage, and in some cases, generate heat.

## What Does a Resistor Do?

Imagine electricity flowing through a wire is like water flowing through a pipe. A resistor is like a narrow section of that pipe, which restricts the flow.

Key functions:

-   **Current Limiting:** This is the most common use. For example, an LED (Light Emitting Diode) can be destroyed if too much current flows through it. A resistor is placed in series with the LED to limit the current to a safe level.
-   **Voltage Division:** Two or more resistors can be used to create a voltage divider, which produces a lower, stable voltage from a higher voltage source. This is very useful for providing a specific reference voltage to a component or reading sensors.
-   **Pull-up and Pull-down:** In digital logic, resistors are used to ensure that a pin is in a known state (either HIGH or LOW) when it would otherwise be "floating," such as when a button is not being pressed.

## Units of Resistance

The unit of electrical resistance is the **Ohm (Ω)**.

You will commonly see values in:

-   **Ohms (Ω)**
-   **Kilo-ohms (kΩ):** 1 kΩ = 1,000 Ω
-   **Mega-ohms (MΩ):** 1 MΩ = 1,000,000 Ω

## How to Read a Resistor (Color Codes)

Through-hole resistors are too small to have their value printed on them. Instead, they use a system of colored bands.

![Resistor Color Code Chart](https://www.build-electronic-circuits.com/wp-content/uploads/2011/11/4-band-resistor-color-code-chart.png)

### 4-Band Resistors:

-   **Band 1:** First digit of the resistance value.
-   **Band 2:** Second digit of the resistance value.
-   **Band 3:** Multiplier (the number of zeros to add).
-   **Band 4:** Tolerance (how accurate the resistor's value is). Gold is ±5%, Silver is ±10%.

**Example:**

A resistor has the colors: **Brown, Black, Red, Gold**

1.  **Brown:** 1
2.  **Black:** 0
3.  **Red:** x 100 (or add two zeros)
4.  **Gold:** ±5% tolerance

So, the value is **10** followed by **two zeros** = **1000 Ω** or **1 kΩ**, with a ±5% tolerance.

## Ohm's Law

The relationship between voltage (V), current (I), and resistance (R) is defined by Ohm's Law:

**V = I * R**

-   **V:** Voltage (in Volts)
-   **I:** Current (in Amperes)
-   **R:** Resistance (in Ohms)

This is the most important formula in basic electronics. You can use it to calculate the correct resistor value needed for a specific application, like protecting an LED.
