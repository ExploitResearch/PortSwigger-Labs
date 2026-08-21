# File path traversal, validation of file extension with null byte bypass

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

Analyze how the filenames for the images are provided. Here, the absolute path is provided in the HTML:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2c773d2a-2c8c-4afe-8a11-42fb1f2f4718/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Y7IK5KRR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210408Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDW8vm4HbsyHj7ed1ipLxoEimfi7Cmd8%2BC7GbWras8LmAiBAGKK1cA%2BSB9Q07d7azhdpAvv2AEM3a1jVokXxl%2BqKuyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMaOg9KsNSwPv3Zsw7KtwD0r%2FdOFv8a3pOYiMzeCciAnVjSyDIKKFicBlHGdXERwsyG7%2FO63HKWkY8WssBaACut4jBR%2FsvJUbp%2BsSXchHbITSIRy5mU1qs8P9UGgbdHplGsrB41walVSuUrl5DKMYWVjMMbNO9VG6RS0EiRBPdr1kdgYH9c0%2BtSK1V7RpodAqadp0ow4Dtf47eyahYGW7oGcz5bMM1X7eAvP%2B61dN%2B8dVCOGxN3phLNEOmDwjuehNsq%2BJjWlWa6gudeoXPEzxbX%2BRVfFRSOwp7y2qA%2BO%2Fsx7yd2eelLk%2BO0djQ%2BV%2BT6FDdbDRZ9xu%2FXyG0vNWANBS9gG6v1I3cMMsJU3uiEkyKmJbvD6s%2BH4hz%2BD4pg5ukkfAnXvfzYlTgn2mufM4wTeTK0PBJ%2F8Y1C3JTEJTg7j79XkK%2FmMdKBve7Id390jgbj9%2F0w1n3PQcy1SNyzwnPgfWW54CknTEns%2BX67LLvhzy6COMNWc3aBpaYMVZ016Am1gsc4xHY5MN%2FTWXKkYb%2B3FgJbHwQ3bL8QOYIKlagdkV92T35cGzlVAvWNNoGhN7bGpKrxrUDY%2FidB%2FCJaXkOPQZMJdKz3N2XVXvJwjVUv476OvIaxxY8Srk1s6Wy4EVVLxOgyfkSlCqtamxDmbkw7sWi1AY6pgF3F4ZKeNfuwP3oniE3AyVAVfCHLgXZfwxUjIFXRUVs%2FN2Pfbjr6hCtrhL%2FPEORhL6qxaLcBItB17MiUbUUD0c3m%2B2fxFwA9wLysuJNEcSB0DT7mWSEQtPnTdKG4OUti5tPNfZnAcpMavjBxvgVODnvfuam3WHs7rPVkGrkfYvpHbf1o0LZGW4YpkuS1c0a2rbCPvnnVqX4oqbgk17%2FnlD0652zwjsx&X-Amz-Signature=b5d61115030b82a927af1fdf32270307104b7785dea367a3bd7586517ce8248a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The rating image just above uses the `images` directory. Guessing that the product images might be in the same directory, try whether path traversal sequences are possible:

Use Burp Suite to intercept and modify a request that fetches a product image.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/14133811-b87b-4ae4-aa01-4c8bce2a0b39/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Y7IK5KRR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210408Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDW8vm4HbsyHj7ed1ipLxoEimfi7Cmd8%2BC7GbWras8LmAiBAGKK1cA%2BSB9Q07d7azhdpAvv2AEM3a1jVokXxl%2BqKuyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMaOg9KsNSwPv3Zsw7KtwD0r%2FdOFv8a3pOYiMzeCciAnVjSyDIKKFicBlHGdXERwsyG7%2FO63HKWkY8WssBaACut4jBR%2FsvJUbp%2BsSXchHbITSIRy5mU1qs8P9UGgbdHplGsrB41walVSuUrl5DKMYWVjMMbNO9VG6RS0EiRBPdr1kdgYH9c0%2BtSK1V7RpodAqadp0ow4Dtf47eyahYGW7oGcz5bMM1X7eAvP%2B61dN%2B8dVCOGxN3phLNEOmDwjuehNsq%2BJjWlWa6gudeoXPEzxbX%2BRVfFRSOwp7y2qA%2BO%2Fsx7yd2eelLk%2BO0djQ%2BV%2BT6FDdbDRZ9xu%2FXyG0vNWANBS9gG6v1I3cMMsJU3uiEkyKmJbvD6s%2BH4hz%2BD4pg5ukkfAnXvfzYlTgn2mufM4wTeTK0PBJ%2F8Y1C3JTEJTg7j79XkK%2FmMdKBve7Id390jgbj9%2F0w1n3PQcy1SNyzwnPgfWW54CknTEns%2BX67LLvhzy6COMNWc3aBpaYMVZ016Am1gsc4xHY5MN%2FTWXKkYb%2B3FgJbHwQ3bL8QOYIKlagdkV92T35cGzlVAvWNNoGhN7bGpKrxrUDY%2FidB%2FCJaXkOPQZMJdKz3N2XVXvJwjVUv476OvIaxxY8Srk1s6Wy4EVVLxOgyfkSlCqtamxDmbkw7sWi1AY6pgF3F4ZKeNfuwP3oniE3AyVAVfCHLgXZfwxUjIFXRUVs%2FN2Pfbjr6hCtrhL%2FPEORhL6qxaLcBItB17MiUbUUD0c3m%2B2fxFwA9wLysuJNEcSB0DT7mWSEQtPnTdKG4OUti5tPNfZnAcpMavjBxvgVODnvfuam3WHs7rPVkGrkfYvpHbf1o0LZGW4YpkuS1c0a2rbCPvnnVqX4oqbgk17%2FnlD0652zwjsx&X-Amz-Signature=a383d03f5be180267b2acda1269d62b4fdfae7be5d31a127c3feb2ac5be837cf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0cfdcd0c-0a28-44c7-b975-b31040ba38ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Y7IK5KRR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210408Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDW8vm4HbsyHj7ed1ipLxoEimfi7Cmd8%2BC7GbWras8LmAiBAGKK1cA%2BSB9Q07d7azhdpAvv2AEM3a1jVokXxl%2BqKuyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMaOg9KsNSwPv3Zsw7KtwD0r%2FdOFv8a3pOYiMzeCciAnVjSyDIKKFicBlHGdXERwsyG7%2FO63HKWkY8WssBaACut4jBR%2FsvJUbp%2BsSXchHbITSIRy5mU1qs8P9UGgbdHplGsrB41walVSuUrl5DKMYWVjMMbNO9VG6RS0EiRBPdr1kdgYH9c0%2BtSK1V7RpodAqadp0ow4Dtf47eyahYGW7oGcz5bMM1X7eAvP%2B61dN%2B8dVCOGxN3phLNEOmDwjuehNsq%2BJjWlWa6gudeoXPEzxbX%2BRVfFRSOwp7y2qA%2BO%2Fsx7yd2eelLk%2BO0djQ%2BV%2BT6FDdbDRZ9xu%2FXyG0vNWANBS9gG6v1I3cMMsJU3uiEkyKmJbvD6s%2BH4hz%2BD4pg5ukkfAnXvfzYlTgn2mufM4wTeTK0PBJ%2F8Y1C3JTEJTg7j79XkK%2FmMdKBve7Id390jgbj9%2F0w1n3PQcy1SNyzwnPgfWW54CknTEns%2BX67LLvhzy6COMNWc3aBpaYMVZ016Am1gsc4xHY5MN%2FTWXKkYb%2B3FgJbHwQ3bL8QOYIKlagdkV92T35cGzlVAvWNNoGhN7bGpKrxrUDY%2FidB%2FCJaXkOPQZMJdKz3N2XVXvJwjVUv476OvIaxxY8Srk1s6Wy4EVVLxOgyfkSlCqtamxDmbkw7sWi1AY6pgF3F4ZKeNfuwP3oniE3AyVAVfCHLgXZfwxUjIFXRUVs%2FN2Pfbjr6hCtrhL%2FPEORhL6qxaLcBItB17MiUbUUD0c3m%2B2fxFwA9wLysuJNEcSB0DT7mWSEQtPnTdKG4OUti5tPNfZnAcpMavjBxvgVODnvfuam3WHs7rPVkGrkfYvpHbf1o0LZGW4YpkuS1c0a2rbCPvnnVqX4oqbgk17%2FnlD0652zwjsx&X-Amz-Signature=9e54d0ce9e95c255f30f7312716f49f0d4ab1b59a9487fdf531cc7fd308d496d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/56296a57-ba4b-4ed4-ab3b-a677c887cfa4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Y7IK5KRR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210408Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDW8vm4HbsyHj7ed1ipLxoEimfi7Cmd8%2BC7GbWras8LmAiBAGKK1cA%2BSB9Q07d7azhdpAvv2AEM3a1jVokXxl%2BqKuyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMaOg9KsNSwPv3Zsw7KtwD0r%2FdOFv8a3pOYiMzeCciAnVjSyDIKKFicBlHGdXERwsyG7%2FO63HKWkY8WssBaACut4jBR%2FsvJUbp%2BsSXchHbITSIRy5mU1qs8P9UGgbdHplGsrB41walVSuUrl5DKMYWVjMMbNO9VG6RS0EiRBPdr1kdgYH9c0%2BtSK1V7RpodAqadp0ow4Dtf47eyahYGW7oGcz5bMM1X7eAvP%2B61dN%2B8dVCOGxN3phLNEOmDwjuehNsq%2BJjWlWa6gudeoXPEzxbX%2BRVfFRSOwp7y2qA%2BO%2Fsx7yd2eelLk%2BO0djQ%2BV%2BT6FDdbDRZ9xu%2FXyG0vNWANBS9gG6v1I3cMMsJU3uiEkyKmJbvD6s%2BH4hz%2BD4pg5ukkfAnXvfzYlTgn2mufM4wTeTK0PBJ%2F8Y1C3JTEJTg7j79XkK%2FmMdKBve7Id390jgbj9%2F0w1n3PQcy1SNyzwnPgfWW54CknTEns%2BX67LLvhzy6COMNWc3aBpaYMVZ016Am1gsc4xHY5MN%2FTWXKkYb%2B3FgJbHwQ3bL8QOYIKlagdkV92T35cGzlVAvWNNoGhN7bGpKrxrUDY%2FidB%2FCJaXkOPQZMJdKz3N2XVXvJwjVUv476OvIaxxY8Srk1s6Wy4EVVLxOgyfkSlCqtamxDmbkw7sWi1AY6pgF3F4ZKeNfuwP3oniE3AyVAVfCHLgXZfwxUjIFXRUVs%2FN2Pfbjr6hCtrhL%2FPEORhL6qxaLcBItB17MiUbUUD0c3m%2B2fxFwA9wLysuJNEcSB0DT7mWSEQtPnTdKG4OUti5tPNfZnAcpMavjBxvgVODnvfuam3WHs7rPVkGrkfYvpHbf1o0LZGW4YpkuS1c0a2rbCPvnnVqX4oqbgk17%2FnlD0652zwjsx&X-Amz-Signature=25ce93c5191f5779809ae3e1c7c381d316e5e72fc601b6cc9b5c5db28b989e1d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

