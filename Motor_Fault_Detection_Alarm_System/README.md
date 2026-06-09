# Motor Fault Detection & Alarm System

## Overview

This project implements an industrial-style Motor Fault Detection and Alarm System using Siemens TIA Portal and an S7-1200 PLC. The system simulates real-world machine protection logic commonly used in manufacturing environments such as automotive assembly lines, conveyor systems, and industrial automation cells.

The PLC continuously monitors fault conditions and automatically shuts down the motor when a fault is detected. The operator must acknowledge and reset the fault before the motor can be restarted.

---

## Features

* Motor Start/Stop Control
* Motor Latching Logic
* Fault Detection
* Fault Latching
* Automatic Motor Shutdown on Fault
* Alarm Light Indication
* Audible Alarm (Buzzer)
* Alarm Acknowledgement Function
* Manual Fault Reset
* Restart Interlock Protection

---

## System Operation

### Normal Operation

1. Operator presses the Start pushbutton.
2. Motor starts and remains latched ON.
3. Motor continues running until a Stop command or fault occurs.

### Fault Condition

1. Fault sensor becomes active.
2. Fault is latched in memory.
3. Motor stops immediately.
4. Alarm light turns ON.
5. Buzzer turns ON.

### Alarm Acknowledgement

1. Operator presses the Acknowledge button.
2. Buzzer turns OFF.
3. Alarm light remains ON to indicate an active fault.

### Fault Reset

1. Fault condition is cleared.
2. Operator presses the Reset button.
3. Fault latch is reset.
4. Alarm light turns OFF.
5. Motor can be restarted.

---

## PLC Tags

### Inputs

| Tag        | Description                  |
| ---------- | ---------------------------- |
| Start_PB   | Start Pushbutton             |
| Stop_PB    | Stop Pushbutton              |
| Temp_Fault | Fault Sensor                 |
| Ack_PB     | Alarm Acknowledge Pushbutton |
| Reset_PB   | Fault Reset Pushbutton       |

### Outputs

| Tag         | Description           |
| ----------- | --------------------- |
| Motor_Run   | Motor Output          |
| Alarm_Light | Fault Indicator Light |
| Buzzer      | Audible Alarm         |

### Internal Memory

| Tag         | Description                  |
| ----------- | ---------------------------- |
| Motor_Latch | Motor Run Latch              |
| Fault_Latch | Latched Fault Condition      |
| Alarm_Ack   | Alarm Acknowledgement Status |

---

## Control Logic

### Motor Control

* Start button sets the motor latch.
* Stop button resets the motor latch.
* Motor cannot start while a fault is active.

### Fault Handling

* Fault sensor sets a fault latch.
* Fault latch immediately stops the motor.
* Fault remains active until manually reset.

### Alarm System

* Alarm light remains ON while a fault exists.
* Buzzer sounds when a fault occurs.
* Acknowledge button silences the buzzer.
* Alarm light remains active until fault reset.

---

## Software Used

* Siemens TIA Portal V18
* Siemens S7-1200 PLC
* PLCSIM for simulation
* Ladder Logic (LAD)

---

## Applications

This project demonstrates concepts commonly used in:

* Industrial Automation
* Manufacturing Systems
* Automotive Body-in-White Production
* Conveyor Systems
* Machine Safety and Protection
* PLC-Based Alarm Management

---

## Future Improvements

* Multiple Fault Types (Overtemperature, Overload, Jam Detection)
* Fault Counter (CTU)
* Fault History Logging
* HMI Operator Interface
* Alarm History Screen
* Runtime Monitoring
* Maintenance Diagnostics

---

## Author

Shrutik Ka Patel

Master of Engineering Practice (Electrical)
Carleton University
