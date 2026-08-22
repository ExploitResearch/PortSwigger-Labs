# Brute-forcing a stay-logged-in cookie

**Lab URL:** https://portswigger.net/web-security/authentication/other-mechanisms/lab-brute-forcing-a-stay-logged-in-cookie

- With Burp running, log in to your own account with the **Stay logged in** option selected. Notice that this sets a `stay-logged-in` cookie.
- Examine this cookie in the [Inspector](https://portswigger.net/burp/documentation/desktop/tools/inspector) panel and notice that it is Base64-encoded. Its decoded value is `wiener:51dc30ddc473d43a6011e9ebba6ca770`. Study the length and character set of this string and notice that it could be an MD5 hash. Given that the plaintext is your username, you can make an educated guess that this may be a hash of your password. Hash
your password using MD5 to confirm that this is the case. We now know
that the cookie is constructed as follows: `base64(username+':'+md5HashOfPassword)`
- Log out of your account.
- Send the most recent `GET /my-account` request to Burp Intruder.
- In Burp Intruder, add a payload position to the `stay-logged-in` cookie and add your own password as a single payload.
- Under **Payload processing**, add the following rules in order. These rules will be applied sequentially to each payload before the request is submitted.
  - Hash: `MD5`
  - Add prefix: `wiener:`
  - Encode: `Base64-encode`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/authentication/Vulnerabilities_in_other_authentication_mechanisms/images/c931fe37d0ae_001.png)

- As the **Update email** button is only displayed when you access the `/my-account` page in an authenticated state, we can use the presence or absence of
this button to determine whether we've successfully brute-forced the
cookie. On the **Settings** tab, add a grep match rule to flag any responses containing the string `Update email`. Start the attack.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/authentication/Vulnerabilities_in_other_authentication_mechanisms/images/c931fe37d0ae_002.png)

- Notice that the generated payload was used to
successfully load your own account page. This confirms that the payload
processing rules work as expected and you were able to construct a valid cookie for your own account.
- Make the following adjustments and then repeat this attack:
  - Remove your own password from the payload list and add the list of [candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords) instead.
  - Change the **Add prefix** rule to add `carlos:` instead of `wiener:`.
- When the attack is finished, the lab will be
solved. Notice that only one request returned a response containing `Update email`. The payload from this request is the valid `stay-logged-in` cookie for Carlos's account.
