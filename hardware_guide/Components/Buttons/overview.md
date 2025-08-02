
# Buttons and Switches

A button or switch is a simple component that controls the flow of current in a circuit by opening or closing the connection.

## How They Work

-   **Normally Open (NO):** This is the most common type of push button. The circuit is disconnected (open) by default. When you press the button, it completes the circuit (closes it), allowing current to flow.
-   **Normally Closed (NC):** The circuit is connected (closed) by default. When you press the button, it breaks the circuit (opens it), stopping the current flow.

## The Problem of Floating Pins

When you connect a button to a microcontroller's input pin, you need to know its state: is it pressed or not pressed? This corresponds to a digital HIGH or LOW.

If you just connect a button to an input pin and VCC (e.g., 5V), the pin will be HIGH when pressed. But what about when it's not pressed? The input pin is not connected to anything, which is called a **floating state**. In this state, the pin can randomly read HIGH or LOW due to electrical noise, leading to unreliable behavior.

To fix this, we must use **pull-up** or **pull-down** resistors.

## Pull-up and Pull-down Resistors

These resistors ensure the input pin is always in a known, stable state.

### 1. Pull-down Resistor

-   **How it works:** A resistor (typically 10kΩ) is connected from the input pin to Ground (GND).
-   **Behavior:**
    -   When the button is **not pressed**, the resistor "pulls" the input pin's voltage down to GND. The pin reads **LOW**.
    -   When the button **is pressed**, it connects the input pin directly to VCC (5V), overriding the resistor. The pin reads **HIGH**.

![Pull-down Resistor Diagram](https://www.upesy.com/wp-content/uploads/2021/09/pull-down-resistor-schematic.png)

### 2. Pull-up Resistor

-   **How it works:** A resistor (typically 10kΩ) is connected from the input pin to VCC (5V).
-   **Behavior:**
    -   When the button is **not pressed**, the resistor "pulls" the input pin's voltage up to VCC. The pin reads **HIGH**.
    -   When the button **is pressed**, it connects the input pin directly to GND, overriding the resistor. The pin reads **LOW**.

![Pull-up Resistor Diagram](https://www.upesy.com/wp-content/uploads/2021/09/pull-up-resistor-schematic.png)

**Note:** The logic is inverted with a pull-up resistor (pressed = LOW).

## Internal Pull-ups

Most microcontrollers (including Arduino and Raspberry Pi) have **internal pull-up resistors** that you can enable in your code. This is extremely convenient as it means you don't need to add an external resistor to your circuit.

**Arduino Example:**
```cpp
// Enables the internal pull-up resistor on pin 2
pinMode(2, INPUT_PULLUP);
```

When using `INPUT_PULLUP`, you simply wire the button between the input pin and GND. The pin will be HIGH when not pressed and LOW when pressed.

## Debouncing

When you press a mechanical button, the metal contacts can bounce against each other for a few milliseconds before settling. A microcontroller is fast enough to read these bounces as multiple, separate presses.

**Debouncing** is the technique used to handle this, ensuring only one press is registered.

-   **Software Debouncing:** The most common method. After detecting a press, you can add a small delay (e.g., 50ms) in your code and then read the button state again to make sure it's still pressed.
-   **Hardware Debouncing:** Can be done by adding a small capacitor to the circuit.
