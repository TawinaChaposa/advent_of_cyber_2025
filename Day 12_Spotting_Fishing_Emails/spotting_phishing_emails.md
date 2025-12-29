## Day 12 – Phishmas Takeover: Email Triage Under Fire

### Scenario Overview

With McSkidy still missing, TBFC is vulnerable. The Email Protection Platform — the SOC’s first line of defence — is completely offline.
That means no automated filtering, no quarantine, no safety net.

Every email reaching TBFC staff now has to be reviewed manually.

The SOC team believes Malhare’s Eggsploit Bunnies are exploiting this chaos by flooding inboxes with phishing emails designed to steal credentials, disrupt operations, and derail SOC-mas entirely. Some of these emails are obvious, but others are carefully disguised as internal IT requests, event logistics, or routine organisational communication.

### My Role
As part of the Incident Response Task Force, my role was to **triage incoming emails**, determine whether each message was legitimate, spam, or phishing, and identify the techniques being used by attackers.

Every wrong decision could give the attackers a foothold — and bring Wareville closer to EAST-mas.

### Key Concepts Observed During Analysis

#### 1. Phishing vs Spam

One of the first lessons reinforced was that **not every unwanted email is phishing**.

* **Spam** is usually bulk, low-effort, and marketing-focused.
* **Phishing** is targeted, intentional, and designed to deceive for gain (credentials, access, money, or data).

Understanding the *intent* behind the email was critical in making the correct classification.

#### 2. Impersonation

Several phishing emails attempted to impersonate trusted individuals or departments, especially McSkidy and TBFC IT.

Key red flags included:
* Use of **free or external email domains**
* Sender addresses that did not match TBFC’s naming conventions
* Display names that looked legitimate, but domains that were not

This reinforced the importance of **checking the actual sender**, not just the name shown in the inbox preview.

#### 3. Social Engineering Tactics

Most phishing emails relied heavily on social engineering rather than technical exploits. Common techniques included:

* **Urgency** (“urgent”, “immediately”, “action required”)
* **Authority** (posing as managers or IT staff)
* **Isolation** (discouraging verification through normal channels)
* **Fear or curiosity** (security incidents, missed messages, upgrades)
These tactics were designed to rush the user into acting before thinking.

#### 4. Typosquatting and Punycode
Some emails used domains that looked legitimate at first glance but contained:
* Slight spelling errors (typosquatting)
* Unicode characters that visually resembled Latin letters (punycode)
This showed how attackers exploit **visual trust** and inattention, especially when users are under pressure.

#### 5. Email Spoofing

Because email protection was down, spoofed emails were able to reach inboxes.

By checking email headers, it was possible to identify spoofing through:
* Failed **SPF**, **DKIM**, and **DMARC** checks
* Mismatched **Return-Path** addresses
This highlighted the importance of header analysis when surface-level inspection isn’t enough.

#### 6. Malicious Attachments

Some phishing attempts used attachments disguised as legitimate files (e.g., voice messages or shared documents).
Notably:
* HTML/HTA files were used instead of traditional executables
* These files can execute scripts directly and are commonly used for credential harvesting

### Trending Phishing Techniques Observed

Rather than delivering malware directly, attackers increasingly:

* Use **legitimate platforms** like OneDrive, Google Docs, or Dropbox
* Lure users into **fake login pages**
* Push interactions into **side channels** such as WhatsApp or phone calls
The goal is no longer just infection — it’s **access**.

## Differentiation Note: How Day 9 Differs from Earlier Phishing (Day 4 / Day 5)

Earlier phishing and social engineering challenges (Day 4 or 5) focused more on:

* Understanding **individual techniques in isolation**
* Learning *what* phishing is and *how* it works conceptually
* Analysing single scenarios or attacker methods

**Day 9 was different** because it was:

* **Operational and defensive**, not theoretical
* Focused on **decision-making under pressure**
* About **triage**, not just identification
* Required distinguishing between **legitimate emails, spam, and phishing**, not just spotting “bad” emails

This challenge simulated a **real SOC environment** where:

* Tools can fail
* Attackers blend in with normal business operations
* Analysts must rely on judgement, context, and careful inspection

It felt less like a lesson and more like **doing the actual job of an incident responder**.

### Final Reflection

Day 9 reinforced a critical truth in cybersecurity:
**When technology fails, people become the last line of defence.**

This room strengthened my ability to:
* Analyse emails holistically
* Think like both an attacker and a defender
* Make confident, evidence-based security decisions in realistic conditions
A strong reminder that phishing remains one of the most dangerous — and effective — attack vectors in modern security.
