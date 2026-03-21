# **🛠 Hardware Repair Portfolio**

## **📋 Case Study: MacBook Pro 14" (M1 Pro)**

**Summary:** Critical power failure following environmental exposure to volcanic magnetite (Mont Batur) and liquid ingress.

### **🔍 Technical Investigation**

| Diagnostic Step | Command | Goal | Result |
| :--- | :--- | :--- | :--- |
| **RTC Clock** | `sudo sntp -sS time.apple.com` | Fix 01/04/2021 RTC bug | **Success**: Restored SSL/Web access |
| **Battery Health** | `pmset -g batt` | Check battery status | `1% - Not charging` |
|  | `sudo pkill powerd` | Reset power daemon | No change (Hardware issue confirmed) |
|  | `sudo nvram AutoBoot=%00` | Disable auto-power on | **Success**: Stabilized ghost signals |
| **Data Bus** | `ioreg -rw0 -c AppleSmartBattery` | Query SMBus registers | **Critical**: Revealed  `Voltage=0,  Cycle=0` |

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

