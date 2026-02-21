# How to Use the UART Interface for Output
The UART interface in the Greenhouse Monitoring System allows the user to interact with the system through a
terminal application like Minicom. The interface enables the user to toggle between Automatic Mode and Manual
Mode, view temperature data, and adjust the LED brightness.

## Steps to Use the UART Interface
### Install Minicom (or any serial terminal software):
Linux: Install Minicom using the following command:
```
sudo apt-get install minicom
```
Windows: You can use PuTTY or Tera Term as alternatives.
macOS: Use screen or CoolTerm.

### Connect the Arduino to your PC:
- Use a USB cable to connect the Arduino Nano to your computer.
- The Arduino will be recognized as a serial device on a COM port.

### Launch Minicom (or terminal software):
- Open a terminal window and type:
```
minicom -b 9600 -o -D /dev/ttyUSB0
```
Replace ```/dev/ttyUSB0``` with the correct port if needed. You can find the port name in your device manager or using ls ```/dev/tty*``` on Linux.

### Mode Selection:
Upon connecting to the Arduino via UART, the system will prompt the user to choose between Automatic or Manual Mode:
- Press 1 to select Automatic Mode.
- Press 2 to select Manual Mode.
Example prompt:
```
1: Automatic Mode
2: Manual Mode
```

### Automatic Mode:
The system will automatically display the temperature every 2 seconds (in Celsius and Fahrenheit).
The LED brightness will be adjusted based on the temperature:
- ≤25°C: 100% brightness
- 26°C: 50% brightness
- ≥27°C: 25% brightness.
To switch back to mode selection, press 0 to return to the mode prompt.

### Manual Mode:
In Manual Mode, the user can control the LED brightness using specific key presses:
- 1 → 0% brightness
- 2 → 25% brightness
- 3 → 50% brightness
- 4 → 75% brightness
- 5 → 100% brightness
- Press 't' to display the current temperature in both Celsius and Fahrenheit.
To switch to Automatic Mode, press 0.

---

## Example interactions:
### Automatic Mode Display:
```
Temperature: 24.5°C / 76.1°F
LED Brightness: 100%
```
Every 2 seconds, the temperature and LED brightness will update.
### Manual Mode Controls:
```
Enter 1 for 0%, 2 for 25%, 3 for 50%, 4 for 75%, 5 for 100%
```
User presses 2 → LED brightness is set to 25%.

### Temperature Request in Manual Mode:
```
t
Temperature: 26.3°C / 79.3°F
```
