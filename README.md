# ESP32 Anti-Tamper Smart Parcel System

## Overview

The Anti-Tamper Smart Parcel System is an ESP32-based embedded security prototype designed to detect unauthorized access and physical/environmental tampering during parcel transit and storage.

The system uses multiple sensing modalities to detect:

- Physical shock and drops
- Unauthorized parcel opening
- Abnormal temperature conditions

The system provides real-time local alerts and serial event logging.

## System Architecture

The system consists of three sensing modules connected to an ESP32:

- MPU6050 - motion and shock detection
- LDR - parcel opening detection
- DHT11 - temperature monitoring
- Buzzer / LED - local tamper alerts
- OLED - system status display
- Serial Monitor - real-time event logging

## Hardware

| Component | Interface / Pin |
|---|---|
| ESP32 | Main controller |
| MPU6050 | I2C - GPIO 21 (SDA), GPIO 22 (SCL) |
| LDR | Analog GPIO 34 |
| DHT11 | Digital GPIO 4 |
| Buzzer / LED | GPIO output |
| OLED | Display output |

## Detection Logic

### MPU6050 - Motion / Shock

| Delta-g | Classification |
|---|---|
| < 0.3 g | Stable |
| 0.3 - 1.5 g | Motion |
| > 1.5 g | Shock / Drop |

### LDR - Parcel Opening

| ADC Value | Classification |
|---|---|
| < 500 | Dark / Closed |
| 500 - 800 | Ambient Light |
| > 800 | Box Opened |

### DHT11 - Temperature

| Temperature | Classification |
|---|---|
| < 20°C | Cold |
| 20 - 35°C | Normal |
| 35 - 50°C | Warm |
| > 50°C | Heat Tamper |

## Tamper States

The system classifies the parcel into four main states:

- SECURE
- SHOCK / DROP
- BOX OPENED
- HEAT TAMPER

A hierarchical decision logic evaluates sensor readings and triggers the appropriate local alert.

## Firmware

The firmware was developed using the Arduino IDE and ESP32 board support package.

The main software modules include:

- `setup()` - initializes sensors, GPIO and communication
- `loop()` - continuously reads sensors and evaluates tamper conditions
- `readAccelerometer()` - processes MPU6050 readings
- `readLDR()` - samples the LDR ADC
- `readTemperature()` - reads temperature
- `evaluateTamper()` - determines the tamper state
- `triggerAlert()` - controls buzzer / LED alerts
- `serialLog()` - logs sensor readings and events

## Testing

The prototype was tested under multiple conditions including:

- Normal resting state
- 30 cm drop
- Parcel lid opening
- Heat exposure
- Simultaneous tamper conditions
- Vehicle/train vibration simulation

The system successfully detected the tested tamper conditions and produced the corresponding alerts.

## Results

- MPU6050 shock detection responded within approximately 10 ms during testing.
- LDR opening detection operated within one 200 ms polling cycle.
- DHT11 temperature monitoring has an inherent approximately 2-second sampling interval.
- The prototype successfully classified the tested tamper conditions.

## Limitations

The current prototype:

- Uses local buzzer/LED and serial alerts
- Does not implement wireless alerting
- Requires manual LDR threshold calibration
- Does not include persistent data logging
- Has not been fully optimized for battery operation

## Future Work

Possible extensions include:

- Wi-Fi / MQTT cloud monitoring
- GPS-based tracking
- Persistent event logging
- Self-calibrating thresholds
- Cryptographic tamper-evidence logging
- Mobile application integration

## Applications

Potential applications include:

- E-commerce parcel delivery
- Pharmaceutical logistics
- Sensitive document transport
- Laboratory sample security

## Technologies

- ESP32
- Embedded C / C++
- Arduino IDE
- MPU6050
- I2C
- ADC
- DHT11
- LDR
- OLED
- GPIO
- Serial communication

## Authors

**Dona Maxin**  
Electronics and Communication Engineering

**Sudarsan P J**
