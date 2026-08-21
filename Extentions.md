# Extentions

## Built-in **Logger**  Vs Logger++

### Built-in Logger (recommended default)

Advantages:

- Native, actively maintained by [PortSwigger](https://portswigger.net/?utm_source=chatgpt.com).
- Logs traffic from all Burp tools, including Intruder, Repeater, Scanner, and extensions. HTTP History only shows proxied browser traffic. ([PortSwigger](https://portswigger.net/burp/documentation/desktop/tools/logger?utm_source=chatgpt.com))
- Tool filtering, search, custom columns, annotations, CSV export, and script-based filters are built in. ([PortSwigger](https://portswigger.net/burp/documentation/desktop/tools/logger/entries?utm_source=chatgpt.com))
- Better performance and memory handling with current Burp releases.
- No extension compatibility issues after Burp updates.

### Logger++

Advantages:

- More powerful filtering language.
- Color-coded highlighting and tagging workflows.
- Grep/extraction features for finding secrets, emails, tokens, etc.
- Advanced export options and Elasticsearch integration. ([PortSwigger](https://portswigger.net/bappstore/470b7057b86f41c396a97903377f3d81?utm_source=chatgpt.com))

Disadvantages:

- Additional memory/CPU overhead during large Intruder attacks.
- Some features that made Logger++ popular years ago now overlap with built-in Logger capabilities. ([PortSwigger](https://portswigger.net/burp/documentation/desktop/tools/logger?utm_source=chatgpt.com))

### For bug bounty hunting

Setup would be:

- **Logger** → primary traffic view.
- **HTTP History** → only for browser-driven traffic.
- **Logger++** → install only if you want complex filters like:
  - highlight all POST requests,
  - find JWTs/API keys with regex,
  - tag admin requests,
  - export large datasets for analysis. ([Hacking Articles](https://www.hackingarticles.in/burpsuite-for-pentester-logger/?utm_source=chatgpt.com))

A common bug bounty filter to use is:

- Logger → Tool = Intruder
- Hide static content (css/js/images)
- Show only parameterized requests

That cuts thousands of noisy Intruder requests down to the interesting ones very quickly ([PortSwigger](https://portswigger.net/burp/documentation/desktop/tools/logger/filter/view?utm_source=chatgpt.com))

### Burp Suite Default Active Scan vs Active Scan++ Extension

| Key Differences  | Default Scanner | Active Scan++ |
|---|---|---|
| Maintenance | PortSwigger (continuous) | Community / PortSwigger Research |
| Speed | Configurable, optimized | Adds overhead (more probes) |
| False positive rate | Tuned & low | Slightly higher (research-oriented) |
| Smuggling detection | ✗ | ✓ |
| Cache poisoning | ✗ | ✓ |
| Collaborator-based blind checks | Limited | Extensive |
| Prototype pollution | ✗ | ✓ |
| Burp Pro required | Yes | Yes (uses Collaborator) |

---

**Use both together.** Active Scan++ doesn't replace the default scanner — it runs *alongside* it and fires additional checks on the same requests. The typical workflow is:

1. Run the default active scan for baseline coverage
1. Have Active Scan++ enabled so it augments with its extra insertion points and checks automatically
1. For targeted testing (smuggling, cache poisoning), trigger Active Scan++ checks manually on specific requests