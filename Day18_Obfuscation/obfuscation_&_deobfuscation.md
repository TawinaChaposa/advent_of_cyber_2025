## Day 18 – Obfuscation and Deobfuscation

### Scenario

An alert was raised after a suspicious email impersonating *northpole-hr* delivered a small PowerShell script. The script contained unreadable strings, suggesting the use of obfuscation techniques to hide malicious behavior. As a Blue Teamer, the task was to safely analyze the script, identify the obfuscation methods used, and recover the original malicious content without executing it on a live system.

---

### My Role

I acted as a **Blue Team analyst** responsible for:

* Identifying obfuscated malicious content
* Safely deobfuscating hidden payloads
* Understanding attacker techniques used to evade detection
* Extracting indicators such as C2 URLs and API keys

---

### Approach

1. **Static Analysis First**

   * Opened the PowerShell script in an isolated VM
   * Reviewed comments and structure without executing blindly

2. **Identify Obfuscation Techniques**

   * Looked for patterns such as random characters, long encoded strings, and unusual symbols
   * Matched visual patterns to known techniques (ROT, Base64, XOR)

3. **Deobfuscation Using CyberChef**

   * Applied decoding operations in the correct order
   * Reversed layered obfuscation step-by-step
   * Verified output readability before proceeding

4. **Controlled Execution**

   * Ran the script only after understanding what it did
   * Completed both deobfuscation and re-obfuscation tasks as instructed

---

### Key Concepts Explained (Briefly)

* **Obfuscation**
  Making code or data hard to read to delay analysis and evade detection. It is not meant to be secure, just confusing.

* **Encoding (e.g., Base64)**
  Converts data into another format for safe transport or hiding content. Easily reversible and commonly abused by attackers.

* **ROT Ciphers (ROT1 / ROT13)**
  Shift letters by a fixed number. Easy to detect because word structure and spacing remain intact.

* **XOR Encoding**
  Uses a key and XOR logic to alter bytes. Output often looks random but keeps the same length. Common in malware due to simplicity and reversibility.

* **Layered Obfuscation**
  Combining multiple techniques (e.g., Base64 → XOR → gzip) to slow down defenders. Must be reversed in the opposite order.

---

### Tools Used

* **CyberChef** – for decoding, XOR operations, Base64 reversal, and gzip decompression
* **PowerShell (isolated VM)** – controlled execution after analysis
* **Visual Studio Code** – script inspection and navigation

---

### Outcome

* Successfully deobfuscated the hidden **C2 URL**
* Identified and re-obfuscated the attacker’s **API key using XOR**
* Retrieved both challenge flags:

  * `THM{C2_De0bfuscation_29838}`
  * `THM{API_Obfusc4tion_ftw_0283}`

---

### Key Takeaways

* Obfuscation is about **evasion, not security**
* Visual pattern recognition is a critical Blue Team skill
* CyberChef is essential for safe malware analysis
* Layered obfuscation requires patience and methodical reversal

---

