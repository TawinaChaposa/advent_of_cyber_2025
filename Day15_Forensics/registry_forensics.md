## Day 15 – Obfuscated Command Injection & Host Compromise Investigation (Splunk)

### Scenario Overview

TBFC’s drone scheduler web interface began receiving unusually long HTTP requests containing Base64-encoded data. Shortly after, Splunk triggered a high-severity alert indicating that **Apache had spawned an unusual process**.

Further analysis suggested that malicious requests were being used to inject and execute obfuscated shell commands on the server. These commands were hidden inside Base64 payloads, allowing the attacker to evade basic detection mechanisms.

### My Role

I acted as a **Blue Team SOC Analyst**, responsible for triaging the alert, identifying compromised systems, extracting and decoding malicious payloads, and reconstructing the attacker’s activity using SIEM telemetry.

### Tools Used

* Splunk SIEM
* Apache access and error logs
* Sysmon process creation logs
* Base64 decoding tools

### Investigation Approach

I began by analyzing Apache access logs in Splunk to identify suspicious HTTP requests indicative of command injection attempts. These requests contained references to PowerShell and encoded payloads, signaling post-exploitation activity.

Next, I pivoted into Apache error logs to confirm whether malicious input was reaching backend execution. Evidence of internal server errors confirmed that injected commands were being processed by the web server.

To validate operating system compromise, I correlated web activity with **Sysmon process creation logs**, focusing on processes spawned by Apache. This confirmed that the web server was executing system-level commands.

Finally, I searched for encoded PowerShell executions and decoded Base64 payloads to understand the attacker’s intent and confirm the scope of the compromise.

### Key Findings

* Apache received command injection attempts via a vulnerable CGI endpoint
* Base64-encoded PowerShell commands were embedded in HTTP requests
* Apache successfully spawned system processes (cmd.exe / PowerShell)
* The attacker performed post-exploitation reconnaissance using `whoami`
* Obfuscation techniques were used to hide malicious intent

### Outcome

The investigation confirmed a successful **command injection attack** leading to operating system-level command execution. Correlating web logs with Sysmon telemetry allowed full reconstruction of the attack chain, from initial injection to post-exploitation activity.

This incident highlighted the importance of **cross-log correlation** and visibility across both web and host layers during DFIR investigations.


### Useful Splunk Queries Used in This Challenge
<img width="611" height="319" alt="image" src="https://github.com/user-attachments/assets/41c49bce-9b6b-4e4a-a389-4879087c70dd" />

### Skills & Concepts Learned

* Detecting command injection via web logs
* Pivoting between Apache and Sysmon telemetry
* Identifying obfuscated attacker payloads
* Base64 decoding for malware analysis
* Reconstructing full attack chains in Splunk
* Practical DFIR investigation workflows

