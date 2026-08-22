# Information disclosure on debug page

### Goal - 

Obtain and submit the `SECRET_KEY` environment variable.

### Analysis/Exploitation -

### Using free tools

When I try to avoid using features from Burp Professional, several good free tools allow for content discovery. The one I use here is [ffuf](https://github.com/ffuf/ffuf) together with the great wordlists provided by [SecLists](https://github.com/danielmiessler/SecLists).

First, I search for common directories within the web root of the application with

```bash
ffuf -w /usr/share/wordlists/SecLists-master/Discovery/Web-Content/directory-list-2.3-small.txt -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/FUZZ
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/a9db3d488244_001.png)

I can now search within this directory for common files with

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery-content/Web-Content/common.txt  -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/cgi-bin/FUZZ
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/a9db3d488244_002.png)

### Using Burp Professional

Go to the "Target" > "Site Map" tab. Right-click on the top-level entry for the lab and select "Engagement tools" > "Find comments". Notice that the home page contains an HTML comment that contains a link called "Debug". This points to `/cgi-bin/phpinfo.php`.

or Use the default options and start the content discovery. Burp quickly shows the `phpinfo.php` file in the site map:

Opening this file in the browser and scrolling through the content shows the answer:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/a9db3d488244_003.png)

### Why It Works

The exploit succeeds because this lab contains a debug page that discloses sensitive information about the application. to solve the lab, obtain and submit the secret_key environment variable.

The official solution confirms: With Burp running, browse to the home page. Go to the &quot;Target&quot; &gt; &quot;Site Map&quot; tab. Right-click on the top-level entry for the lab

The root cause is a failure in the application's security architecture specific to this information disclosure scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains debug page that discloses sensitive, demonstrating how information disclosure vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a debug page that discloses sensitive information about the application. To solve "
- Disable verbose error messages and debug endpoints in production.

## PortSwigger Lab

**Official lab:** Information disclosure on debug page

**PortSwigger:** https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-on-debug-page
