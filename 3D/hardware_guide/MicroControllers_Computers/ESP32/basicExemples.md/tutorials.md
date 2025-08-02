
# ESP32 Tutorials

These tutorials leverage the unique features of the ESP32, like Wi-Fi and Bluetooth.

## Tutorial 1: Web Server to Control an LED

This project creates a simple web server on your network. You can visit the server's IP address in a browser to turn an LED connected to the ESP32 on or off.

**Hardware Needed:**
- 1 x ESP32 Development Board
- 1 x Breadboard
- 1 x LED
- 1 x 330Ω Resistor
- Jumper Wires

**Circuit:**
1.  Connect the LED's longer leg (anode) to a 330Ω resistor.
2.  Connect the other end of the resistor to GPIO 2 on the ESP32.
3.  Connect the LED's shorter leg (cathode) to a GND pin on the ESP32.

**Code:**
*Remember to add your Wi-Fi credentials to the code.*
```cpp
#include <WiFi.h>

// Replace with your network credentials
const char* ssid = "YOUR_SSID";
const char* password = "YOUR_PASSWORD";

// Set web server port number to 80
WiFiServer server(80);

// Variable to store the HTTP request
String header;

// GPIO where the LED is connected
const int ledPin = 2;

void setup() {
  Serial.begin(115200);
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, LOW);

  // Connect to Wi-Fi
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  // Print local IP address and start web server
  Serial.println("\nWiFi connected.");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
  server.begin();
}

void loop(){
  WiFiClient client = server.available();

  if (client) {
    String currentLine = "";
    while (client.connected()) {
      if (client.available()) {
        char c = client.read();
        header += c;
        if (c == '\n') {
          if (currentLine.length() == 0) {
            // HTTP headers
            client.println("HTTP/1.1 200 OK");
            client.println("Content-type:text/html");
            client.println("Connection: close");
            client.println();

            // Web page content
            if (header.indexOf("GET /2/on") >= 0) {
              digitalWrite(ledPin, HIGH);
            } else if (header.indexOf("GET /2/off") >= 0) {
              digitalWrite(ledPin, LOW);
            }
            client.println("<!DOCTYPE html><html>");
            client.println("<head><meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">");
            client.println("<style>html { font-family: Helvetica; display: inline-block; margin: 0px auto; text-align: center;}");
            client.println(".button { background-color: #4CAF50; border: none; color: white; padding: 16px 40px; text-decoration: none; font-size: 30px; margin: 2px; cursor: pointer;}");
            client.println(".button2 {background-color: #555555;}</style></head>");
            client.println("<body><h1>ESP32 Web Server</h1>");
            client.println("<p><a href=\"/2/on\"><button class=\"button\">ON</button></a></p>");
            client.println("<p><a href=\"/2/off\"><button class=\"button button2\">OFF</button></a></p>");
            client.println("</body></html>");
            client.println();
            break;
          }
        }
        else { 
          currentLine += c;
        }
      }
    }
    header = "";
    client.stop();
  }
}
```

**How it Works:**
The ESP32 connects to your Wi-Fi and starts a web server. When you visit its IP address, it serves a simple HTML page with "ON" and "OFF" buttons. Clicking these buttons sends a request back to the ESP32 (e.g., `http://[IP]/2/on`), which the code checks for to turn the LED on or off.

---

## Tutorial 2: Bluetooth Low Energy (BLE) Scanner

This project uses the ESP32's BLE capabilities to scan for nearby Bluetooth devices and print their information to the Serial Monitor.

**Hardware Needed:**
- 1 x ESP32 Development Board

**Code:**
```cpp
#include <BLEDevice.h>
#include <BLEUtils.h>
#include <BLEScan.h>
#include <BLEAdvertisedDevice.h>

int scanTime = 5; //In seconds
BLEScan* pBLEScan;

class MyAdvertisedDeviceCallbacks: public BLEAdvertisedDeviceCallbacks {
    void onResult(BLEAdvertisedDevice advertisedDevice) {
      Serial.printf("Advertised Device: %s \n", advertisedDevice.toString().c_str());
    }
};

void setup() {
  Serial.begin(115200);
  Serial.println("Scanning...");

  BLEDevice::init("");
  pBLEScan = BLEDevice::getScan(); //create new scan
  pBLEScan->setAdvertisedDeviceCallbacks(new MyAdvertisedDeviceCallbacks());
  pBLEScan->setActiveScan(true); //active scan uses more power, but get results faster
  pBLEScan->setInterval(100);
  pBLEScan->setWindow(99);
}

void loop() {
  // put your main code here, to run repeatedly:
  BLEScanResults foundDevices = pBLEScan->start(scanTime, false);
  Serial.print("Devices found: ");
  Serial.println(foundDevices.getCount());
  Serial.println("Scan done!");
  pBLEScan->clearResults();   // delete results fromBLEScan buffer to release memory
  delay(2000);
}
```

**How it Works:**
The ESP32 initializes its BLE radio and performs a scan for a set duration (`scanTime`). When it discovers a device that is advertising its presence, the `onResult` callback function is triggered, printing the device's address and other available information to the serial port.
