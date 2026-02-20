# 🌱 Greenhouse Monitoring System  
## Monitor the Temperature of the Greenhouse using Arduino Nano, DHT11 & UART Interface

---

## 📌 Project Overview

The **Greenhouse Monitoring System** is an embedded systems project designed to monitor greenhouse temperature and control LED brightness accordingly.

The system operates in two modes:

- 🔄 **Automatic Mode** – LED brightness adjusts automatically based on temperature.
- 🎛 **Manual Mode** – User controls LED brightness via UART (Minicom).

This project demonstrates:
- Sensor interfacing
- PWM control
- Serial (UART) communication
- Embedded system design for agricultural automation

---

## 🎯 Features

- ✅ Real-time temperature monitoring
- ✅ Temperature display in Celsius & Fahrenheit
- ✅ Automatic LED brightness control
- ✅ Manual brightness control via UART
- ✅ Mode switching (Automatic / Manual)
- ✅ Stable serial communication (9600 baud)

---

## 🧰 Hardware Components

- Arduino Nano
- DHT11 Temperature Sensor
- LED
- 220Ω Resistor (if requiered) 
- USB Cable
- Breadboard
- Jumper Wires

---

## 🔌 Circuit Connections
### 📍 DHT11 Sensor

| DHT11 Pin | Arduino Nano |
|------------|--------------|
| VCC        | 5V           |
| GND        | GND          |
| DATA       | D2           |

### 📍 LED

| LED Pin | Arduino Nano |
|----------|--------------|
| Anode (+) | D9 (PWM)    |
| Cathode (-) | 220Ω Resistor → GND |

### 📍 UART Communication

- USB cable from Arduino Nano to PC
- Baud Rate: **9600**

---

## 💻 Software Requirements
- Arduino IDE
- DHT11 Library
- Minicom (Linux) / PuTTY (Windows)

### Install Minicom (Linux)
```
sudo apt-get install minicom
```
### Run Minicom:
```
minicom -b 9600 -o -D /dev/ttyUSB0
```

---

## 🚀 Uploading the Code
- Open Arduino IDE
- Select Tools → Board → Arduino Nano
- Select correct Port
- Click Upload
- Wait for successful compilation

---

## System Operation
### Mode Selection Menu
When connected via UART:
```
1: Automatic
2: Manual
```
### Automatic Mode
- Temperature displayed every 2 seconds
- Displayed in Celsius and Fahrenheit
- LED brightness automatically adjusts:
  
| Temperature Range | LED Brightness |
| ----------------- | -------------- |
| ≤ 25°C            | 100%           |
| 25°C < T < 27°C   | 50%            |
| ≥ 27°C            | 25%            |

Press 0 to return to mode selection.

### Manual Mode
Brightness Options:

| Key Press | Brightness |
| --------- | ---------- |
| 1         | 0%         |
| 2         | 25%        |
| 3         | 50%        |
| 4         | 75%        |
| 5         | 100%       |

Additional Commands:
- Press t → Display current temperature
- Press 0 → Return to mode selection

---

## 📊 Sample Output
### Automatic Mode
```
Temperature: 24.8°C / 76.6°F
LED Brightness: 100%
```
### Manual Mode
Manual Mode
```
Enter 1-5 to control brightness
Press t to display temperature
```
If t is pressed:
```
Temperature: 26.4°C / 79.5°F
```

---

## 🧠 Working Principle
- DHT11 reads temperature.
- Arduino processes sensor data.
- PWM signal is generated on Pin D9.
- LED brightness changes based on:
  - Temperature (Automatic Mode)
  - User input (Manual Mode)
- UART enables real-time interaction.

---

## 📈 Results
- Accurate temperature readings observed
- LED brightness correctly adjusts to:
  - 100%
  - 50%
  - 25%
- UART interface works smoothly
- Stable switching between modes

---

## 🔮 Future Improvements
- Add humidity monitoring
- Replace LED with cooling/heating system
- Add LCD display
- IoT cloud integration
- Data logging using SD card
- Mobile app control

---

## 📚 Educational Value
This project demonstrates:
- Embedded C++
- Sensor Interfacing
- PWM Control
- Serial Communication
- Agricultural Automation Concepts

---

## 👨‍💻 Author
Koushik Reddy
- Greenhouse Monitoring System Project
- Embedded Systems & IoT Enthusiast 🌱
