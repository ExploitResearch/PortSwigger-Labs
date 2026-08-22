# File path traversal, validation of file extension with null byte bypass

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

Analyze how the filenames for the images are provided. Here, the absolute path is provided in the HTML:

![](./images/668fdeb71724_001.png)

The rating image just above uses the `images` directory. Guessing that the product images might be in the same directory, try whether path traversal sequences are possible:

Use Burp Suite to intercept and modify a request that fetches a product image.

![](./images/668fdeb71724_002.png)

![](./images/668fdeb71724_003.png)

And indeed, I can back out and return to the images directory. It confirms  path traversal sequences are possible:

**In the lab background, it said:**

{% hint style="info" %}
The application validates that the supplied filename ends with the expected file extension.
{% endhint %}

This check may be done by simply comparing the last 4 characters of the filename with the string literal `.jpg`. Any type of such string comparison may be vulnerable to an ancient issue: null termination of strings.

{% hint style="info" %}
💡 **Some background**
{% endhint %}

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

![](./images/668fdeb71724_004.png)
