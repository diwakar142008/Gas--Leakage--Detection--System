# Smart Gas Leakage Detection and Alert System

## Team Name
TechElites

## Team Members
- P. Diwakar
- S. Harish
- G. Balasubramanian
- M. Santosh

## Project Overview
This project is a Smart Gas Leakage Detection System using ESP32.

The system detects LPG, Methane, and Butane gases using the MQ-2 sensor.
It monitors temperature and humidity using DHT11 sensor.

If gas concentration exceeds the threshold:
- LED turns ON
- Buzzer activates
- LCD displays status (Safe / Moderate / Danger)
- Mobile alert is triggered

## Gas Level Classification
- SAFE: < 350
- MODERATE: 350–600
- DANGER: > 600

## Hardware Components
- ESP32
- MQ-2 Gas Sensor
- DHT11 Sensor
- 16x2 LCD (I2C)
- Buzzer
- LED

## Applications
- Homes
- Industries
- Laboratories
- Kitchens

## Future Improvements
- Automatic gas valve shutoff
- Cloud-based monitoring
- Mobile application integration
