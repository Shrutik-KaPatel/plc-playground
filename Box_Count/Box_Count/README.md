# Conveyor Box Counter

## Description
A conveyor system that automatically stops after detecting a set number of boxes passing a proximity sensor. Built and simulated using Siemens TIA Portal V18 and S7-PLCSIM V18.

## Hardware
- CPU: S7-1214C DC/DC/DC (6ES7 214-1AE30-0XB0, V4.2)
- Simulated in S7-PLCSIM V18

## Tags
| Name | Address | Type | Description |
|------|---------|------|-------------|
| Start_Button | %M0.0 | Bool | Starts the conveyor |
| Stop_Button | %I0.1 | Bool | Manually stops the conveyor |
| Conveyor_Motor | %Q0.0 | Bool | Conveyor belt output |
| Proxi_Sensor | %M0.2 | Bool | Detects each box passing |
| Rising Edge Detection Bit | %M0.3 | Bool | Internal edge detection flag |
| Counter Done Bit | %M0.4 | Bool | Set when box count reaches PV |
| Current Value | %MW10 | Word | Live counter value |

## Logic
- Network 1: Start/Stop motor control with seal-in circuit. Counter Done Bit automatically stops the motor when box count is reached.
- Network 2: Counts boxes using P_TRIG (rising edge detection) and CTU counter (PV=5). Counter resets when Counter Done Bit is HIGH.

## Sequence
1. Operator presses Start — conveyor runs
2. Each box triggers Proxi_Sensor — P_TRIG detects rising edge, CTU increments
3. After 5 boxes — Counter Done Bit goes HIGH
4. Conveyor stops automatically — no manual stop required
5. Press Start to begin a new cycle

## Key Concepts
- Seal-in circuit: motor holds itself ON after Start is released
- P_TRIG: detects rising edge only — prevents double counting on long sensor signals
- M bits (internal flags): used for inter-network communication without physical I/O
- CTU counter resets automatically each new cycle via Counter Done Bit

## Simulation Results
- Box count increments correctly on each sensor trigger
- Motor stops automatically at count = 5
- Manual stop via Stop_Button confirmed
- Tested in PLCSIM RUN mode