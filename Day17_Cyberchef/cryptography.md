## Day 17 — CyberChef & Web Logic Analysis

### Focus

Using **CyberChef** and **browser developer tools** to decode, deobfuscate, and reverse application logic in order to bypass layered authentication controls.

### Scenario Overview

McSkidy is imprisoned behind multiple logical “locks” implemented in a web application. Each lock relies on **encoding, hashing, or transformation logic** rather than traditional authentication. The goal is to inspect the application, understand how credentials are processed, and reverse the logic to unlock each stage.

### My Role

I acted as a Blue Team Analyst, responsible for inspecting web application behavior, identifying encoded and obfuscated data, and reversing authentication logic to bypass layered access controls. My role involved analyzing client-side logic, inspecting HTTP headers and responses, decoding hidden messages using CyberChef, and reconstructing the transformation chains used to protect credentials in order to safely unlock each stage of the system.

###  Key Concepts Learned

* **Encoding vs Encryption**

  * Encoding = compatibility & representation (reversible)
  * Encryption = confidentiality & security (key-based)
* Common encoding/obfuscation techniques:
  * Base64
  * XOR
  * ROT13 / ROT47
  * Hex
  * MD5 hashing
* Importance of **reversing logic**, not guessing passwords

### 🛠 Tools Used

* **CyberChef** (encoding/decoding & chained recipes)
* **Browser Developer Tools**

  * Network tab (HTTP headers)
  * Debugger tab (login logic)
  * Page source inspection
* **CrackStation** (hash lookup)

### Investigation Techniques

| Technique                 | Purpose                          |
| ------------------------- | -------------------------------- |
| Base64 decode             | Reveal hidden chat messages      |
| HTTP header inspection    | Extract hints & recipe IDs       |
| JavaScript logic review   | Understand credential processing |
| Chained CyberChef recipes | Reverse multi-layer encoding     |
| Hash cracking             | Recover plaintext from MD5       |


### Lock Progression Summary

| Lock   | Protection Logic                                       |
| ------ | ------------------------------------------------------ |
| Lock 1 | Base64 encoding                                        |
| Lock 2 | Double Base64 encoding                                 |
| Lock 3 | XOR + Base64                                           |
| Lock 4 | MD5 hash                                               |
| Lock 5 | Dynamic recipe (ROT / XOR / Base64 / Hex combinations) |

Each lock required:

* Extracting **encoded credentials**
* Understanding **how the app transforms them**
* Reversing the process using CyberChef

### Key Takeaways

* **Client-side logic is not security**
* Obfuscation ≠ protection
* Encoding chains can always be reversed if the logic is exposed
* CyberChef is a powerful tool for **DFIR, SOC analysis, and web forensics**
* Browser developer tools are essential for Blue Team investigations

### Blue Team Insight
This room highlights how attackers — and defenders — can exploit **exposed application logic**. Understanding encoding, hashing, and transformation chains is critical when analyzing suspicious web behavior, malware obfuscation, or covert data exfiltration.

### Encoding Concepts Used 

* Base64 Encoding
Base64 is an encoding method used to convert binary or text data into ASCII characters for safe transmission over systems that may not handle raw data well. It is commonly abused by attackers to hide commands in web traffic or scripts, but it offers no security since it can be easily decoded.

* XOR Encoding
XOR is a reversible encoding technique that combines data with a key using a bitwise operation. Its key property is that applying the same XOR operation twice with the same key restores the original data, making it common in malware obfuscation rather than encryption.

* ROT13 / ROT47
ROT-based encodings shift characters by a fixed number of positions. They are simple obfuscation techniques often used to hide readable strings from quick inspection, but they provide no real security.

* MD5 Hashing
MD5 is a cryptographic hash function that converts input data into a fixed-length hash. While it is designed to be one-way, weak or common inputs can often be recovered using hash databases, making MD5 unsuitable for secure authentication.

* Chained Encoding
Chained encoding involves applying multiple encoding or transformation steps in sequence. Attackers use this to increase analysis difficulty, but understanding the order of operations allows analysts to systematically reverse the process.
