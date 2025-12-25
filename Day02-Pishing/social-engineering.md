# Day 02 – Phishing & Social Engineering

This challenge focused on social engineering and phishing techniques from a red team perspective.  
The objective was to design, deliver, and observe a phishing campaign to test employee awareness at The Best Festival Company (TBFC).

## Learning Objectives
- Understand social engineering concepts
- Learn different types of phishing attacks
- Build and host a fake login page
- Use the Social-Engineer Toolkit (SET) to send phishing emails
- Capture and analyze harvested credentials

## Key Concepts

### Social Engineering
Social engineering involves manipulating people into performing actions that compromise security, such as:
- Sharing passwords
- Clicking malicious links
- Opening harmful attachments

Attackers rely on psychological triggers like **urgency**, **authority**, and **curiosity**, which is why social engineering is often called *human hacking*.

### Phishing
Phishing is a form of social engineering delivered through messages such as:
- Email (phishing)
- SMS (smishing)
- Voice calls (vishing)
- QR codes (quishing)

The goal is to trick users into clicking links or entering credentials.

## Practical Exercise

### Hosting a Fake Login Page
A phishing server was launched using a provided Python script:

cd ~/Rooms/AoC2025/Day02
./server.py
The fake login page listened on port 8000 and captured credentials entered by victims.

##Sending a Phishing Email with SET

The Social-Engineer Toolkit (SET) was used to deliver the phishing email.The SET is an open-source tool primarily designed by David Kennedy for social engineering attacks which lets you compose and send a phishing email. Find out more about the social engineering : https://github.com/trustedsec/social-engineer-toolkit

##Key steps:
1. Launch SET: setoolkit
2. Select:
- Social-Engineering Attacks
- Mass Mailer Attack
- Single Email Address
- Configure sender details and SMTP server
- Craft a convincing phishing email containing the fake login URL

##Key Takeaways
- Humans are often the weakest link in security
- Realistic phishing emails are highly effective
- Credential reuse significantly increases impact
- Social engineering attacks can lead to full system compromise
