# **🛠 Hardware Repair Portfolio**

## **📋 Case Study: MacBook Pro 14" (M1 Pro)**

**Summary:** Critical power failure following environmental exposure to volcanic magnetite (Batur) and liquid ingress.

### **🔍 Technical Investigation**

| Diagnostic Step | Tool / Command | Observation |
| :---- | :---- | :---- |
| **Battery Health** | pmset \-g batt | 1%; not charging |
| **RTC Clock** | System Time | Reset to **April 1st, 2021** (00:00) |
| **Data Bus** | ioreg | Voltage: 0V / CycleCount: 0 |

### **🛠️ Software-Side Recovery & Stabilization**

Prior to hardware intervention, the following commands were executed to stabilize the system and restore vital functions:

#### **1\. Resync of the clock for SSL access**

The RTC reset prevented any access to secure websites (HTTPS). Forced synchronization restored full connectivity:

sudo sntp \-sS time.apple.com

#### **2\. Stabilization of parasitic signals**

Since volcanic sand is ferromagnetic, it created electrical arcing within the MagSafe port, causing random reboots. This command disabled the automatic power-on to stabilize the logic board:

\- sudo nvram AutoBoot=%00

### **📉 Final Verdict & Recovery Plan**

Diagnostic confirms a **severed communication on the data bus (SMBus/I2C)** between the Battery Management System (BMS) and the Power Management Unit (PMU).

* \[ \] **Step 1:** Ultrasonic de-oxidation (Logic Board & MagSafe port).  
* \[ \] **Step 2:** Micro-soldering of the SMBus/I2C data traces.  
* \[ \] **Step 3:** Post-repair stress test (10 charging cycles).

*Documented by mcdesmonteix \- 2026*

* **Le contenu :** Ton texte ou tes commandes.
* **La fermeture :** Toujours trois ` ``` ` seuls sur une ligne. **Si tu oublies de fermer, tout le reste de ton document sera gris !**



### 📌 Prochaine étape
Maintenant que ton `README.md` est magnifique et que tu sais créer des blocs de code, **souhaites-tu que je t'apprenne à ajouter des images ou des captures d'écran directement dans ton rapport GitHub pour le rendre encore plus visuel ?**