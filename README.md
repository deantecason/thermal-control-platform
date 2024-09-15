# Embedded Thermal Control Platform for Heat Pump and Refrigeration Systems

<b>Embedded firmware and control platform designed for precise, reliable operation of heat pump and refrigeration systems in real-world deployments.</b>
<br><br>

## System Overview
This controller is designed for:
- Heat pump automation and control
- Retrofit or replacement of legacy controllers
- Development and validation of advanced thermal control strategies

The system supports multi-sensor feedback, actuator control, and constraint-based operation for safe and efficient thermal management.
<br><br>

<img src="./m_controller_and_display.jpg" width="800"><br><br>

## Hardware Capabilities
- 12V DC power input
- 230V relay-controlled outputs
- 4 × 16A relays:
  - Compressor
  - Hot circulation pump / fan
  - Cold circulation pump / fan
  - Crankcase heater
- Pressure safety inputs (hot / cold side)
- Up to 12 temperature sensors (-55°C to +125°C)
- Electronic Expansion Valve (EEV) control (6-pin interface)
- Built-in protections:
  - Overheat / freeze protection
  - Power fault handling
  - Compressor safety logic
  - Liquid return protection
- Serial interface (UART)
- LED-based diagnostics
<br><br>

## Supported System Configurations
- Heat pump systems with EEV
- Systems with capillary tube or TXV
- EEV-only control mode
<br><br>

## Installation Environment
- Indoor systems with stable ambient conditions
- Outdoor systems operating under harsh environments
<br><br>

## Firmware Deployment
Firmware is deployed via UART interface using standard embedded workflow.

- Connect USB → UART converter
- Upload firmware to MCU
- Configure board (ATmega328p-based platform)
- Verify startup via LED and serial output

Required libraries:
- SoftwareSerial
- OneWire
- DallasTemperature
<br><br>

<img src="./m_add_IDE.png" height="300"><br><br>

## Hardware Validation (Self-Test)
Built-in self-test routines allow validation of:
- Relays
- Indicators
- EEV operation
- Temperature sensors

Enable test modes in firmware:
```c
//#define SELFTEST_RELAYS_LEDS_SPEAKER
//#define SELFTEST_EEV
//#define SELFTEST_T_SENSORS
````

<img src="./m_c_selftest_EEV.jpg" width="500"><br> <img src="./m_c_selftest_t_sensors.jpg" width="500"><br> <img src="./m_c_selftest_t_readings.png"><br><br>

## System Configuration

Setpoint control modes:

```c
#define SETPOINT_THI
//#define SETPOINT_TS1
```

* THI: loop-based temperature control (e.g., floor heating)
* TS1: tank-based control (e.g., storage systems) <br><br>

## Electrical Integration

### Power Wiring

<img src="./m_c_wiring_power.jpg" width="600"><br>

### 12V Supply

<img src="./m_c_wiring_12v.jpg" width="600"><br>

### Current Sensing

<img src="./m_c_wiring_current_sensor.jpg" width="600"><br>

### Communication / Interface

<img src="./m_c_wiring_display.jpg" width="600"><br>

### EEV Connection

<img src="./m_c_wiring_EEV.jpg" width="600"><br>

### Temperature Sensors

<img src="./m_c_wiring_t_sensors.jpg" width="600"><br>

### Pressure Sensors

<img src="./m_c_wiring_pressure.jpg" width="600"><br> <img src="./m_c_wiring_pressure_dummy.jpg" width="600"><br><br>

**⚠ High voltage present. System integration must be performed by qualified personnel.** <br><br>

## Runtime Interface

### Serial Console

Provides:

* Real-time telemetry
* System diagnostics
* Control commands
* State monitoring

<img src="./m_console_help.png"><br> <img src="./m_console_stats.png"><br><br>

## System Behavior

### Startup & Operation

* Controlled compressor sequencing
* Pump pre-conditioning
* Thermal stabilization before load
* Constraint-based shutdown conditions

### Refrigerant Charging (Commissioning)

* Incremental charging recommended
* Monitor suction and discharge conditions
* Expect protective stops during early tuning

<img src="./m_add_charge.jpg" height="200"><br><br>

## Control Approach

The system uses a hybrid control strategy combining:

* Feedforward (based on flow and thermal input)
* Feedback (temperature correction)
* Constraint-based protection logic

This enables:

* Stable operation under varying load
* Fast response without overshoot
* Safe handling of thermal inertia and delays <br><br>

## Sensor Implementation

* Use DS18B20 sensors with proper thermal coupling
* Apply insulation to minimize ambient influence
* Ensure accurate mounting for evaporator sensors

<img src="./m_ds18b20_epoxy.jpg" width="500"><br> <img src="./m_ds18b20_wires_protection.jpg" width="500"><br> <img src="./m_ds18b20_evaporator_mount.jpg" height="700"><br><br>

## Heat Exchanger Design Considerations

### Plate Heat Exchanger

* High efficiency
* Higher cost
* Requires proper oil return design

<img src="./m_plate_heat_exchangers.jpg" width="500"><br> <img src="./m_plate_echangers_oxygen_brazing.jpg" width="500"><br><br>

### Tube-in-Tube

* Lower cost
* Easier implementation
* Reduced efficiency

<img src="./m_tube-in-tube_diy1.jpg" width="400">
<img src="./m_tube-in-tube_diy2.jpg" width="400"><br><br>

## System Model Overview

<img src="./m_Deante_Heat_Pump_Controller_model.jpg" width="1000"><br><br>