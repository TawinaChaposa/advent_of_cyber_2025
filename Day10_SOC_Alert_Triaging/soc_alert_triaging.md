#Day 10 – Alert Triaging & Investigation with Microsoft Sentinel

### Scenario Overview

The Security Operations Center (SOC) of **The Best Festival Company** was in chaos. Alerts flooded dashboards, lights flashed red and orange, and the sound of notifications echoed like a digital thunderstorm. The elves scrambled between consoles, unsure where the storm had begun.

Whispers suggested the **Evil Easter Bunnies** were behind the disruption. With the cloud environment under attack, the SOC had to act quickly to triage alerts, determine which were real threats, and prevent further compromise.

This scenario focuses on **alert triaging, investigation, and log correlation** to detect and understand security incidents in a cloud-native environment.

### My Role

As a **SOC Analyst**, I was tasked with:

* Reviewing alerts in Microsoft Sentinel
* Prioritising alerts based on severity, impact, and context
* Correlating related alerts to trace attacker activity
* Investigating logs to confirm malicious behaviour
* Documenting findings and escalating incidents when necessary

### Tools & Environment

* **Microsoft Azure Portal**
* **Microsoft Sentinel** (SIEM & SOAR platform)
* Custom log table: `Syslog_CL`
* KQL (Kusto Query Language) for log queries

### Investigation Approach

#### Step 1: Understanding Alert Triaging
When alerts appear in high volume, not all require immediate attention. I focused on four key dimensions to triage effectively:
<img width="615" height="216" alt="image" src="https://github.com/user-attachments/assets/6c8ae6f7-adfb-46fd-880f-3a90af096e4d" />

Based on these factors, alerts could be escalated, further investigated, or closed if false positives.

#### Step 2: Reviewing Alerts in Sentinel

I accessed Microsoft Sentinel and navigated to the **Incidents** tab. Eight incidents were observed in the lab: four high severity and four medium severity.

I started with **high-severity incidents** as they represented potential compromise points. One example: the **Linux PrivEsc – Kernel Module Insertion** alert.

Key observations included:

* Three events associated with the alert
* Three entities involved
* Classified as a **Privilege Escalation** tactic

By examining the incident timeline and similar incidents, I could correlate multiple alerts affecting the same entity, revealing a broader attack chain.

Example attack chain:
<img width="607" height="133" alt="image" src="https://github.com/user-attachments/assets/4283dfbc-801c-45d0-8430-3b9067c638e2" />

#### Step 3: Diving into Logs

Next, I investigated raw logs in `Syslog_CL` using KQL to validate alerts and uncover attacker actions. Example query:
    ```kql
    set query_now = datetime(2025-10-30T05:09:25.9886229Z);
    Syslog_CL
    | where host_s == 'app-02'
    | project _timestamp_t, host_s, Message
    ```

Observed events on app-02 included:
* Copying `/etc/shadow` to create backup
* Adding the user `Alice` to sudoers
* Modifying `backupuser` account
* Installing `malicious_mod.ko` kernel module
* Successful SSH login by root

These events indicated potential **privilege escalation and persistence activity**, warranting further investigation.

### Observations & Analysis

* High-severity alerts often involved multiple correlated entities.
* Suspicious actions included unusual commands, unauthorized sudoers modifications, and root SSH logins from external IPs.
* Triaging enabled prioritisation of critical incidents over noise and false positives.
* Detailed log analysis revealed the **sequence and scope of the attack**, highlighting the importance of correlation and timeline reconstruction.

### Key Skills & Concepts Learned

* Effective alert triaging based on severity, time, context, and impact
* Correlating multiple alerts to understand attack chains
* Using Microsoft Sentinel for incident management and investigation
* Querying logs using KQL to uncover attacker activity
* Understanding privilege escalation and persistence indicators in Linux
* Documenting findings for incident response and continuous improvement

### Example Commands & Queries
<img width="610" height="172" alt="image" src="https://github.com/user-attachments/assets/c9fbc0ae-cac1-4f08-92e0-dc9a401823ec" />

This task reinforced how **structured triage, correlation, and log analysis** allow SOC analysts to turn an overwhelming flood of alerts into actionable insights, uncovering attacker behaviour and prioritising response effectively.


