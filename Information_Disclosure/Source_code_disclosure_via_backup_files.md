# Source code disclosure via backup files

### Goal - 

Identify and submit the database password, which is hard-coded in the leaked source code.

### Analysis/Exploitation -

When analyzing a web page, one of the first steps is always to check for the existence of a `robots.txt` file.

{% hint style="info" %}
💡 It is a file that requests search engine crawlers to either include or exclude certain parts of the site from their index. Sometimes, interesting locations are revealed.It is up to the crawler whether they obey these wishes or ignore them.
{% endhint %}

In this case, it points straight to the subdirectory `/backup` 

{% hint style="info" %}
💡 (other means to discover it would be tools like Burp Content Discovery, Ffuf, gobuster, wfuzz, ...)
{% endhint %}

Checking the directory shows a backup file for some Java code:

![](./images/2082bf838abe_001.png)

In the code, the credentials for the Postgres database connections can be found:

### Why It Works

The exploit succeeds because this lab leaks its source code via backup files in a hidden directory. to solve the lab, identify and submit the database password, which is hard-coded in the leaked source code.

The official solution confirms: Browse to /robots.txt and notice that it reveals the existence of a /backup directory. Browse to /backup to find the file ProductTemplate.java.bak. Al

The root cause is a failure in the application's security architecture specific to this information disclosure scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab leaks its source code via backup files in a hidden directory. To solve the lab, identify an"
- Disable verbose error messages and debug endpoints in production.
