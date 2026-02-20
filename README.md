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
- 220Ω Resistor
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

```bash
sudo apt-get install minicom

### Run Minicom:
minicom -b 9600 -o -D /dev/ttyUSB0
