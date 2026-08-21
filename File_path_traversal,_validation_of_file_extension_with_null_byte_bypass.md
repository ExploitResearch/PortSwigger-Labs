# File path traversal, validation of file extension with null byte bypass

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

Analyze how the filenames for the images are provided. Here, the absolute path is provided in the HTML:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2c773d2a-2c8c-4afe-8a11-42fb1f2f4718/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667HTESHUB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204701Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIC9g0fskJSZ8gL6JFbMmSqr1QpqGTLOIhY3tSzUKJ1lSAiBT3YCxdT6BaKw%2FeydEkzhklnMfu%2FAxoc99CiyXI3tvJCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM9HjXCPkM7pmbf9J8KtwDPWYyrt0F9c3JRI%2FGI3lGuItKaFKzDJ3kcj0Md%2B%2F33vTGPtBRSiEHg91F3exG%2BUqRc2YrlVHeK%2Bz18HUbdCCsyQLUHt0EWGbanD5XkOCvcLlSqD4DIE5yk8YLLjTiex93mi20bfqo07rrRwd5NLrXSuoyCoCi625%2FiZTiKE60%2Fo0FU29aeZvSorH09dtQF3Vqv0QoD9ztl%2F9oBPlX5gle4m89Ai7nLiXhi3HvjznptdbiEWZ%2BdezCwlP%2BxnO%2BdLdwdujNX9zUg02ng68gZElJZGm%2BZrl7ePSuS1bDeKtFaOHo%2B7x38N8Z8aZr%2FgPWDpFlk0xBPxPGLw1owCjmbZe3BlH%2FO05QEK1cDjxDUr36wngCOhvjmoSvTR5dbyQsbTVJpKqY7bd1VsNctGVpOcZXveTwfk2LW3Ia8xiitBJqjlJWJr%2BC6D%2Fr155vJ7SsTdRU42a4s7yrzwcGUgGdzazsvJJjbnzIDWDZWfSDOD43oGgoZNs3%2FknmLzb13pzBOIfpS11JezDCJtbHqfNeXVba42qnmM8R7OuHcYLIlpT9sFjFg8URZIA%2BrquyL9EnBVMTmNyIsIDTfVDGzvQUrX8eT%2BnIVjJ0hWM%2BB42BjKXttoXPu8iGIwhGWahcTe0wusai1AY6pgF5L1k60dBl69qoDwGPn49CawqCm5i1nZNk3RiOPPlqLAPZ9LIH7%2FeEKSoq7DfrJ3GwPqImznpnSBHfB0z45AYBOYpbQOa2PccpR9u4kVdNlPR9tqviWXnY77mNN91hW36Y7MbZq4RrrieQXA0plwuVPklckVcZZLqvCQ1koZSC5%2BMfDtOywDpKs%2FOiC%2F6FuwYcvSYBha4hcNSe9jV%2FqMV%2FCPhQroTx&X-Amz-Signature=88fa84cb73efcd0f25644da2414922dbac2911140d912ddbac28d5ff1700d716&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The rating image just above uses the `images` directory. Guessing that the product images might be in the same directory, try whether path traversal sequences are possible:

Use Burp Suite to intercept and modify a request that fetches a product image.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/14133811-b87b-4ae4-aa01-4c8bce2a0b39/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667HTESHUB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204701Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIC9g0fskJSZ8gL6JFbMmSqr1QpqGTLOIhY3tSzUKJ1lSAiBT3YCxdT6BaKw%2FeydEkzhklnMfu%2FAxoc99CiyXI3tvJCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM9HjXCPkM7pmbf9J8KtwDPWYyrt0F9c3JRI%2FGI3lGuItKaFKzDJ3kcj0Md%2B%2F33vTGPtBRSiEHg91F3exG%2BUqRc2YrlVHeK%2Bz18HUbdCCsyQLUHt0EWGbanD5XkOCvcLlSqD4DIE5yk8YLLjTiex93mi20bfqo07rrRwd5NLrXSuoyCoCi625%2FiZTiKE60%2Fo0FU29aeZvSorH09dtQF3Vqv0QoD9ztl%2F9oBPlX5gle4m89Ai7nLiXhi3HvjznptdbiEWZ%2BdezCwlP%2BxnO%2BdLdwdujNX9zUg02ng68gZElJZGm%2BZrl7ePSuS1bDeKtFaOHo%2B7x38N8Z8aZr%2FgPWDpFlk0xBPxPGLw1owCjmbZe3BlH%2FO05QEK1cDjxDUr36wngCOhvjmoSvTR5dbyQsbTVJpKqY7bd1VsNctGVpOcZXveTwfk2LW3Ia8xiitBJqjlJWJr%2BC6D%2Fr155vJ7SsTdRU42a4s7yrzwcGUgGdzazsvJJjbnzIDWDZWfSDOD43oGgoZNs3%2FknmLzb13pzBOIfpS11JezDCJtbHqfNeXVba42qnmM8R7OuHcYLIlpT9sFjFg8URZIA%2BrquyL9EnBVMTmNyIsIDTfVDGzvQUrX8eT%2BnIVjJ0hWM%2BB42BjKXttoXPu8iGIwhGWahcTe0wusai1AY6pgF5L1k60dBl69qoDwGPn49CawqCm5i1nZNk3RiOPPlqLAPZ9LIH7%2FeEKSoq7DfrJ3GwPqImznpnSBHfB0z45AYBOYpbQOa2PccpR9u4kVdNlPR9tqviWXnY77mNN91hW36Y7MbZq4RrrieQXA0plwuVPklckVcZZLqvCQ1koZSC5%2BMfDtOywDpKs%2FOiC%2F6FuwYcvSYBha4hcNSe9jV%2FqMV%2FCPhQroTx&X-Amz-Signature=375eddf7daed3824a962c344e6832c84bdbbf0f3e7a1c392906e9a06355fee4d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0cfdcd0c-0a28-44c7-b975-b31040ba38ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667HTESHUB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204701Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIC9g0fskJSZ8gL6JFbMmSqr1QpqGTLOIhY3tSzUKJ1lSAiBT3YCxdT6BaKw%2FeydEkzhklnMfu%2FAxoc99CiyXI3tvJCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM9HjXCPkM7pmbf9J8KtwDPWYyrt0F9c3JRI%2FGI3lGuItKaFKzDJ3kcj0Md%2B%2F33vTGPtBRSiEHg91F3exG%2BUqRc2YrlVHeK%2Bz18HUbdCCsyQLUHt0EWGbanD5XkOCvcLlSqD4DIE5yk8YLLjTiex93mi20bfqo07rrRwd5NLrXSuoyCoCi625%2FiZTiKE60%2Fo0FU29aeZvSorH09dtQF3Vqv0QoD9ztl%2F9oBPlX5gle4m89Ai7nLiXhi3HvjznptdbiEWZ%2BdezCwlP%2BxnO%2BdLdwdujNX9zUg02ng68gZElJZGm%2BZrl7ePSuS1bDeKtFaOHo%2B7x38N8Z8aZr%2FgPWDpFlk0xBPxPGLw1owCjmbZe3BlH%2FO05QEK1cDjxDUr36wngCOhvjmoSvTR5dbyQsbTVJpKqY7bd1VsNctGVpOcZXveTwfk2LW3Ia8xiitBJqjlJWJr%2BC6D%2Fr155vJ7SsTdRU42a4s7yrzwcGUgGdzazsvJJjbnzIDWDZWfSDOD43oGgoZNs3%2FknmLzb13pzBOIfpS11JezDCJtbHqfNeXVba42qnmM8R7OuHcYLIlpT9sFjFg8URZIA%2BrquyL9EnBVMTmNyIsIDTfVDGzvQUrX8eT%2BnIVjJ0hWM%2BB42BjKXttoXPu8iGIwhGWahcTe0wusai1AY6pgF5L1k60dBl69qoDwGPn49CawqCm5i1nZNk3RiOPPlqLAPZ9LIH7%2FeEKSoq7DfrJ3GwPqImznpnSBHfB0z45AYBOYpbQOa2PccpR9u4kVdNlPR9tqviWXnY77mNN91hW36Y7MbZq4RrrieQXA0plwuVPklckVcZZLqvCQ1koZSC5%2BMfDtOywDpKs%2FOiC%2F6FuwYcvSYBha4hcNSe9jV%2FqMV%2FCPhQroTx&X-Amz-Signature=55e1c7d93c24734ccd58619012d8478adb99abe33557abc074b7987085defa35&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/56296a57-ba4b-4ed4-ab3b-a677c887cfa4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667HTESHUB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204701Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIC9g0fskJSZ8gL6JFbMmSqr1QpqGTLOIhY3tSzUKJ1lSAiBT3YCxdT6BaKw%2FeydEkzhklnMfu%2FAxoc99CiyXI3tvJCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM9HjXCPkM7pmbf9J8KtwDPWYyrt0F9c3JRI%2FGI3lGuItKaFKzDJ3kcj0Md%2B%2F33vTGPtBRSiEHg91F3exG%2BUqRc2YrlVHeK%2Bz18HUbdCCsyQLUHt0EWGbanD5XkOCvcLlSqD4DIE5yk8YLLjTiex93mi20bfqo07rrRwd5NLrXSuoyCoCi625%2FiZTiKE60%2Fo0FU29aeZvSorH09dtQF3Vqv0QoD9ztl%2F9oBPlX5gle4m89Ai7nLiXhi3HvjznptdbiEWZ%2BdezCwlP%2BxnO%2BdLdwdujNX9zUg02ng68gZElJZGm%2BZrl7ePSuS1bDeKtFaOHo%2B7x38N8Z8aZr%2FgPWDpFlk0xBPxPGLw1owCjmbZe3BlH%2FO05QEK1cDjxDUr36wngCOhvjmoSvTR5dbyQsbTVJpKqY7bd1VsNctGVpOcZXveTwfk2LW3Ia8xiitBJqjlJWJr%2BC6D%2Fr155vJ7SsTdRU42a4s7yrzwcGUgGdzazsvJJjbnzIDWDZWfSDOD43oGgoZNs3%2FknmLzb13pzBOIfpS11JezDCJtbHqfNeXVba42qnmM8R7OuHcYLIlpT9sFjFg8URZIA%2BrquyL9EnBVMTmNyIsIDTfVDGzvQUrX8eT%2BnIVjJ0hWM%2BB42BjKXttoXPu8iGIwhGWahcTe0wusai1AY6pgF5L1k60dBl69qoDwGPn49CawqCm5i1nZNk3RiOPPlqLAPZ9LIH7%2FeEKSoq7DfrJ3GwPqImznpnSBHfB0z45AYBOYpbQOa2PccpR9u4kVdNlPR9tqviWXnY77mNN91hW36Y7MbZq4RrrieQXA0plwuVPklckVcZZLqvCQ1koZSC5%2BMfDtOywDpKs%2FOiC%2F6FuwYcvSYBha4hcNSe9jV%2FqMV%2FCPhQroTx&X-Amz-Signature=262fbafa028de4256dd2f7cc7e3d6b2b65e3e0562d12a9ad1bb20bf4750c45cc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

