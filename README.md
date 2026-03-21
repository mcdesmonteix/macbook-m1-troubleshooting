# **🛠 Hardware Repair Portfolio**

## **📋 Case Study: MacBook Pro 14" (M1 Pro)**

**Summary:** Critical power failure following environmental exposure to volcanic magnetite (Mont Batur) and liquid ingress.

### **🔍 Technical Investigation**

| Diagnostic Step | Tool / Command | Observation |
| :---- | :---- | :---- |
| **Battery Health** | pmset \-g batt | 1%; not charging |
| **RTC Clock** | System Time | Reset to **April 1st, 2021** (00:00) |
| **Data Bus** | ioreg -rw0 -c AppleSmartBattery | Communication broken on the SMBus (Voltage=0, Cycle=0) |
|  |grep -i "Voltage\|CycleCount\|IsCharging" |  |

### **🛠️ Software-Side Recovery & Stabilization**

Prior to hardware intervention, the following commands were executed to stabilize the system and restore vital functions:

#### **1\. Resync of the clock for SSL access**

The RTC reset prevented any access to secure websites (HTTPS). Forced synchronization restored full connectivity:

`sudo sntp \-sS time.apple.com`

#### **2\. Stabilization of parasitic signals**

Since volcanic sand is ferromagnetic, it created electrical arcing within the MagSafe port, causing random reboots. This command disabled the automatic power-on to stabilize the logic board:

`sudo nvram AutoBoot=%00`

### **📉 Final Verdict & Recovery Plan**

Diagnostic confirms a **severed communication on the data bus (SMBus/I2C)** between the Battery Management System (BMS) and the Power Management Unit (PMU).

* \[ \] **Step 1:** Ultrasonic de-oxidation (Logic Board & MagSafe port).  
* \[ \] **Step 2:** Micro-soldering of the SMBus/I2C data traces.  
* \[ \] **Step 3:** Post-repair stress test (10 charging cycles).

*Documented by mcdesmonteix \- 2026*

