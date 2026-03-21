# 🛠 Hardware Repair Journal

This repository archives my technical interventions, diagnostics, and hardware troubleshooting.

---

## 💻 MacBook Pro 14" (M1 Pro) - Critical Power Failure
**Model :** A2442 (2021) | **Symptom :** Battery 1% / RTC Reset | **Date :** March 2026

### 🔍 Historic & Diagnosis
- **Incidents :** Volcanic sand (magnetite) + liquid leakage.
- **RTC Bug :** Clock stuck on **01/04/2021** (VBACKUP voltage loss).
- **ioreg Analysis  :** `Voltage = 0V` | `CycleCount = 0`.
- **Evidence :** **SMBus/I2C** data bus break confirmed.

### 🛠 Troubleshooting Commands Used
- `pmset -g batt` : Charge status.
- `sudo sntp -sS time.apple.com` : Resync of the clock for SSL access.
- `sudo nvram AutoBoot=%00` : Stabilization of parasitic signals from the MagSafe.

### 📉 Status
Waiting for **micro-soldering** (Deoxidation / Repair of data tracks).

### Critical Findings:
\ `Voltage` = 0 (Communication line severed or shorted).
\ `CycleCount` = 0 (BMS chip silent).
\ `NotChargingReason` = 33620032 (Firmware-level safety inhibition).

## Hardware Stabilization
To prevent ghost power-on signals from volcanic sand residues (magnetite) in the MagSafe port:

Bash
sudo nvram AutoBoot=%00

## 📉 Technical Conclusion
The diagnostic points to a severed SMBus/I2C data line or a failed PMU/CD3217 charging controller.
Recommended Repair: 
1. Ultrasonic cleaning (de-oxidation).
2. Micro-soldering of data traces.
3. BMS/Battery replacement if internal circuitry is fried.

---
