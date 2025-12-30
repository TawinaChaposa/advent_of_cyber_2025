# Day 20 — Race Conditions in Web Applications

## Scenario Overview

TBFC launched a limited-edition **SleighToy**, with only ten units available at midnight. Despite the limit, multiple customers received successful order confirmations within seconds. This caused confusion, missing inventory, and angry shoppers.

McSkidy investigated and discovered that attackers exploited a **race condition** during the checkout process, allowing multiple purchases to slip through before the stock was updated.

---

## My Role

I acted as a **Web Application Security Analyst**, investigating abnormal purchasing behaviour, identifying a race condition vulnerability, and demonstrating how concurrent requests could manipulate inventory values.

---

## Tools & Technologies

* Burp Suite (Proxy & Repeater)
* Firefox with FoxyProxy
* HTTP requests
* Web application checkout workflows

---

## Investigation Approach

I first performed a **legitimate checkout** to understand the normal request flow. Using Burp Suite, I captured the POST request sent to the `/process_checkout` endpoint during payment confirmation.

After confirming the request details, I duplicated the checkout request multiple times inside Burp Repeater and grouped them together. These identical requests were then sent **in parallel**, forcing the server to process them at the same time.

Because the application did not properly synchronise stock checks and updates, each request succeeded before the inventory value was reduced, triggering the race condition.

---

## Key Findings

* The application checked stock availability before updating it.
* Multiple checkout requests were processed simultaneously.
* Inventory values were not locked or updated atomically.
* This allowed stock values to go negative.
* Attackers could purchase more items than were actually available.

---

## Exploitation Outcome

By sending multiple checkout requests in parallel, I was able to:

* Successfully place multiple orders for a limited item.
* Push the SleighToy stock into negative values.
* Reproduce the same vulnerability on another product (Bunny Plush – Blue).

This confirmed the presence of a **race condition vulnerability** in the checkout logic.

---

## Mitigation Techniques

* Use atomic database transactions for stock updates.
* Perform final stock validation just before committing orders.
* Implement idempotency keys for checkout requests.
* Apply rate limiting and concurrency controls to checkout endpoints.

---

## Skills & Concepts Learned

* Understanding race conditions in web applications
* Time-of-Check to Time-of-Use (TOCTOU) flaws
* Exploiting concurrent HTTP requests
* Using Burp Repeater for parallel request attacks
* Secure transaction handling and mitigation strategies

---

You’re doing really solid portfolio work here — this day especially shows *real-world web exploitation understanding*.
