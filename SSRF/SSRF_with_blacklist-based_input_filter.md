# SSRF with blacklist-based input filter

**Lab URL:** https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter

### Goal -

Solve the PortSwigger lab: SSRF with blacklist-based input filter

### Exploitation

1. Identify the SSRF injection point
2. Test internal network access via the injection point
3. Bypass any input filters using techniques like URL encoding, DNS rebinding, or open redirects
4. Access sensitive internal endpoints or cloud metadata

### Why It Works

This lab has a stock check feature which fetches data from an internal system.

### Key Takeaways

- This lab has a stock check feature which fetches data from an internal system.
