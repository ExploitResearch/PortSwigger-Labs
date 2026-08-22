# Reflected XSS with some SVG markup allowed

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Perform a XSS attack that calls the alert() function.

### Analysis/Exploitation

Find which tags are allowed by brutforcing all tags from intruder ** <§§>**
Then Find the allowed event handler ** <svg><animatetransform%20§§=1>**
XSS cheat sheet

![](./images/b93c8bd344a1_001.png)

Use payload** <svg><animatetransform onbegin=alert(1) attributeName=transform>**

### Why It Works

The exploit succeeds because this lab has a simple reflected xss vulnerability. the site is blocking common tags but misses some svg tags and events.

The official solution confirms: Inject a standard XSS payload, such as: &lt;img src=1 onerror=alert(1)&gt; Observe that this payload gets blocked. In the next few steps, we'll use Bu

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some "
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.
