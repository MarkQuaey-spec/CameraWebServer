# CameraWebServer

OV2640 camera web server for the Freenove ESP32-S3-WROOM, built on the Espressif `esp32` Arduino core's CameraWebServer example.

## Hardware

- Freenove ESP32-S3-WROOM board with OV2640 camera module (PSRAM required for UXGA resolution / high JPEG quality)
- USB cable for flashing

## Arduino IDE Setup

1. Install the [ESP32 board package](https://github.com/espressif/arduino-esp32) in Arduino IDE (Boards Manager → search "esp32").
2. Select board: **ESP32S3 Dev Module** (or your specific Freenove S3 variant).
3. Board menu settings:
   - PSRAM: **OPI PSRAM** (or `enabled`, depending on package version)
   - Partition Scheme: **Custom** (uses `partitions.csv` in this repo — needs at least 3MB APP space)
   - Flash Mode: **QIO**
   - USB Mode: default
4. Open `CameraWebServer.ino` in Arduino IDE.

## Configuration

1. In `board_config.h`, confirm the correct camera model is uncommented. This repo defaults to:
   ```cpp
   #define CAMERA_MODEL_ESP32S3_EYE
   ```
2. In `CameraWebServer.ino`, set your WiFi credentials (left blank in this repo — **do not commit real credentials**):
   ```cpp
   const char *ssid = "YOUR_WIFI_SSID";
   const char *password = "YOUR_WIFI_PASSWORD";
   ```

## Flashing

1. Connect the board via USB and select the correct serial port.
2. Click Upload.
3. Open the Serial Monitor at 115200 baud.
4. On successful WiFi connection, the IP address of the camera stream will be printed, e.g.:
   ```
   Camera Ready! Use 'http://192.168.x.x' to connect
   ```
5. Open that address in a browser to view the stream and controls.

## Notes

- Never commit real WiFi credentials to this repo — keep `ssid`/`password` blank in source control and fill them in locally before flashing.
- `partitions.csv` defines a custom partition table; make sure the IDE's Partition Scheme is set to **Custom** or the build will fail/overflow.
