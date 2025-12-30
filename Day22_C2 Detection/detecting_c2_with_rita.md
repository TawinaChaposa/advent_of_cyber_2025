## Day 22 – Command and Control (C2) Detection Using RITA

### Scenario Overview

Following a series of attacks by King Malhare’s underlings, The Best Festival Company (TBFC) remained on high alert. Although network activity appeared quiet, Sir Elfo suspected hidden Command and Control (C2) communication within captured network traffic. To efficiently hunt for stealthy malicious connections, the team decided to use **RITA (Real Intelligence Threat Analytics)** after converting packet captures (PCAPs) into **Zeek logs**.

---

### My Role

I acted as a **Threat Hunter / SOC Analyst**, responsible for detecting potential Command and Control activity by analyzing network traffic. My task was to convert raw PCAP data into Zeek logs, import them into RITA, and interpret RITA’s analytics to identify suspicious beaconing, long-lived connections, and known indicators of compromise.

---

### Tools Used

* Zeek (Network Security Monitoring)
* RITA (Real Intelligence Threat Analytics)
* Linux command line
* PCAP network traffic files
* Threat intelligence (VirusTotal, blocklists)

---

### Investigative Approach

1. **Prepared network data** by converting PCAP files into structured Zeek logs.
2. **Imported Zeek logs into RITA** to allow automated behavioral analysis.
3. **Reviewed RITA results** focusing on severity scores, beaconing behavior, rare signatures, and threat intel matches.
4. **Analyzed suspicious domains and IP addresses**, correlating findings with known malicious indicators.
5. **Interpreted threat modifiers** such as long connection durations, non-standard ports, and low prevalence connections to assess C2 likelihood.

---

### Key Concepts Explained (Briefly)

* **Command and Control (C2):** Communication channel used by malware to receive instructions and exfiltrate data.
* **Beaconing:** Periodic communication from an infected host to a C2 server.
* **Zeek:** A passive network analysis tool that converts traffic into structured logs.
* **RITA:** A detection framework that analyzes Zeek logs to identify C2 patterns without inspecting payload contents.

---

### Commands Used (Reference Table)

| Purpose                         | Command                                                        |
| ------------------------------- | -------------------------------------------------------------- |
| List available directories      | `ls`                                                           |
| Convert PCAP to Zeek logs       | `zeek readpcap pcaps/AsyncRAT.pcap zeek_logs/asyncrat`         |
| Navigate to Zeek logs directory | `cd ~/zeek_logs/asyncrat/`                                     |
| List generated Zeek logs        | `ls`                                                           |
| Import Zeek logs into RITA      | `rita import --logs ~/zeek_logs/asyncrat/ --database asyncrat` |
| View RITA analysis results      | `rita view asyncrat`                                           |

---

### Key Findings

* RITA identified **suspicious external connections** with long FQDNs and uncommon patterns.
* A domain using **Cloudflare tunneling** (`trycloudflare.com`) was flagged as malicious via threat intelligence.
* An external IP address was confirmed as malicious using VirusTotal.
* Indicators included:

  * Long-lived connections
  * Non-standard ports
  * Rare TLS signatures
  * Low prevalence across internal hosts
* These behaviors strongly suggested **Command and Control activity**.

---

### Outcome

The analysis successfully demonstrated how **behavior-based network analytics** can uncover encrypted and stealthy C2 communications. Even with a small dataset, RITA provided valuable insights that allowed suspicious connections to be identified and prioritized for deeper investigation.

---

### Skills & Concepts Learned

* Converting PCAP files into Zeek logs
* Using RITA for threat hunting and C2 detection
* Interpreting beaconing behavior and threat modifiers
* Understanding encrypted C2 detection without payload inspection
* Correlating network metadata with threat intelligence
* Thinking like a threat hunter during post-compromise analysis

---
