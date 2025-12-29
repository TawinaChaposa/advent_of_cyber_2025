#Day 09 – Cracking Encrypted Files & Understanding Password Attacks

##Scenario Overview

As the balance between Easter and Christmas began to destabilise, unusual activity was detected within the systems of The Best Festival Company. Deep inside the servers, several encrypted PDF and ZIP files were discovered, labelled “North Pole Asset List.”

Sir Carrotbane suspected these files contained sensitive information linked to Santa’s master gift registry — data that could allow King Malhare to manipulate the festive order and gain control over both worlds.

With rumours spreading and encrypted data at risk of exposure, an urgent investigation was required to understand how weak passwords could undermine encryption and allow attackers to recover protected information.

##My Role

I acted as a Cybersecurity Analyst, tasked with investigating encrypted files and demonstrating how attackers exploit weak passwords to gain access to protected data.

##My objective was to:

- Identify the type of encryption used
- Apply appropriate password‑cracking techniques
- Demonstrate how dictionary and targeted attacks can recover weak passwords
- Understand how such activity can be detected and responded to from a defensive (SOC) perspective

##Tools Used

- Linux command line
- file utility (file type identification)
- pdfcrack
- john (John the Ripper)
- zip2john / pdf2john
- Wordlists (e.g. rockyou.txt)

##Investigation Approach

I began by identifying the file types to determine the correct cracking approach. Encrypted files require different tools depending on whether they are PDFs or ZIP archives.

Once the file types were confirmed, I prioritised dictionary attacks, as these are fast and highly effective against weak or reused passwords. Using common leaked password lists, I attempted to recover passwords without attacking the encryption algorithms themselves.

Where necessary, hashes were extracted into formats compatible with cracking tools such as John the Ripper. This allowed me to perform offline password attacks, simulating how a real attacker would operate once they had obtained an encrypted file.

Beyond the cracking process, I shifted perspective to the defender’s side — analysing how such activity could be detected through process monitoring, command‑line telemetry, GPU usage, and unusual file access patterns.

##Key Findings

- Encryption strength depends heavily on password quality rather than the algorithm alone.
- Weak or common passwords can be recovered quickly using dictionary attacks.
- Offline password cracking leaves no authentication logs, making it stealthy from a network perspective.
- Cracking tools generate detectable artefacts at the endpoint level, including:
- Known binaries (john, hashcat, pdfcrack)
- Wordlist access patterns
- High CPU or GPU utilisation
- Legacy encryption methods (especially in ZIP files) significantly lower the barrier for attackers.

##Outcome

The investigation demonstrated how attackers can bypass encrypted file protections without breaking cryptography itself, simply by exploiting poor password practices.

From a defensive standpoint, the exercise highlighted the importance of:

- Strong password policies
- Endpoint monitoring
- Detecting suspicious tooling and resource usage
- Educating users on encryption limitations

This task reinforced how encryption is only as strong as the password protecting it and why detection must extend beyond network‑based alerts.

Useful Commands & Queries
<img width="603" height="231" alt="image" src="https://github.com/user-attachments/assets/45d9883e-1fec-4d51-8fb1-be09d42973b6" />

##Skills & Concepts Learned

- Understanding password‑based file encryption
- Practical use of password‑cracking tools
- Dictionary vs brute‑force vs mask attacks
- Identifying endpoint indicators of cracking activity
- SOC‑level detection strategies for offline attacks
- Thinking from both attacker and defender perspectives
