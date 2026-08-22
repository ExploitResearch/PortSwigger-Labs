# Web LLM Attacks

Large Language Model (LLM) attacks target applications that integrate AI-powered features. As LLMs are increasingly embedded in web applications for chatbots, content generation, and API orchestration, they introduce new attack surfaces that traditional security testing may not cover.

Key vulnerability classes:

- **LLM API exploitation**: LLMs with access to APIs can be tricked into making unauthorized calls
- **Indirect prompt injection**: Attackers inject instructions via data sources that the LLM processes
- **Excessive agency**: LLMs granted too many permissions can perform destructive actions
- **Insecure output handling**: LLM output is rendered without sanitization, leading to XSS or other injection attacks

## Labs

- [Bypassing AI scanner defenses to exfiltrate sensitive information](./Bypassing_AI_scanner_defenses_to_exfiltrate_sensitive_information.md)
- [Exploiting AI agents to exfiltrate sensitive information](./Exploiting_AI_agents_to_exfiltrate_sensitive_information.md)
- [Exploiting AI agents to perform destructive actions](./Exploiting_AI_agents_to_perform_destructive_actions.md)
- [Exploiting AI agents to trigger secondary vulnerabilities](./Exploiting_AI_agents_to_trigger_secondary_vulnerabilities.md)
- [Exploiting LLM APIs with excessive agency](./Exploiting_LLM_APIs_with_excessive_agency.md)
- [Exploiting insecure output handling in LLMs](./Exploiting_insecure_output_handling_in_LLMs.md)
- [Exploiting vulnerabilities in LLM APIs](./Exploiting_vulnerabilities_in_LLM_APIs.md)
- [Indirect prompt injection](./Indirect_prompt_injection.md)
