# Indirect prompt injection

### Goal -

Solve the PortSwigger lab: Indirect prompt injection

### Exploitation

1. Interact with the LLM to understand its capabilities and API access
2. Craft a prompt that exploits the specific vulnerability (excessive agency, indirect injection, or insecure output)
3. Use the LLM's API access to perform the attack (delete users, exfiltrate data, etc.)

### Why It Works

The exploit succeeds because this lab is vulnerable to indirect prompt injection. the user carlos frequently uses the live chat to ask about the lightweight "l33t" leather jacket product. to solve the lab, delete carlos.

The root cause is a failure in the application's security architecture specific to this llm attacks scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to indirect prompt injection. The user carlos frequently uses the live chat t"
- LLM API access should follow least-privilege — block destructive operations by default.
