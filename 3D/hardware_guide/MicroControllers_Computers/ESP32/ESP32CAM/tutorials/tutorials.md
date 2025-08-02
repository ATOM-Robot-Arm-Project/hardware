

# ESP32-CAM Tutorials

Here are some tutorials to help you get started with the ESP32-CAM.

## 1. Camera Web Server

This is the most popular ESP32-CAM project. It hosts a web page on your local network that streams video from the camera.

### Arduino IDE Setup

1.  **Board:** In the Arduino IDE, go to `Tools > Board` and select "AI Thinker ESP32-CAM".
2.  **Example Sketch:** Go to `File > Examples > ESP32 > Camera` and open the `CameraWebServer` example.

### Code Configuration

In the `CameraWebServer` sketch, you need to make a few changes:

1.  **Select Camera Model:** Uncomment the line for the AI-Thinker model:
    ```cpp
    #define CAMERA_MODEL_AI_THINKER
    ```
2.  **Enter Wi-Fi Credentials:** Find the following lines and replace `ssid` and `password` with your Wi-Fi network's name and password:
    ```cpp
    const char* ssid = "YOUR_SSID";
    const char* password = "YOUR_PASSWORD";
    ```

### Upload and Run

1.  Follow the programming connections and procedure outlined in the `conections.md` file (connect `GPIO 0` to `GND`).
2.  Upload the sketch.
3.  Disconnect `GPIO 0` from `GND` and press the reset button.
4.  Open the Serial Monitor and set the baud rate to `115200`.
5.  The ESP32-CAM will connect to your Wi-Fi and print its IP address in the Serial Monitor.
6.  Open a web browser on a device connected to the same Wi-Fi network and enter the IP address.
7.  You should see a web page with a video stream from your camera!

## 2. Taking a Photo and Saving to MicroSD Card

This project shows you how to capture an image and save it as a `.jpg` file on a MicroSD card.

### Arduino IDE Setup

1.  Make sure you have the ESP32 board support installed.
2.  Insert a formatted MicroSD card into the ESP32-CAM's card slot.

### Example Code

This code initializes the camera and the SD card, takes a picture, and saves it. You can then trigger this action with a button press or another sensor.

```cpp
#include "esp_camera.h"
#include "FS.h"
#include "SD_MMC.h"

// Pin definition for CAMERA_MODEL_AI_THINKER
#define PWDN_GPIO_NUM     32
#define RESET_GPIO_NUM    -1
#define XCLK_GPIO_NUM      0
#define SIOD_GPIO_NUM     26
#define SIOC_GPIO_NUM     27
#define Y9_GPIO_NUM       35
#define Y8_GPIO_NUM       34
#define Y7_GPIO_NUM       39
#define Y6_GPIO_NUM       36
#define Y5_GPIO_NUM       21
#define Y4_GPIO_NUM       19
#define Y3_GPIO_NUM       18
#define Y2_GPIO_NUM        5
#define VSYNC_GPIO_NUM    25
#define HREF_GPIO_NUM     23
#define PCLK_GPIO_NUM     22

void setup() {
  Serial.begin(115200);
  Serial.setDebugOutput(true);
  Serial.println();

  camera_config_t config;
  // ... (camera configuration - see full example online) ...

  // initialize the camera
  esp_err_t err = esp_camera_init(&config);
  if (err != ESP_OK) {
    Serial.printf("Camera init failed with error 0x%x", err);
    return;
  }

  if(!SD_MMC.begin()){
    Serial.println("Card Mount Failed");
    return;
  }
  uint8_t cardType = SD_MMC.cardType();
  if(cardType == CARD_NONE){
    Serial.println("No SD card attached");
    return;
  }

  // Take a picture
  camera_fb_t * fb = esp_camera_fb_get();
  if(!fb) {
    Serial.println("Camera capture failed");
    return;
  }

  // Save picture to microSD card
  fs::FS &fs = SD_MMC;
  String path = "/picture.jpg";
  File file = fs.open(path.c_str(), FILE_WRITE);
  if(!file){
    Serial.println("Failed to open file in writing mode");
  } else {
    file.write(fb->buf, fb->len); // payload (image), payload length
    Serial.printf("Saved file to path: %s\n", path.c_str());
  }
  file.close();
  esp_camera_fb_return(fb);
}

void loop() {
  // Code in setup runs once
}
```
*Note: This is a simplified version. For the full, working code, please refer to online tutorials from resources like Random Nerd Tutorials.*

