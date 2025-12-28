#Day 2: Phishing Campaign & Social Engineering (Red Team Exercise)

##Scenario Overview

In response to several recent cybersecurity threats against The Best Festival Company (TBFC), the local red team scheduled an authorised penetration test to evaluate employee awareness and resilience against phishing attacks.

 ##My Role
 
As part of this exercise, I joined the TBFC red team alongside Recon McRed, Exploit McRed, and Pivot McRed. Our mission was to plan and execute a controlled phishing campaign to assess whether prior cybersecurity awareness training had been effective.

This simulation focused on human vulnerabilities, recognising that even well-secured systems can be compromised if users are manipulated.

##Understanding the Threat: Social Engineering & Phishing

Social engineering is the practice of manipulating people into making security mistakes such as:
- Clicking malicious links
- Entering credentials into fake portals
- Trusting messages that appear urgent or authoritative
  
Phishing is a subset of social engineering that uses communication channels such as:
- Email
- SMS (smishing)
- Voice calls (vishing)
- QR codes (quishing)

In this challenge, the objective was to harvest login credentials by convincing a target user to enter them into a fake TBFC portal login page.

#Attack Setup & Execution

##Building the Phishing Trap

To capture credentials, a fake TBFC login page was hosted using a provided Python script.
This page mimicked a legitimate portal and logged any credentials entered by the victim.
The phishing server was launched on the AttackBox and verified locally to ensure it appeared convincing to the target user.

##Delivering the Phishing Email (SET Toolkit)

To avoid suspicion, the phishing email was sent using the Social-Engineer Toolkit (SET), an open-source framework designed for social engineering campaigns.
The email was crafted to impersonate a trusted shipping company, increasing the likelihood of user interaction. The message included a link to the fake login page hosted earlier.

##Useful Commands & Actions Used

<img width="610" height="399" alt="image" src="https://github.com/user-attachments/assets/245d64b2-ede3-4a86-ada0-a9b73671a1c7" />

##Outcome

- Successfully harvested valid TBFC credentials
- Confirmed password reuse across internal services
- Demonstrated that employees remain vulnerable to phishing attacks
The results indicated that an attacker could gain unauthorized access to critical systems, posing a serious operational risk to TBFC.

##Skills & Concepts Learned

- Social engineering fundamentals
- Phishing campaign planning
- Credential harvesting techniques
- Using the Social-Engineer Toolkit (SET)
- Red team attack workflows
- Human-focused attack vectors

##Key Takeaway
This challenge highlighted that cybersecurity is not only a technical problem. Even with security controls in place, human error can lead to full system compromise if awareness and vigilance are lacking.
