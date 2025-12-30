## Day 16 — Windows Registry Forensics (DFIR)

### Scenario Overview

TBFC’s critical dispatch server showed abnormal behavior. A forensic investigation was launched to determine how the system was compromised by analyzing **registry artefacts**, while other teams handled logs, memory, and filesystem analysis.

### 🧠 Key Concepts Learned

* The **Windows Registry** stores system and user configuration data
* Registry data is stored in **hives** (SYSTEM, SOFTWARE, SAM, NTUSER.DAT, etc.)
* Registry hives must be analyzed **offline** to avoid evidence tampering
* **Registry Explorer** allows safe forensic analysis of collected hives
* Registry keys can reveal:

  * Installed applications
  * User activity
  * Startup persistence
  * System identity

### Tools Used

* **Registry Explorer**
* Offline Registry Hives (SYSTEM, SOFTWARE, NTUSER.DAT, etc.)

### 🔎 Investigation Highlights

| Investigation Goal     | Registry Location                                        |
| ---------------------- | -------------------------------------------------------- |
| Computer name          | HKLM\SYSTEM\ControlSet001\Control\ComputerName           |
| Installed applications | HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall |
| User-launched programs | NTUSER.DAT                                               |
| Startup persistence    | HKLM\Software\Microsoft\Windows\CurrentVersion\Run       |

### Outcome

* **Malicious application installed**: DroneManager Updater
* **Execution path**:
  `C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe`
* **Persistence mechanism added**:
  `"C:\Program Files\DroneManager\dronehelper.exe" --background`
* Confirms attacker established **startup persistence**
* Abnormal activity began on **21st October 2025**

### Key Takeaways

Registry artefacts are critical in **Digital Forensics & Incident Response (DFIR)**. Even when files are deleted, the registry often preserves evidence of attacker actions, making it invaluable for timeline reconstruction and persistence detection.

