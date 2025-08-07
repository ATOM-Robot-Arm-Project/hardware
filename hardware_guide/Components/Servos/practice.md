# Servo Tutorials

This section provides tutorials for using servo motors in your robotics projects.

## 1. Basic Servo Control with Arduino

This tutorial demonstrates how to control a servo motor using an Arduino board.

### Components

- Arduino Uno
- Standard Servo Motor
- Jumper Wires

### Circuit

1. Connect the servo's **GND** (brown or black wire) to the Arduino's **GND** pin.
2. Connect the servo's **VCC** (red wire) to the Arduino's **5V** pin.
3. Connect the servo's **Signal** (orange or yellow wire) to a PWM-capable pin on the Arduino, such as pin 9.

### Code

```cpp
#include <Servo.h>

Servo myServo;

void setup() {
  myServo.attach(9); // Attaches the servo on pin 9 to the servo object
}

void loop() {
  myServo.write(0);    // Move the servo to 0 degrees
  delay(1000);         // Wait for a second
  myServo.write(90);   // Move the servo to 90 degrees
  delay(1000);         // Wait for a second
  myServo.write(180);  // Move the servo to 180 degrees
  delay(1000);         // Wait for a second
}
```

### Instructions

1.  Upload the code to your Arduino board.
2.  The servo will sweep back and forth between 0, 90, and 180 degrees.

## 2. Controlling a Servo with a Potentiometer

This tutorial shows how to control the position of a servo motor using a potentiometer.

### Components

- Arduino Uno
- Standard Servo Motor
- 10kΩ Potentiometer
- Jumper Wires

### Circuit

1.  Connect the servo as described in the previous tutorial.
2.  Connect one of the potentiometer's outer pins to **GND**.
3.  Connect the other outer pin to **5V**.
4.  Connect the center pin to an analog input pin on the Arduino, such as **A0**.

### Code

```cpp
#include <Servo.h>

Servo myServo;
int potPin = A0;
int potValue;
int angle;

void setup() {
  myServo.attach(9);
}

void loop() {
  potValue = analogRead(potPin);
  angle = map(potValue, 0, 1023, 0, 180);
  myServo.write(angle);
  delay(15);
}
```

### Instructions

1.  Upload the code to your Arduino board.
2.  Turn the potentiometer to control the position of the servo motor.
