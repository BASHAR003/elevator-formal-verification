# Elevator Formal Verification

Formal verification of an elevator controller using SystemVerilog assertions and assumptions, developed as part of the **Formal Verification** course (Winter 2026) at the **Technion – Israel Institute of Technology**.

## Project Overview

This project models an elevator system with **5 floors** and verifies its correctness using formal property checking. The design is verified using assumption-based techniques and SVA (SystemVerilog Assertions).

## Files

| File | Description |
|------|-------------|
| `elevator_pkg.sv` | Package defining enums: `Direction` (UP/DOWN), `DoorsOp` (OPEN/CLOSE), `EngineOp` (GO/STOP) |
| `elevator.sv` | RTL design of the elevator controller — handles door timing, engine control, floor lights, and direction logic |
| `properties.sv` | SVA properties file — contains assumptions, assertions, and cover properties bound to the elevator module |
| `setup.tcl` | TCL setup script for the formal verification tool |

## Verified Properties

### Assumptions
- **Assume 1–2**: The elevator moves up/down by one floor when the engine is running in the corresponding direction.
- **Q1a**: The elevator stays on the same floor when the engine is stopped.
- **Q1b**: The elevator starts on exactly one floor (one-hot encoding).

### Assertions
- **Q2**: The elevator never goes below the ground floor (basement safety).
- **Q3**: The elevator never goes above the top floor (roof safety).
- **Q4**: Doors are never open while the elevator is moving (door safety).
- **Q5**: A request to floor 0 is eventually served (liveness).

### Cover Properties
- **Q6**: Floor light for floor 0 can remain active for 40 consecutive cycles.
- **Q7**: The elevator can travel from floor 0 to the top floor, stopping at each floor going up.
- **Q8**: The elevator can travel from the top floor to floor 0, stopping at each floor going down.
- **Q9**: The elevator can complete 10 full round trips (up then down).

## How to Run

Use a formal verification tool (e.g., Cadence JasperGold) with the provided TCL setup script:

```tcl
source setup.tcl
```

## Tools & Technologies

- **Language**: SystemVerilog (IEEE 1800-2009)
- **Verification**: SystemVerilog Assertions (SVA)
- **Formal Tool**: Cadence Jasper
