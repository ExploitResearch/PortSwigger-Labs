# 2FA simple bypass

**Lab URL:** https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-simple-bypass

- Log in to your own account. Your 2FA verification code will be sent to you by email. Click the **Email client** button to access your emails.
- Go to your account page and make a note of the URL.
- Log out of your account.
- Log in using the victim's credentials.
- When prompted for the verification code, manually change the URL to navigate to `/my-account`. The lab is solved when the page loads.

### Why It Works

This lab's two-factor authentication can be bypassed.

### Key Takeaways

- This lab's two-factor authentication can be bypassed.
