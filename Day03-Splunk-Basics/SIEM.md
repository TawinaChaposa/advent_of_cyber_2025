#Day 03 – SOC Investigation with Splunk

## Overview
This challenge simulated a ransomware incident at The Best Festival Company (TBFC).  
Using Splunk, I performed a full SOC-style investigation to identify the intrusion vector, attacker behavior, and post-exploitation activity.

## Tools & Technologies
- Splunk (Search & Reporting)
- SPL (Search Processing Language)
- Web server logs
- Firewall logs

## Investigation Summary

### Log Sources
- `web_traffic`: HTTP requests to the web server
- `firewall_logs`: Allowed and blocked network traffic

### Key Findings

**1. Initial Detection**
- Identified abnormal traffic spikes using time-based analysis
- Narrowed the investigation window to the peak activity day

**2. Attacker Identification**
- Filtered out legitimate browsers
- Discovered a single external IP responsible for malicious activity  

**3. Attack Chain**
- Reconnaissance via cURL/Wget probing for configuration files
- Enumeration using path traversal attempts (`../../`)
- Exploitation through automated SQL injection tools (sqlmap, Havij)
- Successful Remote Code Execution via web shell
- Ransomware execution 

**4. Post-Exploitation Activity**
- Confirmed outbound Command-and-Control (C2) communication
- Measured data exfiltration from firewall logs

## Impact
- Successful compromise of the web server
- Confirmed ransomware staging and data exfiltration
- Demonstrated lack of effective outbound traffic controls

## Skills Demonstrated
- SOC alert triage
- Log analysis and correlation
- SPL query development
- Incident timeline reconstruction
- Ransomware and C2 detection
