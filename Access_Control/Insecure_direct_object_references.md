# Insecure direct object references

**Lab URL:** https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references

### Target Goal - 

find the password for the user `carlos`, and log into the account.

### Analysis/Exploitation -

- Select the **Live chat** tab.
- Send a message and then select **View transcript**.

**It’s sending a GET request to **`/download-transcript/2.txt`**! and we can see our own session’s transcript in response.**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/78ce20cf5321_001.png)

**What if I change the **`2.txt`** to **`1.txt`** Or **`3.txt`**, and so on?**

Change the filename to `1.txt` and review the text. Notice a password within the chat transcript.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/78ce20cf5321_002.png)

It should be **user **`carlos`**’s password!**

Login as carlos with this password

### Why It Works

This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs.

### Key Takeaways

- This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs.
