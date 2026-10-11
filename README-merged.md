# ESP32 IoT Monitor — DHT22 + OLED

A beginner embedded project built in the [Wokwi](https://wokwi.com) simulator.
An ESP32 reads temperature and humidity from a DHT22 sensor and displays the readings in real time on a 128×64 SSD1306 OLED screen, while also printing them to the Serial Monitor.

![Simulation](simulation.png)

## Overview
- **Microcontroller:** ESP32
- **Display:** SSD1306 0.96" OLED, 128×64, I2C address `0x3C`
- **Sensor:** DHT22 digital temperature & humidity sensor
- **Simulation:** Wokwi (no hardware needed to run)

## Features
- Real-time temperature (°C) and humidity (%) readings
- Live OLED display using Adafruit GFX / SSD1306 libraries
- Serial Monitor output at 115200 bps for debugging (`Temp: 24.00`)
- 1-second refresh interval

## Wiring / Pinout

| Peripheral | Pin | ESP32 Pin | Protocol | Description |
|---|---|---|---|---|
| SSD1306 | VCC | 3V3 | Power | 3.3V supply |
| SSD1306 | GND | GND | Ground | Common ground |
| SSD1306 | SCL | GPIO 22 | I2C Clock | I2C clock line |
| SSD1306 | SDA | GPIO 21 | I2C Data | I2C data line |
| DHT22 | VCC | 3V3 | Power | 3.3V supply |
| DHT22 | DATA | GPIO 15 | 1-Wire Digital | Sensor data |
| DHT22 | GND | GND | Ground | Common ground |

## Project Structure
```
├── sketch.ino       # Main C++ firmware (setup & loop)
├── diagram.json     # Wokwi hardware schematic & wiring
├── libraries.txt    # Library dependencies for Wokwi
├── simulation.png   # Screenshot of running simulation
└── README.md        # Documentation
```

## How to Run

**Method 1: Web Simulation (no hardware)**
1. Import `sketch.ino` and `diagram.json` into Wokwi
2. Add the libraries from `libraries.txt` via Library Manager
3. Click Start Simulation
4. Click the DHT22 module to adjust temperature/humidity sliders and watch the display update

**Method 2: Physical Hardware**
1. Open the project in Arduino IDE
2. Install: Adafruit SSD1306, Adafruit GFX Library, DHT sensor library
3. Wire the modules using the pinout table above
4. Select ESP32 Dev Module, choose your COM port, and upload

## How It Works
- `setup()` runs once at startup: starts Serial (115200), initializes the DHT sensor, and initializes the OLED. If the OLED fails to initialize, the program halts.
- `loop()` repeats forever: reads temperature/humidity, prints temperature to Serial, clears and redraws the OLED, waits 1000 ms.

## What I Learned
- Difference between `setup()` (run once, initialization) and `loop()` (runs repeatedly)
- Why a sensor's DATA pin must connect to a GPIO (it sends digital pulses encoding the readings), not to power/ground
- I2C addressing: `0x3C` is the OLED's address on the I2C bus, like a house number that lets the ESP32 talk to the right device

## Future Improvements
- [ ] Add LED alarm when temperature exceeds 30°C
- [ ] Show warning message on OLED when threshold is exceeded
- [ ] Add °F display toggle
