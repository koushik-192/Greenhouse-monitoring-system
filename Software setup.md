# SOFTWARE SETUP  
## Overview:  
The software setup is a crucial step in configuring the development environment to enable communication between the microcontroller 
and the computer. It involves installing necessary tools, writing the microcontroller program, and configuring the serial communication 
terminal (MiniCom) to visualize data transmission.  
## Tools Required:  
- Integrated Development Environment (IDE)  
   A software tool to write, compile, and upload code to the microcontroller.
  Examples:  
    - Arduino IDE (for Arduino boards)
    - STM32CubeIDE (for STM32 boards)  
    - PlatformIO (for ESP32/ESP8266 boards)
- MiniCom  
 - A serial communication terminal to receive and display data sent over UART.  
 - MiniCom is open-source and widely used on Linux systems.  
## Steps for Software Setup:  
### Step 1: Install MiniCom  
- Open a terminal and update the system:  
```
sudo apt update
```
- Install MiniCom:  
```  
sudo apt install minicom
```

### Step 2: Identify the Serial Port  
Run the following command to find the active serial port: 
```
dmesg | grep tty 
```
- Note the port name (e.g., /dev/ttyUSB0 or /dev/ttyACM0).
- Here, /dev/ttyUSB0 is used.
 
### Step 3: Configure MiniCom  
-Launch MiniCom with root privileges to allow access to the serial port:  
```
sudo minicom -s
```
![WhatsApp Image 2026-02-21 at 2 50 26 PM (3)](https://github.com/user-attachments/assets/d17ac7ae-089a-48b5-b45b-8477d3311de4)
In the Configuration Menu, select Serial port setup and set the following parameters:  
- Serial Device: /dev/ttyUSB0 (or your identified port).
- Bps/Par/Bits : 9600  
- Flow Control: Disable hardware and software flow control.
![Setup](https://github.com/user-attachments/assets/e68b4202-be51-46cd-9733-52a44137d563)
Save the configuration and exit the menu to start the terminal. 

### Step 4: Write and Upload Microcontroller Code  
Upload the following code into Arduino:
```
 void #include <DHT.h> 
#include <Arduino.h> 
 
#define DHTPIN 2       // DHT11 data pin 
#define DHTTYPE DHT11  // DHT11 sensor type 
#define LEDPIN 9       // LED connected to pin 9 
 
DHT dht(DHTPIN, DHTTYPE); // Initialize DHT sensor 
 
int mode = 0;  // 1 = Automatic, 2 = Manual
unsigned long previousMillis = 0; 
const long interval = 2000; // 2-second delay in automatic mode 
 
void setup() { 
  Serial.begin(9600);  // Initialize UART communication 
  dht.begin();         // Initialize DHT sensor 
  pinMode(LEDPIN, OUTPUT); // Set LED pin as output 
  displayModeSelection();   // Show initial mode selection 
} 
 
void loop() { 
  // Handle UART input 
  if (Serial.available() > 0) { 
    String command = Serial.readStringUntil('\n'); 
    command.trim();  // Remove extra whitespace 
    if (command == "0") { 
      mode = 0; 
      displayModeSelection(); 
    } else if (mode == 0) { 
      handleModeSelection(command); 
    } else if (mode == 2) { 
      handleManualCommand(command); 
    } 
  } 
 
  // Automatic Mode: Temperature display & LED adjustment every 2 seconds 
  if (mode == 1) { 
    unsigned long currentMillis = millis(); 
    if (currentMillis - previousMillis >= interval) {  
      previousMillis = currentMillis; 
      displayTemperature(); 
      adjustLEDBrightness(); 
    } 
  } 
} 
 
void displayModeSelection() { 
  Serial.println("Select Mode:"); 
  Serial.println("1: Automatic (Temperature-based LED brightness)"); 
  Serial.println("2: Manual (LED brightness control)"); 
} 
 
void handleModeSelection(String command) { 
  if (command == "1") { 
    mode = 1; 
    Serial.println("Automatic mode selected. Press '0' to return to mode selection."); 
  } else if (command == "2") { 
    mode = 2; 
    displayManualOptions(); 
  } else { 
    Serial.println("Invalid selection. Please enter '1' for automatic or '2' for manual."); 
  } 
} 
 
void displayManualOptions() { 
  Serial.println("Manual mode selected:"); 
  Serial.println("1: 0% brightness"); 
  Serial.println("2: 25% brightness");   
  Serial.println("3: 50% brightness"); 
  Serial.println("4: 75% brightness"); 
  Serial.println("5: 100% brightness"); 
  Serial.println("Press 't' to display current temperature."); 
  Serial.println("Press '0' to switch modes."); 
} 
 
void handleManualCommand(String command) { 
  // Handle LED brightness control commands 
  if (command == "1") { 
    analogWrite(LEDPIN, 0); // 0% brightness 
    Serial.println("LED Brightness set to 0%."); 
  } else if (command == "2") { 
    analogWrite(LEDPIN, 64); // 25% brightness 
    Serial.println("LED Brightness set to 25%."); 
  } else if (command == "3") { 
    analogWrite(LEDPIN, 127); // 50% brightness 
    Serial.println("LED Brightness set to 50%."); 
  } else if (command == "4") { 
    analogWrite(LEDPIN, 191); // 75% brightness 
    Serial.println("LED Brightness set to 75%."); 
  } else if (command == "5") { 
    analogWrite(LEDPIN, 255); // 100% brightness 
    Serial.println("LED Brightness set to 100%."); 
  } else if (command == "t") { 
    // User pressed 't', display current temperature 
    displayTemperature(); 
  } else {   
    Serial.println("Invalid command. Use '1' to '5' to adjust brightness, or press 't' to display 
temperature."); 
  } 
} 
 
void displayTemperature() { 
  float tempC = dht.readTemperature(); 
  float tempF = dht.readTemperature(true); 
   
  if (isnan(tempC) || isnan(tempF)) { 
    Serial.println("Failed to read temperature."); 
  } else { 
    Serial.print("Temperature: "); 
    Serial.print(tempC); 
    Serial.print("°C / "); 
    Serial.print(tempF); 
    Serial.println("°F"); 
  } 
} 
 
void adjustLEDBrightness() { 
  float tempC = dht.readTemperature(); 
   
  if (!isnan(tempC)) { 
    int brightness; 
    if (tempC <= 25) { 
      brightness = 255;  // 100% brightness 
    } else if (tempC >= 27) { 
      brightness = 64;   // 25% brightness 
  
    } else { 
      brightness = 127;  // 50% brightness 
    } 
    analogWrite(LEDPIN, brightness); 
    Serial.print("LED Brightness adjusted to: "); 
    Serial.print((brightness * 100) / 255); 
    Serial.println("%."); 
  } else { 
    Serial.println("Skipping LED adjustment (sensor error)."); 
  } 
} 
```

### Step 5: Test the Communication  
Open MiniCom and observe the output. 
