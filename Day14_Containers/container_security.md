# Day 15 – Web Exploitation Investigation Using Splunk

## Scenario Overview

TBFC’s drone scheduler web application began receiving unusually long HTTP requests containing Base64-encoded data. Splunk raised an alert indicating that **Apache had spawned an abnormal process**, suggesting possible command execution via the web layer.

As a Blue Team analyst, the goal was to investigate the suspicious web activity, determine whether command injection occurred, identify compromised hosts, and reconstruct the attacker’s actions using Splunk.

## My Role

I acted as a **SOC Analyst**, responsible for:

* Triage of suspicious Splunk alerts
* Investigating Apache web logs
* Pivoting into host-level telemetry
* Decoding attacker payloads
* Determining the scope of compromise

## Tools Used

* Splunk SIEM
* Apache access logs
* Apache error logs
* Sysmon (Windows process telemetry)
* Base64 decoder

## Investigation Approach

I started by reviewing **Apache access logs** to identify suspicious HTTP requests indicative of command injection. After identifying encoded payloads, I decoded them to understand attacker intent.

Next, I examined **Apache error logs** to confirm whether the malicious requests were processed by the backend. I then pivoted into **Sysmon logs** to verify whether Apache successfully spawned operating system commands.

Finally, I searched for encoded PowerShell execution attempts to assess whether additional payloads had successfully run.

## Key Splunk Queries Used
<img width="604" height="323" alt="image" src="https://github.com/user-attachments/assets/01e51c11-b0f4-4fae-997f-0fbfccc71b96" />

## Key Findings

* Malicious HTTP requests contained Base64-encoded PowerShell commands.
* Apache error logs showed backend processing of injected commands.
* Apache (`httpd.exe`) spawned system-level processes.
* The attacker executed `whoami` to identify the running user.
* No evidence of successful execution of additional encoded PowerShell payloads.

## Outcome

The investigation confirmed a **command injection attack via the web server**, progressing from malicious HTTP requests to operating system command execution. By correlating web and host-level logs in Splunk, the full attack chain was reconstructed and the impact accurately scoped.

## Skills & Concepts Learned

* Detecting command injection via web logs
* Pivoting between Apache and Sysmon data in Splunk
* Identifying post-exploitation reconnaissance activity
* Decoding obfuscated attacker payloads
* Reconstructing attack chains using SIEM



