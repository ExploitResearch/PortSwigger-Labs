# File path traversal, validation of file extension with null byte bypass

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

Analyze how the filenames for the images are provided. Here, the absolute path is provided in the HTML:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2c773d2a-2c8c-4afe-8a11-42fb1f2f4718/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UHWMCH3I%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215537Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCGdJRnG0a%2BMKt477Ax%2FiOJsv%2FewsB1%2FprZ26XFTpHw4gIhAL%2Fu7s2I%2ByAdj0mRJSd3rd6vICskyAcWFa4Wk4mWjNqeKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw9Y45KQC0xsYOja%2BQq3APG8R9GrAuoHDheXgnW%2F9Aix2A4PRsX5cvWHke3kn8a2XwvROR6mhzhMeWPBoe3Itdgbn6uLyEUwua1mGzPc8hIHzkNFQMJvS2eBgiQiCsk3rU1AfiBcH346fb63zQAPXorRJgI%2FmpBCvTntXyqtIw%2FNkYlP84XHnBqB4wouCWTJ1Dm6ejS8QYfs6NEnOGopuC9bBs%2BMqPjRA5a9S%2BwE8OiJuE%2BppRH6HQCkdsjAw2ENhpyMdFRAFTZuc4sN%2FXBHmW4N4vkjHKYracOMfaFQDIh2VKcIysGs8zFzSbX25OFo6QY8wE3O0iIlmKSkAIA0ofJhFgB3UiKWG8XfpZJbe%2FNKIXBPRpWRXwFsm%2FVyvo0XHoBgNq19oxOtBmPWonwRhjKGVUZkMUThhBQWKQzUHfCMCAxlhz0DE6plAbd2W12gbWhRX%2FIzRGhbQmuns5pl1TK0BxhrlJKSvH4Zt4n5st6Tpzfsgb5%2F9JSwWh7JE6mtPnIxASXKe4b2qPIKms59Jj6g34bYv%2BQrtTQAKw9XzPMPXxJff%2FcGMFewfSAmL0bVJ8kdlYDM7ZFwFBNLGTQOD%2F9FevwfJht2bLO3D%2FX%2FRMadRLJY8ZrKg%2Fm615YKG7IMIntglB8OgShyZUghTC7hqPUBjqkAbF0L9t61fT6NdIlRpcdkScjIN8uDzTF9abT5HIsimP74PCfufZanlcyoq7YdpqXyRBxYlaas4uskFSvoaOr318iSvFhm8FpPCWnz2J6QlO4ukYPcRGnln3FmTS5KSH2MtekmA0qo0xYxWAQ37iGTxEew99n1RTvYXwtC0VcavBPEHai7HHtDGln0O7%2FouSVcjsF9%2F%2BWuDxbBL43tYJyQfTxNxuk&X-Amz-Signature=f8056394dfa5f2609b98b46866ce428adb173aefe2a869eceaa1d918e9d2ca2c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The rating image just above uses the `images` directory. Guessing that the product images might be in the same directory, try whether path traversal sequences are possible:

Use Burp Suite to intercept and modify a request that fetches a product image.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/14133811-b87b-4ae4-aa01-4c8bce2a0b39/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UHWMCH3I%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215537Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCGdJRnG0a%2BMKt477Ax%2FiOJsv%2FewsB1%2FprZ26XFTpHw4gIhAL%2Fu7s2I%2ByAdj0mRJSd3rd6vICskyAcWFa4Wk4mWjNqeKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw9Y45KQC0xsYOja%2BQq3APG8R9GrAuoHDheXgnW%2F9Aix2A4PRsX5cvWHke3kn8a2XwvROR6mhzhMeWPBoe3Itdgbn6uLyEUwua1mGzPc8hIHzkNFQMJvS2eBgiQiCsk3rU1AfiBcH346fb63zQAPXorRJgI%2FmpBCvTntXyqtIw%2FNkYlP84XHnBqB4wouCWTJ1Dm6ejS8QYfs6NEnOGopuC9bBs%2BMqPjRA5a9S%2BwE8OiJuE%2BppRH6HQCkdsjAw2ENhpyMdFRAFTZuc4sN%2FXBHmW4N4vkjHKYracOMfaFQDIh2VKcIysGs8zFzSbX25OFo6QY8wE3O0iIlmKSkAIA0ofJhFgB3UiKWG8XfpZJbe%2FNKIXBPRpWRXwFsm%2FVyvo0XHoBgNq19oxOtBmPWonwRhjKGVUZkMUThhBQWKQzUHfCMCAxlhz0DE6plAbd2W12gbWhRX%2FIzRGhbQmuns5pl1TK0BxhrlJKSvH4Zt4n5st6Tpzfsgb5%2F9JSwWh7JE6mtPnIxASXKe4b2qPIKms59Jj6g34bYv%2BQrtTQAKw9XzPMPXxJff%2FcGMFewfSAmL0bVJ8kdlYDM7ZFwFBNLGTQOD%2F9FevwfJht2bLO3D%2FX%2FRMadRLJY8ZrKg%2Fm615YKG7IMIntglB8OgShyZUghTC7hqPUBjqkAbF0L9t61fT6NdIlRpcdkScjIN8uDzTF9abT5HIsimP74PCfufZanlcyoq7YdpqXyRBxYlaas4uskFSvoaOr318iSvFhm8FpPCWnz2J6QlO4ukYPcRGnln3FmTS5KSH2MtekmA0qo0xYxWAQ37iGTxEew99n1RTvYXwtC0VcavBPEHai7HHtDGln0O7%2FouSVcjsF9%2F%2BWuDxbBL43tYJyQfTxNxuk&X-Amz-Signature=64a257b02325c5574144b2897be7fb9c03433e8d8284cc8cda5c61919a4a0e48&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0cfdcd0c-0a28-44c7-b975-b31040ba38ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UHWMCH3I%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215537Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCGdJRnG0a%2BMKt477Ax%2FiOJsv%2FewsB1%2FprZ26XFTpHw4gIhAL%2Fu7s2I%2ByAdj0mRJSd3rd6vICskyAcWFa4Wk4mWjNqeKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw9Y45KQC0xsYOja%2BQq3APG8R9GrAuoHDheXgnW%2F9Aix2A4PRsX5cvWHke3kn8a2XwvROR6mhzhMeWPBoe3Itdgbn6uLyEUwua1mGzPc8hIHzkNFQMJvS2eBgiQiCsk3rU1AfiBcH346fb63zQAPXorRJgI%2FmpBCvTntXyqtIw%2FNkYlP84XHnBqB4wouCWTJ1Dm6ejS8QYfs6NEnOGopuC9bBs%2BMqPjRA5a9S%2BwE8OiJuE%2BppRH6HQCkdsjAw2ENhpyMdFRAFTZuc4sN%2FXBHmW4N4vkjHKYracOMfaFQDIh2VKcIysGs8zFzSbX25OFo6QY8wE3O0iIlmKSkAIA0ofJhFgB3UiKWG8XfpZJbe%2FNKIXBPRpWRXwFsm%2FVyvo0XHoBgNq19oxOtBmPWonwRhjKGVUZkMUThhBQWKQzUHfCMCAxlhz0DE6plAbd2W12gbWhRX%2FIzRGhbQmuns5pl1TK0BxhrlJKSvH4Zt4n5st6Tpzfsgb5%2F9JSwWh7JE6mtPnIxASXKe4b2qPIKms59Jj6g34bYv%2BQrtTQAKw9XzPMPXxJff%2FcGMFewfSAmL0bVJ8kdlYDM7ZFwFBNLGTQOD%2F9FevwfJht2bLO3D%2FX%2FRMadRLJY8ZrKg%2Fm615YKG7IMIntglB8OgShyZUghTC7hqPUBjqkAbF0L9t61fT6NdIlRpcdkScjIN8uDzTF9abT5HIsimP74PCfufZanlcyoq7YdpqXyRBxYlaas4uskFSvoaOr318iSvFhm8FpPCWnz2J6QlO4ukYPcRGnln3FmTS5KSH2MtekmA0qo0xYxWAQ37iGTxEew99n1RTvYXwtC0VcavBPEHai7HHtDGln0O7%2FouSVcjsF9%2F%2BWuDxbBL43tYJyQfTxNxuk&X-Amz-Signature=5764e383db1f5c692701a9779ed3bc178809c64bfde3c989b46d8871611a8e7e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/56296a57-ba4b-4ed4-ab3b-a677c887cfa4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UHWMCH3I%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215537Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCGdJRnG0a%2BMKt477Ax%2FiOJsv%2FewsB1%2FprZ26XFTpHw4gIhAL%2Fu7s2I%2ByAdj0mRJSd3rd6vICskyAcWFa4Wk4mWjNqeKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw9Y45KQC0xsYOja%2BQq3APG8R9GrAuoHDheXgnW%2F9Aix2A4PRsX5cvWHke3kn8a2XwvROR6mhzhMeWPBoe3Itdgbn6uLyEUwua1mGzPc8hIHzkNFQMJvS2eBgiQiCsk3rU1AfiBcH346fb63zQAPXorRJgI%2FmpBCvTntXyqtIw%2FNkYlP84XHnBqB4wouCWTJ1Dm6ejS8QYfs6NEnOGopuC9bBs%2BMqPjRA5a9S%2BwE8OiJuE%2BppRH6HQCkdsjAw2ENhpyMdFRAFTZuc4sN%2FXBHmW4N4vkjHKYracOMfaFQDIh2VKcIysGs8zFzSbX25OFo6QY8wE3O0iIlmKSkAIA0ofJhFgB3UiKWG8XfpZJbe%2FNKIXBPRpWRXwFsm%2FVyvo0XHoBgNq19oxOtBmPWonwRhjKGVUZkMUThhBQWKQzUHfCMCAxlhz0DE6plAbd2W12gbWhRX%2FIzRGhbQmuns5pl1TK0BxhrlJKSvH4Zt4n5st6Tpzfsgb5%2F9JSwWh7JE6mtPnIxASXKe4b2qPIKms59Jj6g34bYv%2BQrtTQAKw9XzPMPXxJff%2FcGMFewfSAmL0bVJ8kdlYDM7ZFwFBNLGTQOD%2F9FevwfJht2bLO3D%2FX%2FRMadRLJY8ZrKg%2Fm615YKG7IMIntglB8OgShyZUghTC7hqPUBjqkAbF0L9t61fT6NdIlRpcdkScjIN8uDzTF9abT5HIsimP74PCfufZanlcyoq7YdpqXyRBxYlaas4uskFSvoaOr318iSvFhm8FpPCWnz2J6QlO4ukYPcRGnln3FmTS5KSH2MtekmA0qo0xYxWAQ37iGTxEew99n1RTvYXwtC0VcavBPEHai7HHtDGln0O7%2FouSVcjsF9%2F%2BWuDxbBL43tYJyQfTxNxuk&X-Amz-Signature=fe9bbf1728e2fd68217221ed865eff6baf5a249117e98da7532f2e5c47bec46c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
