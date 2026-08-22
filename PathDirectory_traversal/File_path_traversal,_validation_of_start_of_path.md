# File path traversal, validation of start of path

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

Analyze how the filenames for the images are provided. Here, the absolute path is provided in the HTML:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/c9cba9089fd2_001.png)

open any product or open any image in new tab

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/c9cba9089fd2_002.png)

If you don't see it in the HTTP history, check if images are filtered out in the filter bar (by default it is hidden): apply above filter to see image request and sent it to repeater

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/c9cba9089fd2_003.png)

The application checks that the path starts with the expected values, in this case, the absolute path `/var/www/images`, so neither different absolute paths (`/etc/passwd`) nor relative paths (`../../../etc/passwd`) are possible.

What I do not know is if this check is done with the path provided in the request or with the canonical path. The canonical path is always a direct, absolute and unique path from the root to the fileFor example, the path `/var/www/images/30.jpg` is both absolute and canonical. The path `/var/www/images/../images/30.jpg` is still absolute but not canonical as it is not a unique identifier. I can simply leave some parts out (the `../images/`) and still identify the same file

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/c9cba9089fd2_004.png)

Here<span style="color: #E03E1B"> ../ </span>will move up a directory to <span style="color: #E03E1B">/var/www</span> and then adds<span style="color: #E03E1B"> /images/58.jpg </span>to it

Therefore I can reference any file on the file system when I use a non-canonical path, as long as it is absolute and starts with `/var/www/images/`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/PathDirectory_traversal/images/c9cba9089fd2_005.png)

Referencing the `/etc/passwd` file

## PortSwigger Lab

**Official lab:** File path traversal, validation of start of path

**PortSwigger:** https://portswigger.net/web-security/file-path-traversal/lab-validate-start-of-path
