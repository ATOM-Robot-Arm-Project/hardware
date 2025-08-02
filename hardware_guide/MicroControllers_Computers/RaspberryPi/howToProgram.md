
# How to Program a Raspberry Pi

Programming a Raspberry Pi is different from programming a microcontroller. Since the Raspberry Pi is a full computer running an operating system (like Raspberry Pi OS), you write and run code directly on the device itself.

## 1. Setting Up Your Raspberry Pi

First, you need to get your Raspberry Pi running.

- **Install Raspberry Pi OS:** Download the Raspberry Pi Imager from the [official website](https://www.raspberrypi.com/software/) and use it to flash the Raspberry Pi OS onto a microSD card.
- **Initial Boot:** Insert the microSD card into your Pi, connect a monitor, keyboard, mouse, and power supply, and turn it on.
- **Complete Setup:** Follow the on-screen instructions to set up your location, password, and connect to Wi-Fi.

## 2. Accessing Your Raspberry Pi

You have two main ways to work with your Raspberry Pi:

- **Desktop Environment:** Use it like a regular computer with the connected monitor, keyboard, and mouse.
- **Headless (Remote Access):** Access your Pi from another computer over the network using SSH (for a command-line interface) or VNC (for the full graphical desktop). This is very common for robotics and embedded projects.

To enable SSH and VNC, open the Raspberry Pi Configuration tool (`Menu > Preferences > Raspberry Pi Configuration > Interfaces`) and enable them.

## 3. Programming Languages

Python is the most popular and officially recommended language for programming on the Raspberry Pi. Raspberry Pi OS comes with Python and several useful libraries pre-installed.

### Writing and Running a Python Script

1.  **Open a Code Editor:** You can use the pre-installed **Thonny IDE**, which is excellent for beginners, or any other text editor like VS Code (which can be installed on the Pi).
2.  **Write Your Code:** Create a new file and write your Python code. For example, a simple "Hello, World!" script named `hello.py`:
    ```python
    print("Hello from the Raspberry Pi!")
    ```
3.  **Save the File:** Save the script in your home directory or a project folder.
4.  **Run from the Terminal:**
    - Open the **Terminal** application.
    - Navigate to the directory where you saved your file using the `cd` command (e.g., `cd my_project`).
    - Run the script using the python interpreter:
      ```bash
      python hello.py
      ```

## 4. Controlling GPIO Pins

The real power for physical computing comes from the GPIO (General-Purpose Input/Output) pins. You can use Python libraries to control them.

- **gpiozero:** A modern, beginner-friendly library for controlling GPIO devices.
- **RPi.GPIO:** The classic, more traditional library for GPIO control.

### Example: Blinking an LED with `gpiozero`

1.  **Connect the Hardware:** Connect an LED to GPIO pin 17 and a ground pin on the Raspberry Pi (don't forget a resistor!).
2.  **Write the Python Script:**
    ```python
    from gpiozero import LED
    from time import sleep

    led = LED(17)

    while True:
        led.on()
        sleep(1)
        led.off()
        sleep(1)
    ```
3.  **Run the Script:** Save the code and run it from the terminal (`python blink.py`). The LED should start blinking.
