# Soyosource 3-Phase Passive Limiter Mod
## The Problem:
​Standard Soyosource limiters only measure a single phase. However, modern utility meters are balancing (saldierend) across all three phases. If your stove is running on Phase 2, but your inverter is only monitoring Phase 1, it won't ramp up production, and you'll end up paying for electricity despite having a full battery.
​Digital solutions (like ESP32/RS485 bridges) often suffer from control latency (1–5 seconds delay). This results in "wasted" energy or unwanted grid export during fast load changes.

## 🌟 The Solution: Analog Vector Summation
​
​This circuit uses the laws of AC physics to "straighten out" the 120^\circ phase shifts between L1, L2, and L3. By using a passive RC-network, we shift the phase of the secondary sensors so they align perfectly with the primary phase.
This repository contains a solution for adapting the single-phase **Soyosource Current Limiter Sensor** for use in a three-phase power system using an external passive filter circuit.
The result is a real-time physical summation of your entire household's current, fed directly into the inverter's original sensor port.

## 🌟 Key Advantages

Zero Latency: No processing time, no Wi-Fi drops, no lag. The inverter reacts at the speed of light to any load change.
Set and Forget: No firmware updates, no crashing, no API changes. It is purely hardware-based and autonomous.
Low Budget: Replaces expensive Smart Meter Gateways with a handful of resistors and capacitors.
Non-Invasive: No need to modify the inverter's internal communication or firmware. The original sensor input remains untouched.

## Overview
Standard Soyosource limiters typically monitor only one phase. This modification uses a passive summing and filtering circuit to combine signals from multiple phases (e.g., L1 and L2) into a single input that the Soyosource sensor can interpret.

### Core Principle
The solution uses an **external passive filter** to sum AC current signals from different phases. Due to the phase shift (120°) and circuit characteristics, signals are attenuated differently. This is compensated for by adjusting the number of wire loops through the sensor.

## Results 
Based on calculations and empirical measurements and simulations from the Akkudoktor.net forum:

| Phase | Measured Attenuation | Sensor Calibration (Loops) | Resulting Contribution |
| :--- | :--- | :--- | :--- |
| **L1** | 1 (100%) | 1 Loop | 1 units |
| **L2** | 1/2 (50%) | 2 Loops | 1 units |

**Summary of Findings:**
- **Attenuation:** The actual circuit attenuates L1 to 1 and L2 to 1/2 of the original signal strength.
- **Compensation:** By looping the L1 wire **once** and the L2 wire **twice** through the Soyosource sensor, both phases contribute equally to the final reading.


## Hardware Design
The design consists of:
1. **Passive Filter Circuit:** A network of resistors to sum the AC signals from current transformers.
2. **Current Transformers:** Standard transformers used to pick up the phase current.
3. **Stripboard Layout:** A compact implementation on a standard prototyping board.

### Included Files (Work in Progress)
*   `schematics/passiv_filter.jpg`: Circuit diagram for the filter.
*   `layout/streifenraster.jpg`: Stripboard assembly guide.
*   `docs/masszeichnung.jpg`: Dimensional drawings for mechanical integration.
*   `images/...`: several pictures

## How to Use
1. Build the passive filter circuit on a stripboard according to the provided layout.
2. Connect current transformers to L1 and L2.
3. Pass the L1 output wire through the Soyosource sensor **once**.
4. Pass the L2 output wire through the Soyosource sensor **twice**.


## Credits
This project is based on my research on the [Akkudoktor.net forum](https://akkudoktor.net/t/soyosource-current-limiter-sensor-auf-drei-phasen-umbauen-mit-externer-schaltung/18355/59).

---
*Disclaimer: This is an experimental modification involving AC signals. Handle with care and ensure proper insulation.*
