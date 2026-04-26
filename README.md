# Soyosource 3-Phase Passive Limiter Mod (Analog Vector Summation)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/juergen874/soyosource-3phase-passive-limiter.svg)](https://github.com/juergen874/soyosource-3phase-passive-limiter/stargazers)
[![Forum: Akkudoktor](https://img.shields.io/badge/Forum-Akkudoktor.net-blue)](https://akkudoktor.net/t/soyosource-current-limiter-sensor-auf-drei-phasen-umbauen-mit-externer-schaltung/18355/)

**English | [Deutsch](#de-nulleinspeisung-auf-3-phasen-mit-soyosource)**

A hardware-based solution for real-time 3-phase balancing (saldierend) with Soyosource GTIL inverters. This analog circuit solves the "single-phase limitation" without the latency of digital ESP32/RS485 solutions.

---

## 🌟 The Problem
Standard Soyosource limiters only measure a **single phase**. However, utility meters balance across all three phases (L1+L2+L3).
*   **The Issue:** If your inverter is on L1, but your stove is on L2, the inverter won't increase power. You pay for electricity while your battery stays full.
*   **Digital Lag:** ESP32/RS485 bridges often have a 1–5 second delay, leading to grid export or unnecessary import during fast load changes.

## 🚀 The Solution: Analog Vector Summation
This circuit uses an **analog RC-network** to "straighten out" the 120° phase shifts between L1, L2, and L3. 
*   **Real-Time:** No processing time. The inverter reacts at the speed of light.
*   **Passive:** No firmware, no Wi-Fi, no crashes. It is purely autonomous hardware.
*   **Accurate:** By using specific wire loops (1 Loop for L1, 2 Loops for L2), we compensate for physical attenuation to achieve a perfect 1:1 summation.

### Results & Calibration
| Phase | Signal Attenuation | Sensor Calibration | Effective Contribution |
| :--- | :--- | :--- | :--- |
| **L1** | 1 (100%) | **1 Loop** | 100% |
| **L2** | 0.5 (50%) | **2 Loops** | 100% |

---

## <a name="de-nulleinspeisung-auf-3-phasen-mit-soyosource"></a>🇩🇪 Nulleinspeisung auf 3 Phasen mit Soyosource
Eine rein hardwarebasierte Lösung für die 3-Phasen-Summierung bei Soyosource-Wechselrichtern.

### Warum dieses Mod?
*   **Saldierende Zähler:** Moderne Stromzähler verrechnen alle drei Phasen. Ein Standard-Soyosource sieht aber nur eine Phase. Dieses Projekt ermöglicht die echte Nulleinspeisung über alle Phasen hinweg.
*   **Keine Latenz:** Im Gegensatz zu Tasmota, ESP32 oder Shelly-Lösungen gibt es keine Verzögerung durch WLAN oder Protokolle. Die Regelung erfolgt physikalisch in Echtzeit.
*   **Kostengünstig:** Ersetzt teure Smart-Meter-Gateways durch einfache Widerstände und Kondensatoren.

### Hardware-Aufbau
1.  **Passiver Filter:** Ein Netzwerk aus Widerständen summiert die AC-Signale der Stromwandler (CTs).
2.  **Kompensation:** Da die Schaltung das Signal von L2 dämpft, wird dies einfach durch **zwei Windungen** am Sensor ausgeglichen (L1 = 1 Windung, L2 = 2 Windungen).

---

## 🛠️ Hardware Design (WIP)
*   `schematics/`: Circuit diagrams for the passive filter.
*   `layout/`: Stripboard (Streifenraster) assembly guide.
*   `images/`: Build photos and measurement results.

## 🔗 Links & Resources
*   **Discussion & Background:** [Akkudoktor.net Forum Thread](https://akkudoktor.net/t/soyosource-current-limiter-sensor-auf-drei-phasen-umbauen-mit-externer-schaltung/18355/)
*   **Keywords:** Soyosource Limiter, 3-Phase Sensor, Zero Export, Nulleinspeisung, Balkonkraftwerk, Photovoltaik, Analog Summing, Current Transformer, Phase Shift Compensation.

---
*Disclaimer: This is an experimental modification involving AC signals. Always work with caution and ensure proper insulation.*
