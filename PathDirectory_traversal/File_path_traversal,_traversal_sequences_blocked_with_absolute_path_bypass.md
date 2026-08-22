# File path traversal, traversal sequences blocked with absolute path bypass

**Lab URL:** https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

open any product or open any image in new tab

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/37ac64c35968_001.png)

apply above filter to see image request and sent it to repeater

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/37ac64c35968_002.png)

This time however, the application blocks traversal sequences,requesting `../../../etc/passwd` does not lead to any file,If the webserver's default working directory is assumed when no path is explicitly given.

The application prepends this default working directory to the requested filename before trying to access the file (e.g. something like `'/var/html/www/' + $_REQUEST["filename"]`, the hardcoded first part could be interpreted as 'default working directory').Providing an absolute path could be the solution to exploit the path traversal vulnerability.

To bypass this, we can just provide the absolute path of the `/etc/passwd`:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/37ac64c35968_003.png)

### Why It Works

The application has a path traversal vulnerability in display of product images, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The path traversal vulnerability is exploitable because user input is processed without adequate validation.
