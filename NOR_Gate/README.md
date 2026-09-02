# Two-Input NOR Gate — Cadence Virtuoso Implementation
 
## Overview
This project presents the design and simulation of a two-input NOR gate implemented at the transistor level using Cadence Virtuoso, based on standard static CMOS logic design principles. The implementation includes the schematic design, a reusable schematic symbol, a test bench for verification, and transient simulation of the circuit.
 
## Circuit Design
 
### Schematic
The NOR gate schematic was built using four MOSFETs from the GPDK (Generic Process Design Kit) technology library:
 
- **Pull-up network:** Two PMOS transistors (PM0, PM1) connected in series between VDD and the output node
- **Pull-down network:** Two NMOS transistors (NM0, NM1) connected in parallel between the output node and ground
| Transistor | Type | Width (W) | Length (L) | Multiplier (m) |
|---|---|---|---|---|
| PM0, PM1 | PMOS (gpdk090_pmos1v) | 120n | 100n | 1 |
| NM0, NM1 | NMOS (gpdk090_nmos1v) | 120n | 100n | 1 |
 
Inputs Va and Vb drive the gate terminals of the corresponding PMOS-NMOS pairs, and the output Vout is taken from the common node between the pull-up and pull-down networks.
 
### Symbol
A schematic symbol was created for the NOR gate to make it reusable as a portable component in larger designs, following standard convention:
- Va, Vb — inputs (left)
- Vout — output (right, with inversion bubble)
- VDD — top
- GND — bottom
### Test Bench
A test bench was constructed by instantiating the NOR gate symbol and applying:
- Two pulse voltage sources to Va and Vb (v1 = 0, v2 = 1, rise time = 50p, with differing pulse widths/periods to exercise different input combinations)
- A DC voltage source (vdc = 1) to VDD
- Ground connections as required
## Simulation
- **Analysis type:** Transient (tran)
- **Duration:** 100 ns
- **Environment:** ADE-L / ADE-XL
- **Result:** Simulation completed with 0 errors, 0 warnings
### Expected Truth Table
 
| Va | Vb | Vout |
|----|----|----|
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |
 
### Observations
Due to certain technical constraints while accessing Cadence remotely, the complete output waveform could not be observed during the initial simulation. The toggling behavior of input Vb was later verified on the VIVA waveform viewer, confirming correct input stimulus application. The output waveform Vout could not be conclusively verified against the expected truth table within the scope of this attempt.
 
## Files
- nor.zip — Cadence project files (schematic, symbol, test bench)
## Tools Used
- Cadence Virtuoso (Schematic Composer)
- ADE-L / ADE-XL
- GPDK Technology Library
 
