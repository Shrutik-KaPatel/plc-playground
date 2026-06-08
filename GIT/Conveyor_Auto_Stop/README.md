Conveyor Auto-Stop (Timer-Based Logic)

## Description
A timed conveyor sequence simulated using Siemens TIA Portal V18 and S7-PLCSIM V18.
The conveyor starts after a configurable delay and stops automatically after a set run duration —
no manual stop required.

## Hardware
- CPU: S7-1214C DC/DC/DC (6ES7 214-1AE30-0XB0, V4.2)
- Simulated in S7-PLCSIM V18

## Tags
| Name | Address | Type | Description |
|------|---------|------|-------------|
| Start_Button | %I0.0 | Bool | Initiates the timed sequence |
| Conveyor_Motor | %Q0.0 | Bool | Conveyor belt output |

## Logic
- Rung 1: Start_Button → TON1 (PT=5s) — pre-start delay
- Rung 2: TON1.Q → TON2 (PT=7s) — run duration timer
- Rung 3: TON1.Q (NO) + TON2.Q (NC) → Conveyor_Motor

## Sequence
1. Operator presses Start
2. 5-second pre-start delay (TON1 counts)
3. Conveyor starts automatically
4. After 7 seconds of running, conveyor stops automatically (TON2 expires, NC contact opens)

## Key Concepts
- TON timer Q output used as inter-rung signal — no additional tags needed
- NC contact as automatic shutoff condition
- Fully automatic stop — no Stop button required

## Simulation Results
- Pre-start delay confirmed: motor ON at 5s
- Auto-stop confirmed: motor OFF at 12s
- Tested in PLCSIM RUN mode