# File path traversal, validation of file extension with null byte bypass

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

Analyze how the filenames for the images are provided. Here, the absolute path is provided in the HTML:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2c773d2a-2c8c-4afe-8a11-42fb1f2f4718/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XPRIKQNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221937Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCl%2B7afy7rtybJWteRt6J4WUmvLAhXKMw0VlnpAv6nQnAIgQciyMwd6CSLayuBaY0Jt11y8SrcmypoJ1i6Z6tO1ycgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDE02pHc5wAXz6kXi4ircA6V8S1rW77oK35o0bJOb4Qx8OQZtrLwor4koeL%2FRXBQSCM4b70acV0xn4NN%2FV%2FGZIugz5oAk0cUWAo4zuDPE0%2F1zhwQBtGwaiNLXGM1ZQJwaUa0F9l%2BPVKFoG1bGNA4GX6yRDwJ8yvc%2FO7ESrOlqThQcWDAxWwnXSUUxJoblWKt9Laj1z6gWyYWxedU0%2Fjs0IfBgUhfBK2t1TLXrslrubl9WJjMeY%2FFNNi2aBL%2Fqo%2FY2%2BIf2A2ETr%2FRsZsI8q2WJrod1czBECELn90Gfpv%2BQGirMfNxSjVZY%2F8eKEruplIMGJOofNNUDqJTbQ7sXu2d1bguR%2FzWdfEdQbmVYrED9i%2BdJnTqTT6kTg%2FZn3TKBM%2BrC5nKztjur9TMrjhKNFkHIU%2B45j%2FwRT1NI9WHWA1d0lhYLqWuFSVa3gpBK%2FH1d%2BmI4%2BwktwB9ao0OPv6dobNWPChmZ%2FvRW2GWAPuLZgvdCKyBC16sblp7kXeizRCDRFWAKKhlbcj1gozLGAiBPribeCoi13e18ghAo76Bu1OUG9%2FqnU1ml79CQx6eU2GN9tOgV2ezfXky8T3%2Bmk%2FGkzrn1PTWNlx%2BIhtrIRi3bmpvyezkSXiCW0aye5WZu607q4CYRiIL8fJpu1V09hdeAMOmDo9QGOqUBMO5j5queIqxqJKWZVjF1CEYxVocRUM%2Bbj4L8a3VISDvQjJwoHsTtWcNECIUZ%2BK9DBn2XsEeygSKJjqRwZV1SZLroylWIBznlUcLT8QI3p62RKO%2FfGhQqtg%2FgSEjfopilr9HDyQc3W04lKVEqDYI6ZselqL9XoPKqa0R6woCx1BgLkOSCuBq7MffUgu8CwiyVLlQ8ENdVtUhnRwlQWPBLIwBsVJK%2B&X-Amz-Signature=02a37a1bd9ddb0e2f1032960e1b09b40b0a6108fca1bdfe496213b2ad5140f87&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The rating image just above uses the `images` directory. Guessing that the product images might be in the same directory, try whether path traversal sequences are possible:

Use Burp Suite to intercept and modify a request that fetches a product image.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/14133811-b87b-4ae4-aa01-4c8bce2a0b39/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XPRIKQNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221937Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCl%2B7afy7rtybJWteRt6J4WUmvLAhXKMw0VlnpAv6nQnAIgQciyMwd6CSLayuBaY0Jt11y8SrcmypoJ1i6Z6tO1ycgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDE02pHc5wAXz6kXi4ircA6V8S1rW77oK35o0bJOb4Qx8OQZtrLwor4koeL%2FRXBQSCM4b70acV0xn4NN%2FV%2FGZIugz5oAk0cUWAo4zuDPE0%2F1zhwQBtGwaiNLXGM1ZQJwaUa0F9l%2BPVKFoG1bGNA4GX6yRDwJ8yvc%2FO7ESrOlqThQcWDAxWwnXSUUxJoblWKt9Laj1z6gWyYWxedU0%2Fjs0IfBgUhfBK2t1TLXrslrubl9WJjMeY%2FFNNi2aBL%2Fqo%2FY2%2BIf2A2ETr%2FRsZsI8q2WJrod1czBECELn90Gfpv%2BQGirMfNxSjVZY%2F8eKEruplIMGJOofNNUDqJTbQ7sXu2d1bguR%2FzWdfEdQbmVYrED9i%2BdJnTqTT6kTg%2FZn3TKBM%2BrC5nKztjur9TMrjhKNFkHIU%2B45j%2FwRT1NI9WHWA1d0lhYLqWuFSVa3gpBK%2FH1d%2BmI4%2BwktwB9ao0OPv6dobNWPChmZ%2FvRW2GWAPuLZgvdCKyBC16sblp7kXeizRCDRFWAKKhlbcj1gozLGAiBPribeCoi13e18ghAo76Bu1OUG9%2FqnU1ml79CQx6eU2GN9tOgV2ezfXky8T3%2Bmk%2FGkzrn1PTWNlx%2BIhtrIRi3bmpvyezkSXiCW0aye5WZu607q4CYRiIL8fJpu1V09hdeAMOmDo9QGOqUBMO5j5queIqxqJKWZVjF1CEYxVocRUM%2Bbj4L8a3VISDvQjJwoHsTtWcNECIUZ%2BK9DBn2XsEeygSKJjqRwZV1SZLroylWIBznlUcLT8QI3p62RKO%2FfGhQqtg%2FgSEjfopilr9HDyQc3W04lKVEqDYI6ZselqL9XoPKqa0R6woCx1BgLkOSCuBq7MffUgu8CwiyVLlQ8ENdVtUhnRwlQWPBLIwBsVJK%2B&X-Amz-Signature=a7ae703c60bee2e65aa960b386122adb030c6cbaf705381e60598242e5716536&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0cfdcd0c-0a28-44c7-b975-b31040ba38ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XPRIKQNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221937Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCl%2B7afy7rtybJWteRt6J4WUmvLAhXKMw0VlnpAv6nQnAIgQciyMwd6CSLayuBaY0Jt11y8SrcmypoJ1i6Z6tO1ycgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDE02pHc5wAXz6kXi4ircA6V8S1rW77oK35o0bJOb4Qx8OQZtrLwor4koeL%2FRXBQSCM4b70acV0xn4NN%2FV%2FGZIugz5oAk0cUWAo4zuDPE0%2F1zhwQBtGwaiNLXGM1ZQJwaUa0F9l%2BPVKFoG1bGNA4GX6yRDwJ8yvc%2FO7ESrOlqThQcWDAxWwnXSUUxJoblWKt9Laj1z6gWyYWxedU0%2Fjs0IfBgUhfBK2t1TLXrslrubl9WJjMeY%2FFNNi2aBL%2Fqo%2FY2%2BIf2A2ETr%2FRsZsI8q2WJrod1czBECELn90Gfpv%2BQGirMfNxSjVZY%2F8eKEruplIMGJOofNNUDqJTbQ7sXu2d1bguR%2FzWdfEdQbmVYrED9i%2BdJnTqTT6kTg%2FZn3TKBM%2BrC5nKztjur9TMrjhKNFkHIU%2B45j%2FwRT1NI9WHWA1d0lhYLqWuFSVa3gpBK%2FH1d%2BmI4%2BwktwB9ao0OPv6dobNWPChmZ%2FvRW2GWAPuLZgvdCKyBC16sblp7kXeizRCDRFWAKKhlbcj1gozLGAiBPribeCoi13e18ghAo76Bu1OUG9%2FqnU1ml79CQx6eU2GN9tOgV2ezfXky8T3%2Bmk%2FGkzrn1PTWNlx%2BIhtrIRi3bmpvyezkSXiCW0aye5WZu607q4CYRiIL8fJpu1V09hdeAMOmDo9QGOqUBMO5j5queIqxqJKWZVjF1CEYxVocRUM%2Bbj4L8a3VISDvQjJwoHsTtWcNECIUZ%2BK9DBn2XsEeygSKJjqRwZV1SZLroylWIBznlUcLT8QI3p62RKO%2FfGhQqtg%2FgSEjfopilr9HDyQc3W04lKVEqDYI6ZselqL9XoPKqa0R6woCx1BgLkOSCuBq7MffUgu8CwiyVLlQ8ENdVtUhnRwlQWPBLIwBsVJK%2B&X-Amz-Signature=70684c13ed321f4a0adf8903abbfd9ec896c19cb0efeb6f67cabced99076e74b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

And indeed, I can back out and return to the images directory. It confirms  path traversal sequences are possible:

**In the lab background, it said:**

> The application validates that the supplied filename ends with the expected file extension.

This check may be done by simply comparing the last 4 characters of the filename with the string literal `.jpg`. Any type of such string comparison may be vulnerable to an ancient issue: null termination of strings.

> 💡 **Some background**

A lot of low-level software like operating systems are written in C. In that language, strings are defined as sequences of characters that are followed by a null byte (a full byte of all zeros in binary, or %00 in URLencoding). There was no way of checking the length of a string but iterating over it until a null byte was found.

As long as the null byte was found within the reserved memory area, the length of the string was found. For example, if within a 10-character range the content is `ABCD%00`, then the string is `ABCD` with a length of 4. The amount of memory used is always one byte more than the usable length to account for the null byte.

This leads to a wonderful amount of bugs and vulnerabilities. If the developer does not account for this additional byte it can result in reading or writing over the reserved space, leading to all kinds of undesired consequences, like application crashes (best case) or arbitrary code execution (best case for attackers).

A lot of low-level functionality is still based on C, so terminates a string at the first null byte found. If all components of a system agree on the same behaviour, this does not pose an issue (besides the inherent issues of null termination).

But if components treat strings differently, then this different behaviour can be exploited.

For example, a lot of more modern languages have dedicated string types and do neither require nor use null termination for their strings. In this case, I want to access a file, so at some point, the request will be passed from the application to the operating system

### The malicious payload

I need to construct a string that fulfils these requirements:

- Succeeds the filename check in the application, in this case ending in `.jpg`
- Contains a null byte **(**`%00`**) **so that the operating system will not process the full filename
- Result filename must reference `/etc/passwd`

Above I already established that basic path traversal is possible. So a valid filename that fulfils the requirements would be `../../../etc/passwd%00Anything.jpg`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/56296a57-ba4b-4ed4-ab3b-a677c887cfa4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XPRIKQNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221937Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCl%2B7afy7rtybJWteRt6J4WUmvLAhXKMw0VlnpAv6nQnAIgQciyMwd6CSLayuBaY0Jt11y8SrcmypoJ1i6Z6tO1ycgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDE02pHc5wAXz6kXi4ircA6V8S1rW77oK35o0bJOb4Qx8OQZtrLwor4koeL%2FRXBQSCM4b70acV0xn4NN%2FV%2FGZIugz5oAk0cUWAo4zuDPE0%2F1zhwQBtGwaiNLXGM1ZQJwaUa0F9l%2BPVKFoG1bGNA4GX6yRDwJ8yvc%2FO7ESrOlqThQcWDAxWwnXSUUxJoblWKt9Laj1z6gWyYWxedU0%2Fjs0IfBgUhfBK2t1TLXrslrubl9WJjMeY%2FFNNi2aBL%2Fqo%2FY2%2BIf2A2ETr%2FRsZsI8q2WJrod1czBECELn90Gfpv%2BQGirMfNxSjVZY%2F8eKEruplIMGJOofNNUDqJTbQ7sXu2d1bguR%2FzWdfEdQbmVYrED9i%2BdJnTqTT6kTg%2FZn3TKBM%2BrC5nKztjur9TMrjhKNFkHIU%2B45j%2FwRT1NI9WHWA1d0lhYLqWuFSVa3gpBK%2FH1d%2BmI4%2BwktwB9ao0OPv6dobNWPChmZ%2FvRW2GWAPuLZgvdCKyBC16sblp7kXeizRCDRFWAKKhlbcj1gozLGAiBPribeCoi13e18ghAo76Bu1OUG9%2FqnU1ml79CQx6eU2GN9tOgV2ezfXky8T3%2Bmk%2FGkzrn1PTWNlx%2BIhtrIRi3bmpvyezkSXiCW0aye5WZu607q4CYRiIL8fJpu1V09hdeAMOmDo9QGOqUBMO5j5queIqxqJKWZVjF1CEYxVocRUM%2Bbj4L8a3VISDvQjJwoHsTtWcNECIUZ%2BK9DBn2XsEeygSKJjqRwZV1SZLroylWIBznlUcLT8QI3p62RKO%2FfGhQqtg%2FgSEjfopilr9HDyQc3W04lKVEqDYI6ZselqL9XoPKqa0R6woCx1BgLkOSCuBq7MffUgu8CwiyVLlQ8ENdVtUhnRwlQWPBLIwBsVJK%2B&X-Amz-Signature=911260114e38f846940cb15360a4cd04d0404103ec24f7161b9298ba7a05c9c9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
