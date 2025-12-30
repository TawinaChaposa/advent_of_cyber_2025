# Day 19 — ICS / SCADA Incident Response (Modbus & PLCs)

## Scenario Overview

A critical failure disrupted TBFC’s drone delivery operations in Wareville. Although system dashboards showed normal operations, drones were delivering incorrect items. Investigation revealed a deliberate attack by King Malhare, who manipulated the **industrial control system (ICS)** governing drone logistics.

The attack targeted the **SCADA-controlled PLC**, altering Modbus registers and coils to sabotage Christmas deliveries while hiding the changes behind falsified system states and a built-in trap mechanism.

---

## My Role

I acted as an **ICS / OT Incident Responder**, responsible for investigating a compromised industrial control environment, identifying malicious logic manipulation, and safely restoring operations without triggering destructive fail-safes.

---

## Tools & Technologies

* Nmap
* Modbus TCP (Port 502)
* PLCs & SCADA concepts
* Python
* `pymodbus` library
* CCTV monitoring interface

---

## Investigation Approach

I began with **network reconnaissance** to identify exposed services and confirmed that the PLC was accessible over **Modbus TCP without authentication**. Using live CCTV feeds, I validated that the physical process was functioning—but producing incorrect outcomes, indicating a **logic manipulation attack** rather than system failure.

Next, I directly interrogated the PLC by reading **holding registers** and **coils** via Modbus. This revealed attacker-modified values controlling package selection, disabled inventory verification, suppressed audit logging, and an active protection mechanism designed to trigger a self-destruct sequence if changes were made incorrectly.

A key discovery was the importance of **change order**. Modifying certain registers before disabling protection would activate an irreversible trap.

---

## Key Findings

* Modbus TCP (port 502) was exposed with no authentication or encryption.
* Package selection logic was maliciously altered via holding registers.
* Safety mechanisms and audit logging were deliberately disabled.
* A protection coil was active, designed to trigger system destruction if remediation steps were performed out of order.
* The attacker left a clear signature within system registers as a calling card.

---

## Remediation & Outcome

I safely restored the system by:

1. Disabling the protection mechanism first.
2. Resetting package selection to Christmas gifts.
3. Re-enabling inventory verification and audit logging.
4. Verifying that no emergency or self-destruct mechanisms were triggered.

Normal operations were restored, confirmed both logically and visually via the CCTV feed, and Christmas deliveries resumed successfully.

---

## Skills & Concepts Learned

* ICS / OT incident response methodology
* SCADA and PLC architecture
* Modbus protocol weaknesses and abuse
* Logic manipulation attacks on physical systems
* Safe remediation sequencing in industrial environments
* Using Python to interact directly with PLCs
