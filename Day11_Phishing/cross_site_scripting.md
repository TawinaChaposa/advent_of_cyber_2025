## Day X – Cross-Site Scripting (XSS) Investigation

### Scenario Overview

After last year’s automation and tech modernisation, **Santa’s Workshop** rolled out a secure messaging portal that allows direct communication with McSkidy. However, the system logs started revealing strange behaviour: suspicious search terms, unusual messages, and letters that looked more like scripts than heartfelt notes.

Something wasn’t right. The evidence suggested someone was abusing the portal’s input fields to inject malicious content. My task was to investigate the logs, reproduce the behaviour, and determine whether the portal was vulnerable to **Cross-Site Scripting (XSS)** attacks.

### My Role

As a **Cybersecurity Analyst**, I was responsible for:

* Understanding how XSS attacks work
* Testing the portal for reflected and stored XSS vulnerabilities
* Observing system logs to confirm malicious execution
* Identifying security weaknesses and recommending mitigations


### Target Application

* Web application hosted at: `http://MACHINE_IP`
* Features included:

  * Message search functionality
  * Message submission form

### Understanding the Threat: XSS

Cross-Site Scripting (XSS) occurs when a web application accepts user input and displays it without proper sanitisation or encoding. As a result, browsers may interpret injected content as executable JavaScript rather than harmless text.

In this investigation, I focused on:

* **Reflected XSS** – payload executes immediately in the response
* **Stored XSS** – payload is saved on the backend and executes for all users who load the page

### Investigation & Exploitation

#### Step 1: Testing for Reflected XSS

I began by testing the **search functionality**, since search terms are often reflected directly in the page output.

I injected the following payload into the search bar:```<script>alert('Reflected Meow Meow')</script> ```

After clicking **Search Messages**, an alert box appeared in the browser.

**What this confirmed:**

* User input was reflected directly into the page
* The application did not encode or sanitise input
* The browser executed injected JavaScript
* The portal was vulnerable to **Reflected XSS**

To validate this further, I reviewed the **System Logs** section, which clearly showed the injected script being processed.

#### Step 2: Testing for Stored XSS

Next, I investigated whether malicious input could be **persisted on the server**.

The message submission form stores messages for McSkidy to view later, making it a strong candidate for stored XSS testing.

I submitted the following payload as a message:```<script>alert('Stored Meow Meow')</script>```

After sending the message, I refreshed the page.

**Result:**

* The alert appeared automatically on page load
* The payload was executed repeatedly
* The script had been stored server-side

This confirmed a **Stored XSS vulnerability**, meaning any user who accessed the page would unknowingly execute the attacker’s code.

### Observations & Impact

The portal suffered from both reflected and stored XSS vulnerabilities due to improper input handling.

**Potential attacker impact included:**

* Stealing session cookies
* Impersonating users
* Injecting phishing prompts
* Defacing the interface
* Running arbitrary JavaScript in victim browsers

The presence of stored XSS made this especially dangerous, as it allowed a “set-and-forget” attack affecting all users.

### Defensive Lessons Learned

This investigation reinforced several critical XSS prevention techniques:

* **Sanitise and encode all user input and output**
* Avoid dangerous rendering methods like `innerHTML`
* Use safer alternatives such as `textContent`
* Protect cookies with:
  * `HttpOnly`
  * `Secure`
  * `SameSite` attributes
* Validate and filter inputs at both client and server levels

### Key Skills Demonstrated

* Web application security testing
* Identifying reflected vs stored XSS
* Payload injection and validation
* Log analysis for malicious behaviour
* Secure coding awareness and mitigation strategies

This exercise demonstrated how even a seemingly simple messaging portal can become a powerful attack surface if input validation is overlooked. By methodically testing, observing behaviour, and validating through logs, I was able to identify the root cause of the unusual activity affecting McSkidy’s portal.
