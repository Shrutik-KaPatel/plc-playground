# 01 — Motor Start/Stop

My first PLC program. The embedded equivalent of "Hello World" — except here, 
a motor turns on and stays on until you tell it to stop.

## What it does
Press START → motor runs. Release START → motor keeps running. Press STOP → motor stops.
Classic seal-in (latching) circuit on a Siemens S7-1200.

## Hardware (simulated)
- CPU: S7-1214C DC/DC/DC
- TIA Portal V18 + S7-PLCSIM V18
- No physical hardware

## Tags
| Tag | Address | Type |
|-----|---------|------|
| Start_button | %I0.0 | Input |
| Stop_button | %I0.1 | Input (NC) |
| Motor_Output | %Q0.0 | Output |

## What I learned
- Scan cycle = polling loop (same as `while(1)` in embedded C)
- Ladder logic rung = one `if` statement
- NC contact on Stop button = fail-safe by design (wire breaks → motor stops)
- Seal-in circuit = SR latch (Start=Set, Stop=Reset)

## Mistakes I made
- Added a Safety CPU (1214FC) instead of standard (1214C) — Safety PLCs block direct I/O forcing in simulation, wasted a lot of time debugging what looked like a logic error
- Project path was on OneDrive — caused TIA Portal to freeze during hardware catalog loading

## Simulation evidence
Screenshots in `/screenshots`:
- `Ladder_logic.png` — rung with live monitoring
- `run_mode.png` — PLCSIM showing RUN state
- `Values.png` — watch table with tag values