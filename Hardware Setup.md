# Hardware Setup
The Greenhouse Monitoring System uses the following hardware components:
-	Arduino Nano: Serves as the microcontroller, processing temperature data and controlling the LED brightness.
-	DHT11 Temperature Sensor: Measures the internal temperature of the greenhouse.
-	LED: Represents temperature-based brightness control to simulate environmental adjustments.
-	Resistor (220Ω or 330Ω): Limits current to protect the LED.
-	UART Interface (via USB): Facilitates communication between the Arduino and a terminal (e.g., Minicom) for user interaction.

### Connections Overview:
 
![Circuit Diagram](https://github.com/user-attachments/assets/7bd81d3e-0806-4e80-a82f-48e1441811cd)

•	The DHT11 is connected to pin D2 for data transmission.
•	The LED is connected to pin D9 (PWM) for brightness control.
•	The Arduino Nano communicates with the computer via a USB cable for power and UART interaction.
This setup provides a simple yet effective framework for temperature monitoring and control.
