
# How to Program an Arduino

Programming an Arduino is done using the Arduino IDE (Integrated Development Environment), a free software that runs on your computer.

## 1. Download and Install the Arduino IDE

- Go to the official Arduino website: [https://www.arduino.cc/en/software](https://www.arduino.cc/en/software)
- Download the version of the IDE that is compatible with your operating system (Windows, macOS, or Linux).
- Follow the installation instructions.

## 2. Connect the Arduino to Your Computer

- Use a USB cable to connect your Arduino board to your computer.
- The green power LED on the board should light up.

## 3. Configure the Arduino IDE

- **Select your board:** Go to `Tools > Board` and select the type of Arduino board you are using (e.g., "Arduino Uno").
- **Select the port:** Go to `Tools > Port` and select the serial port that your Arduino is connected to. This will usually be a COM port on Windows or a `/dev/tty.usbmodem` port on macOS.

## 4. Write Your First Sketch (Program)

An Arduino program is called a "sketch." Here is a simple example that blinks the built-in LED on the board:

```cpp
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

## 5. Upload the Sketch to the Arduino

- Click the "Upload" button (the right-arrow icon) in the Arduino IDE.
- The IDE will compile the sketch and upload it to your Arduino board.
- You should see the built-in LED on your board start to blink.
