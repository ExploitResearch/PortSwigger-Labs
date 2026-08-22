# File path traversal, traversal sequences stripped with superfluous URL-decode

**Lab URL:** https://portswigger.net/web-security/file-path-traversal/lab-superfluous-url-decode

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

open any product or open any image in new tab

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/5db72fb5f8fa_001.png)

apply above filter to see image request and sent it to repeater

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/5db72fb5f8fa_002.png)

The lab description mentions that the application removes path traversal sequences first, then URLdecodes the remaining.

URL encoding is a means to ensure data is within the character range that is allowed in URLs, regardless of the actual value of the data. It is usually used for data that either contains characters
 that have a special meaning within URLs (e.g. `&`) or is non-printable data. But of course, it can be used for any printable ASCII characters.

In the case of characters within the normal ASCII range, the character is represented by a `%`, followed by its ASCII value in hex. The characters required for a path traversal and their encodings are:

```text
. --> %2e
/ --> %2f
```

### Accessing /etc/passwd

One level of URLdecoding is usually done by the server itself upon receiving the request. Therefore just encoding `../` as `%2e%2e%2f` will not be enough. The server performs the URLdecoding and passes `../` to the application, which filters it out. So URLencode the encoded string again before sending.

For this, we need to  also encode the `%` character itself:

```text
. --> %2e
/ --> %2f
% --> %25
```

One possible string would be `%252e%252e%252f`. The server decodes each `%25` to `%`, the strings `2e` and `2f `by themselves have no special meaning and will be treated as literal characters. The application, therefore, receives the sequence `%2e%2e%2f`, strips path traversal components (which are not there at this point), then URLdecodes it to `../`

**Now, we can use **`%252E%252E%252F`** as **`../`**:**

or we can **use **[**CyberChef**](https://gchq.github.io/CyberChef/)** to do URL encoding:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/5db72fb5f8fa_003.png)

Therefore A valid filename for the path traversal for `../../../etc/passwd`is  `%252e%252e%252f%252e%252e%252f%252e%252e%252fetc/passwd`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/5db72fb5f8fa_004.png)

### An alternative payload

Of course, when using Burp Repeater it is much easier to just type the `../../../` part in, than select it and `right-click -> Convert Selection -> URL -> URL encode all characters` twice.

This also encodes the `2 5 e f` characters from the first conversion, leading to a filename of `%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66etc/passwd`, which is also perfectly fine here:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/5db72fb5f8fa_005.png)
