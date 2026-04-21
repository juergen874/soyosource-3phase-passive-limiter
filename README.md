# Soyosource 3-Phase Passive Limiter Mod

This repository contains a solution for adapting the single-phase **Soyosource Current Limiter Sensor** for use in a three-phase power system using an external passive filter circuit.

## Overview
Standard Soyosource limiters typically monitor only one phase. This modification uses a passive summing and filtering circuit to combine signals from multiple phases (e.g., L1 and L2) into a single input that the Soyosource sensor can interpret.

### Core Principle
The solution uses an **external passive filter** to sum AC current signals from different phases. Due to the phase shift (120°) and circuit characteristics, signals are attenuated differently. This is compensated for by adjusting the number of wire loops through the sensor.

## Results by "menergie" (ochsnerj)
Based on empirical measurements and simulations by user **menergie** from the Akkudoktor.net forum:

| Phase | Measured Attenuation | Sensor Calibration (Loops) | Resulting Contribution |
| :--- | :--- | :--- | :--- |
| **L1** | 1/2 (50%) | 1 Loop | 0.5 units |
| **L2** | 1/4 (25%) | 2 Loops | 0.5 units |

**Summary of Findings:**
- **Attenuation:** The actual circuit attenuates L1 to 1/2 and L2 to 1/4 of the original signal strength.
- **Compensation:** By looping the L1 wire **once** and the L2 wire **twice** through the Soyosource sensor, both phases contribute equally to the final reading.
- **Display Scaling:** The Soyosource display will show approximately **50% of the actual total power** value across the phases. This is a consistent linear scaling factor.

## Hardware Design
The design consists of:
1. **Passive Filter Circuit:** A network of resistors to sum the AC signals from current transformers.
2. **Current Transformers:** Standard transformers used to pick up the phase current.
3. **Stripboard Layout:** A compact implementation on a standard prototyping board.

### Included Files (Work in Progress)
*   `schematics/passiv_filter.jpg`: Circuit diagram for the filter.
*   `layout/streifenraster.jpg`: Stripboard assembly guide.
*   `docs/masszeichnung.jpg`: Dimensional drawings for mechanical integration.

## How to Use
1. Build the passive filter circuit on a stripboard according to the provided layout.
2. Connect current transformers to L1 and L2.
3. Pass the L1 output wire through the Soyosource sensor **once**.
4. Pass the L2 output wire through the Soyosource sensor **twice**.
5. Note that the power displayed on the Soyosource unit must be multiplied by 2 to get the real-world value.

## Credits
This project is based on the research and implementation by user **menergie** (ochsnerj) on the [Akkudoktor.net forum](https://akkudoktor.net/t/soyosource-current-limiter-sensor-auf-drei-phasen-umbauen-mit-externer-schaltung/18355/59).

---
*Disclaimer: This is an experimental modification involving AC signals. Handle with care and ensure proper insulation.*
