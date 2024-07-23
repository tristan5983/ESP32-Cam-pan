# ESP32-Cam-pan


Overview
The code turns an ESP32 module into a web-controlled pan-tilt camera system using an ESP32-CAM board. It sets up the ESP32 as a WiFi Access Point (AP) named "ESP32-CAM-AP" with a specified password. Clients can connect to this AP to control the camera's movement and view the live stream from the camera.

Components and Libraries Used
ESP32 Libraries: The code utilizes libraries specific to the ESP32 platform for handling WiFi communication (WiFi.h), camera interfacing (esp_camera.h), and HTTP server functionality (esp_http_server.h).

Servo Control: Two servos (Servo1 and Servo2) are used for controlling pan and tilt movements of the camera module.

Functionality
Setup Function (setup())
Disable Brownout Detector: Ensures stable operation by disabling the brownout detector.

Servo Initialization: Configures two servos (Servo1 and Servo2) attached to GPIO pins SERVO_1 and SERVO_2, respectively, for controlling pan and tilt movements.

Serial Communication: Initializes serial communication for debugging and informational messages.

Camera Initialization:

Configures camera pins and parameters (camera_config_t).
Initializes the camera using esp_camera_init().
WiFi Access Point Setup:

Configures the ESP32 as an Access Point (WiFi.softAP()).
Sets the SSID to "ESP32-CAM-AP" and password to "password" (replace with desired credentials).
Server Setup:

Starts an HTTP server to handle requests.
Registers URIs (/, /action, /stream) for serving the web interface (index_handler()), handling camera movement commands (cmd_handler()), and streaming MJPEG video (stream_handler()).
Prints IP Address: Displays the IP address of the Access Point (WiFi.softAPIP()) on the Serial Monitor for clients to connect.

Loop Function (loop())
The loop() function in this code is empty (void loop() {}), indicating that the main program loop does not contain any continuous tasks. Instead, the functionality relies on callbacks and event-driven operations handled by the HTTP server and camera functions.
Web Interface (INDEX_HTML)
The code includes an HTML page (INDEX_HTML) embedded in the program memory.
This page provides a basic interface for controlling the camera:
Displays a live stream from the camera.
Offers buttons for panning and tilting the camera (Up, Down, Left, Right).
Uses JavaScript to send HTTP requests (XMLHttpRequest) to the ESP32 server when buttons are pressed.
HTTP Request Handlers
index_handler(): Handles requests to the root URI ("/") and serves the embedded HTML page (INDEX_HTML).

stream_handler(): Manages MJPEG streaming of camera images. Retrieves frames from the camera, converts them to JPEG format, and streams them in a multipart response.

cmd_handler(): Processes commands (Up, Down, Left, Right) sent via HTTP GET requests. Adjusts servo positions based on the command received.

Error Handling
The code includes basic error handling (ESP_FAIL, ESP_OK) for camera operations, WiFi initialization, and HTTP server operations.
Errors are logged to the Serial Monitor (Serial.println()).
Usage
Connecting to the Access Point:

Users connect their devices to the WiFi network named "ESP32-CAM-AP" using the password "password".
Controlling the Camera:

Users open a web browser and navigate to the IP address displayed on the Serial Monitor (http://<ESP32-AP-IP>/).
They can view the live stream from the camera and use the provided buttons to pan and tilt the camera in real-time.
Functionality Expansion:

The code can be extended by modifying the HTML interface (INDEX_HTML) or adding additional HTTP request handlers to support more complex functionalities.
Conclusion
In summary, the provided code turns the ESP32-CAM module into a standalone WiFi-controlled pan-tilt camera system. It leverages the ESP32's capabilities for WiFi communication, camera interfacing, and web server operations to offer a user-friendly interface for remote camera control and monitoring.



