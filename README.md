# PortSwigger Web Security Academy — Labs & Notes

A collection of notes, solutions, and techniques from the [PortSwigger Web Security Academy](https://portswigger.net/web-security/) labs, organized by vulnerability category.

## Structure

This repository mirrors the original Notion hierarchy. Each category is a directory containing its own README and individual lab solution pages.

| Category | Labs | Description |
|----------|------|-------------|
| [Book Notes](Book_Notes/) | 3 | General Burp Suite methodology and web app (in)security theory |
| [authentication](authentication/) | 4 | Auth bypass, 2FA, password resets, multi-factor |
| [SQL Injection](SQL_Injection/) | 6 | SQLMap, cheat sheet, examining DB, blind SQLi |
| [SSRF](SSRF/) | 1 | Server-Side Request Forgery basics |
| [Clickjacking](Clickjacking/) | 5 | Frame-based attacks with various defenses |
| [XSS](XSS/) | 3 | Reflected, Stored, DOM-based Cross-Site Scripting |
| [CSRF](CSRF/) | 12 | Token validation bypass, SameSite bypasses |
| [Access Control](Access_Control/) | 13 | IDOR, role-based access, multi-step process bypass |
| [Path/Directory traversal](PathDirectory_traversal/) | 6 | Path traversal with various filter bypasses |
| [File upload vulnerabilities](File_upload_vulnerabilities/) | 7 | Web shell upload, Content-Type bypass, path traversal |
| [OS Command Injection](OS_Command_Injection/) | 5 | Simple, blind, with time delays and output redirection |
| [Business logic vulnerabilities](Business_logic_vulnerabilities/) | 11 | Client-side trust, logic flaws, race conditions |
| [Information Disclosure](Information_Disclosure/) | 5 | Error messages, debug pages, backup files |
| [JWT attack](JWT_attack/) | 10 | Signature bypass, weak keys, algorithm confusion |
| [CORS](CORS/) | 4 | Origin reflection, null origin, insecure protocols |
| [Race condition](Race_condition/) | 6 | Limit overrun, multi-endpoint, partial construction |
| [API Pentesting](API_Pentesting/) | — | API security testing notes |
| [XXE](XXE/) | — | XML External Entity notes |
| [Extentions](Extentions/) | — | Burp Suite extensions notes |

## References

- [PortSwigger Web Security Academy](https://portswigger.net/web-security/)
- [PortSwigger Research Blog](https://portswigger.net/research)

## Source

Originally maintained in [Notion](https://www.notion.so/). Exported and structured as Markdown for version control.

## License

See [LICENSE](LICENSE). Lab content references PortSwigger Web Security Academy; refer to PortSwigger for original lab licensing terms.
