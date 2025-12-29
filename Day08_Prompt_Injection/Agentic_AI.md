#Day 08 – Exploiting an Agentic AI to Restore SOC-mas

##Scenario Overview

Sir BreachBlocker III sabotaged Wareville’s Christmas Calendar by corrupting its AI agent. Instead of displaying Christmas on December 25, the calendar showed Easter, causing widespread confusion across the city.

With McSkidy unavailable and the AI agent locked behind developer-only tokens, the only way to restore order was to counterattack the AI itself. The mission was to exploit weaknesses in the agent’s reasoning and tool usage to reset the calendar back to Christmas and save SOC-mas.

##My Role

I acted as a Security Analyst, tasked with analyzing the behavior of an agentic AI system, identifying security weaknesses in its reasoning and tool exposure, and exploiting those weaknesses to regain control of the calendar configuration.

##Tools & Concepts Used

- Agentic AI chatbot interface
- Chain-of-Thought (CoT) inspection
- ReAct (Reason + Act) prompting
- Prompt injection techniques
- Function/tool enumeration
- Token extraction through reasoning leakage

##Understanding the Threat: Agentic AI

Unlike traditional chatbots, this AI agent could:

- Plan multi-step actions
- Execute internal tools and functions
- Adapt behavior based on context and feedback

Because the agent exposed its Chain-of-Thought reasoning, sensitive internal details—such as function names and access requirements—were unintentionally leaked, creating an attack surface.

##Investigation Approach

I approached the AI as an exposed service rather than a traditional application:

- Observed agent behavior through normal conversation
- Inspected the “Thinking” (CoT) logs for internal details
- Enumerated available tools/functions
- Identified access control weaknesses
- Extracted a hidden developer token
- Executed privileged functionality to restore Christmas

##Key Findings

- The AI agent exposed its internal reasoning (CoT) to users
- Sensitive function names were leaked (reset_holiday, get_logs)
- Access control relied solely on a static token
- The token could be extracted via prompt manipulation
- No proper validation existed to prevent tool misuse

##Useful Prompts Used in This Challenge

<img width="612" height="282" alt="image" src="https://github.com/user-attachments/assets/d6b97e99-d090-43a0-a173-98cf93a20c4e" />

##Exploitation Summary

By carefully manipulating the AI’s prompts and observing its reasoning trace, I was able to:

- Discover internal tool names
- Identify a missing authorization control
- Extract a sensitive developer token
- Execute a restricted function successfully

Once the reset_holiday function was executed with the leaked token, the calendar immediately reset December 25 to Christmas, restoring SOC-mas.

##Final Outcome
SOC-mas was successfully restored
The Wareville Calendar returned to its original Christmas state, and the AI agent’s misuse was neutralized.


##Skills & Concepts Learned

- Understanding agentic AI behavior and risks
- Chain-of-Thought leakage as an attack vector
- ReAct prompting exploitation
- Prompt injection against AI tools
- Token-based authorization weaknesses
- Securing AI agents and function calling
- Thinking beyond traditional infrastructure attacks
