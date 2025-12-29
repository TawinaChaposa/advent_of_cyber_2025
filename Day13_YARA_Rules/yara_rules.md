## Day 13 – Threat Hunting with YARA

### Scenario Overview

During the SOC-mas incident, McSkidy went missing but left behind a series of image files suspected to contain hidden messages. Although the files appeared harmless, the blue team believed they were part of a covert communication method used during crisis response.

The task was to analyze these files and uncover the hidden message using **YARA rules**.

### My Role

I acted as a **Blue Team Analyst**, responsible for creating and executing YARA rules to detect hidden indicators within non-malicious-looking files and extract meaningful intelligence.

### Tools Used

* YARA
* Regular expressions (regex)
* Recursive directory scanning
* Linux command-line tools

### Investigation Approach

I began by reviewing the scenario requirements to understand what indicators to search for. Based on this, I designed a YARA rule to detect strings beginning with a specific keyword followed by alphanumeric characters.

Using regex within YARA, I scanned all image files in the target directory recursively. Once matches were identified, I extracted and organized the results to reconstruct the intended message.

### Key Findings

* Multiple image files contained hidden text-based indicators.
* All indicators followed a consistent keyword-and-code pattern.
* When ordered correctly, the extracted values revealed a clear message from McSkidy.

### Outcome

The investigation confirmed that YARA can be effectively used beyond traditional malware detection. By applying pattern-matching logic to image files, hidden indicators were successfully uncovered, demonstrating YARA’s value in threat hunting and intelligence analysis.

### Skills & Concepts Learned

* Writing custom YARA rules
* Using regex for pattern-based detection
* Threat hunting in non-executable files
* Applying YARA in blue team investigations
