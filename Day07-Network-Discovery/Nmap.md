#Day 07 – Network Service Discovery & Server Re-Entry

##Scenario Overview

Christmas preparations at The Best Festival Company (TBFC) came to a halt when HopSec breached the QA environment (tbfc-devqa01), locking the SOC team out of critical testing infrastructure. To make matters worse, the compromised server began transforming into a malicious EAST-mas node, controlled by rogue “bad bunnies”.

With QA frozen and the SOC-mas pipeline stalled, the mission was clear: trace HopSec’s trail, uncover exposed services, regain access to the server, and evict the attackers before the takeover was complete.

##My Role

I acted as a Security Analyst, tasked with performing network service discovery, identifying exposed services, exploiting misconfigurations, and regaining access to the compromised QA server using reconnaissance and enumeration techniques.

##Tools Used

- Nmap – Network and service discovery
- FTP client – Accessing exposed FTP services
- Netcat (nc) – Interacting with custom TCP services
- Dig – DNS enumeration via UDP
- Linux system utilities (ss, mysql)
- Investigation & Attack Path

The investigation began externally, using network scanning to identify exposed services. Once initial access was gained, on-host service discovery was performed to identify locally bound services and sensitive data stores.

The attack path followed three key phases:

- External reconnaissance and port scanning
- Service interaction and key extraction
- On-host enumeration and data access

##Key Findings

- Multiple unnecessary services were exposed to the network
- FTP allowed anonymous authentication
- A custom TCP service revealed sensitive information through simple commands
- DNS records exposed hidden data via TXT queries
- A locally bound MySQL database contained the final flag

##Useful Commands Used in This Challenge

<img width="605" height="403" alt="image" src="https://github.com/user-attachments/assets/8b216942-2879-4057-b668-1a19bcf2174a" />

Key 1 (FTP): 3aster_
Key 2 (Custom TBFC service): 15_th3_
Key 3 (DNS TXT record): n3w_xm45

These keys were combined to access the hidden admin console on the QA web application.

##Final Outcome

After regaining access to the server, on-host enumeration revealed a locally bound MySQL database running on port 3306. Querying the database exposed the final flag, confirming full compromise recovery.

##Skills & Concepts Learned

- Network service discovery using TCP and UDP scans
- Identifying misconfigured and unnecessary exposed services
- Service interaction via FTP and Netcat
- DNS enumeration using TXT records
- On-host service discovery with ss
- Local database enumeration
- Understanding attack surface reduction
