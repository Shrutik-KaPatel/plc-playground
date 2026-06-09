# Traffic Light Sequence

## Description
An automated traffic light sequence simulated using Siemens TIA Portal V18 and S7-PLCSIM V18.
The system cycles through Green, Yellow, and Red phases automatically with configurable timing,
and repeats continuously until manually stopped.

## Hardware
- CPU: S7-1214C DC/DC/DC (6ES7 214-1AE30-0XB0, V4.2)
- Simulated in S7-PLCSIM V18

## Tags

**Inputs**
| Name | Address | Type | Description |
|------|---------|------|-------------|
| Start | %I0.0 | Bool | Starts the traffic light cycle |
| Reset | %I0.1 | Bool | Stops and resets the sequence |
| Traffic_Sensor | %I0.2 | Bool | Traffic presence sensor |

**Outputs**
| Name | Address | Type | Description |
|------|---------|------|-------------|
| Green_Led | %Q0.0 | Bool | Green light output |
| Red_Led | %Q0.1 | Bool | Red light output |
| Yellow_Led | %Q0.2 | Bool | Yellow light output |

**Memory**
| Name | Address | Type | Description |
|------|---------|------|-------------|
| Run_Mode | %M0.0 | Bool | System running flag |
| Repeat_Cycle | %M0.1 | Bool | Triggers next cycle |

## Logic
- Network 1: Start/Reset control with seal-in — sets Run_Mode
- Network 2: Run_Mode initializes Green ON, Yellow OFF, Red ON
- Network 3: Run_Mode + Green → TON (5s) → Yellow ON
- Network 4: Run_Mode + TON2 (10s) → Green ON
- Network 5: Run_Mode + TON3 (15s) → Repeat_Cycle — restarts sequence

## Sequence
1. Operator presses Start — Run_Mode activates
2. Green ON for 5 seconds
3. Yellow ON — transition phase
4. Red ON — stop phase
5. Cycle repeats automatically
6. Press Reset to stop at any time

## Key Concepts
- Seal-in circuit for stable Run_Mode control
- Chained TON timers for precise phase timing
- M bits as internal flags for inter-network communication
- Repeat_Cycle bit triggers automatic sequence restart

## Simulation Results
- Green → Yellow → Red sequence confirmed
- Automatic cycle repeat confirmed
- Manual reset confirmed
- Tested in PLCSIM RUN mode