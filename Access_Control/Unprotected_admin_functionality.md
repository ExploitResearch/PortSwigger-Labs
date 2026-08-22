# Unprotected admin functionality

### Target Goal - 

delete the user `carlos`

### Analysis/Exploitation -

- Go to the lab and view `robots.txt` by appending `/robots.txt` to the lab URL. Notice that the `Disallow` line discloses the path to the admin panel.
![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/09c257cbe144_001.png)

- In the URL bar, replace `/robots.txt` with `/administrator-panel` to load the admin panel.
![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/09c257cbe144_002.png)

- Delete `carlos`

## PortSwigger Lab

**Official lab:** Unprotected admin functionality

**PortSwigger:** https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality
