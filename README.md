# differential-pressure-spirometer
Arduino-based spirometer leveraging a Venturi pneumotach and MPX2010DP differential pressure sensing, with analog front-end amplification and signal processing for real-time flow and volume analysis (FEV1, PEF).

# DIY Respiratory Spirometer

A DIY spirometer system built with an `MPX2010DP` differential pressure sensor, `INA163` instrumentation amplifier, Arduino Mega, 16x2 LCD, and Python-based data acquisition/visualization.

## Overview

This project measures respiratory pressure signals and estimates airflow and spirometry metrics such as:

- `FEV1` — Forced Expiratory Volume in the first 1 second
- `FVC` — Forced Vital Capacity

The system includes:

- `MPX2010DP` differential pressure sensor
- `INA163` preamplifier
- analog filtering stages
- Arduino Mega for sampling and user interface
- 16x2 LCD for countdown/results
- LED indicators for visual feedback
- Python for serial acquisition, plotting, baseline calibration, and metric calculation

## Features

- 4-second baseline calibration before each test
- LCD-guided countdown
- LED countdown and flash feedback
- live plotting of:
  - voltage
  - pressure
  - flow rate
- automatic breath detection
- calculation of `FEV1` and `FVC`
- result sent back to Arduino LCD

## Arduino Responsibilities

The Arduino code:

- performs baseline sampling
- displays instructions on the LCD
- controls the LED sequence
- records analog samples from `A0`
- streams samples to Python over serial
- waits for Python to return computed `FEV1` and `FVC`

## Python Responsibilities

The Python code:

- triggers the Arduino test
- receives baseline and breath data over serial
- converts ADC readings to voltage
- converts voltage to differential pressure
- estimates flow using the Venturi model
- detects the start and end of exhalation
- computes `FEV1` and `FVC`
- plots voltage, pressure, and flow
- sends final results back to the Arduino LCD

## Notes

- The flow calculation is based on the Venturi equation and depends on correct tube geometry and pressure tap placement.
- Accurate spirometry requires proper calibration against a known reference device.
- If the Venturi tube is not installed, pressure plots remain meaningful, but flow/FEV1/FVC values are only rough estimates.
