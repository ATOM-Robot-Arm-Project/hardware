
# LEDs (Light Emitting Diodes)

An LED is a semiconductor light source that emits light when current flows through it. They are one of the most common components in electronics, used for everything from simple indicators to lighting.

## How an LED Works

-   **Diode:** An LED is a type of diode, which means it only allows current to flow in one direction.
-   **Polarity:** Because it's a diode, an LED has polarity. It has a positive lead (**anode**) and a negative lead (**cathode**).
-   **Anode (Positive):** This is typically the longer leg.
-   **Cathode (Negative):** This is typically the shorter leg. The flat edge on the side of the LED also indicates the cathode.

If you connect an LED backwards, it will not light up and can be damaged.

![LED Polarity Diagram](https://www.build-electronic-circuits.com/wp-content/uploads/2013/08/led-polarity.png)

## Why You MUST Use a Resistor with an LED

An LED has very little internal resistance. If you connect it directly to a voltage source (like a 5V pin on an Arduino), a very large amount of current will flow through it, instantly destroying the LED. This is called thermal runaway.

To prevent this, you **must** always use a **current-limiting resistor** in series with the LED.

### How to Calculate the Resistor Value

You can use Ohm's Law (V = I * R) to find the right resistor value.

**R = (Vs - Vf) / I**

-   **R:** The resistance you need (in Ohms).
-   **Vs:** The voltage of your power source (e.g., 5V for an Arduino).
-   **Vf:** The LED's forward voltage. This is the amount of voltage the LED "drops" when it's on. It varies by color (see chart below).
-   **I:** The desired current for the LED (in Amperes). A safe and common value for most 5mm LEDs is 20mA, which is **0.020A**.

### Typical LED Forward Voltages (Vf)

| Color | Forward Voltage (approx.) |
| :--- | :---: |
| Red | 1.8V - 2.2V |
| Green | 2.0V - 2.4V |
| Blue | 3.0V - 3.4V |
| White | 3.0V - 3.4V |
| Yellow | 2.0V - 2.2V |

**Example Calculation (Red LED with 5V source):**

-   Vs = 5V
-   Vf = 2.0V (average for a red LED)
-   I = 0.020A (20mA)

R = (5V - 2.0V) / 0.020A

R = 3V / 0.020A

R = 150 Ω

The closest standard resistor value is 220Ω, which is a perfect choice as it provides a little extra protection.

## Types of LEDs

-   **Through-Hole:** The standard LEDs with two legs, common in breadboarding.
-   **Surface Mount (SMD):** Tiny LEDs that are soldered directly onto a circuit board.
-   **RGB LEDs:** These combine three separate LEDs (Red, Green, and Blue) in a single package. By controlling the brightness of each color, you can create any color in the spectrum.
