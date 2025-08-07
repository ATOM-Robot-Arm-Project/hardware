

# Raspberry Pi Zero 2 W Tutorials

Programming the Pi Zero 2 W is identical to any other Raspberry Pi. These tutorials focus on projects that are well-suited to its small size and lower power consumption.

## Tutorial 1: Creating a Wireless Network Scanner

This project turns your Pi Zero 2 W into a portable device that can scan for Wi-Fi networks and display their details. This is great for a "headless" (no monitor) setup.

**Hardware Needed:**
- 1 x Raspberry Pi Zero 2 W
- A power source (e.g., a USB power bank)

**Software Setup:**
This project uses standard Python libraries that come with Raspberry Pi OS.

**Code (`wifi_scanner.py`):**
```python
import subprocess
import time

def scan_wifi():
    """Scans for Wi-Fi networks and returns a list of SSIDs."""
    try:
        # Use the nmcli tool to scan for networks
        scan_result = subprocess.check_output(['nmcli', 'dev', 'wifi'], text=True)
        networks = []
        for line in scan_result.split('\n'):
            if line.strip().startswith('*'):
                # This is the currently connected network
                continue
            if len(line.strip()) > 0 and not line.startswith('IN-USE'):
                parts = line.strip().split()
                if len(parts) > 1:
                    ssid = parts[1]
                    if ssid != '--':
                        networks.append(ssid)
        return list(set(networks)) # Return unique SSIDs
    except (subprocess.CalledProcessError, FileNotFoundError):
        print("Could not execute nmcli. Make sure it's installed.")
        return []

if __name__ == "__main__":
    print("Starting Wi-Fi scan... Press Ctrl+C to stop.")
    try:
        while True:
            print("\n--- New Scan ---")
            found_networks = scan_wifi()
            if found_networks:
                for network in found_networks:
                    print(f"Found network: {network}")
            else:
                print("No networks found.")
            time.sleep(10) # Wait 10 seconds before scanning again
    except KeyboardInterrupt:
        print("\nScan stopped.")

```

**How to Run (Headless):**
1.  Save this script on your Pi Zero 2 W.
2.  SSH into your Pi from another computer.
3.  Run the script: `python wifi_scanner.py`
4.  The Pi will continuously scan for and display the names (SSIDs) of nearby Wi-Fi networks.

---

## Tutorial 2: Headless Button-Controlled LED

This project shows how to control an LED with a button without needing a monitor. It's a perfect example of a simple, embedded application for the Zero 2 W.

**Hardware Needed:**
- 1 x Raspberry Pi Zero 2 W (with soldered GPIO header)
- 1 x Breadboard
- 1 x LED
- 1 x 330Ω Resistor
- 1 x Push Button
- Jumper Wires

**Circuit:**
1.  **LED:** Connect the longer leg to a 330Ω resistor, and the other end of the resistor to GPIO 17. Connect the shorter leg to GND.
2.  **Button:** Connect one leg to GPIO 2 and the other leg to GND.

**Code (`headless_button.py`):**
```python
from gpiozero import LED, Button
from signal import pause

# Initialize the LED on GPIO 17
led = LED(17)

# Initialize the Button on GPIO 2
# The internal pull-up resistor is enabled by default
button = Button(2, pull_up=True)

print("Program is running. Press the button to toggle the LED.")
print("Press Ctrl+C in the terminal to exit.")

# The toggle() function flips the state of the LED
button.when_pressed = led.toggle

# pause() keeps the script running in the background
pause()
```

**How it Works:**
1.  SSH into your Pi Zero 2 W.
2.  Run the script: `python headless_button.py`
3.  The script will run in the foreground. You can now press the physical button connected to your Pi, and the LED will turn on and off. The `pause()` function is essential for keeping the script alive to listen for button presses.

```