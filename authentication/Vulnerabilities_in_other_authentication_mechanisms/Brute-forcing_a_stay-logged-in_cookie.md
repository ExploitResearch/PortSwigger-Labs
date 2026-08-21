# Brute-forcing a stay-logged-in cookie

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f91009d9-d88e-4a5e-9e1f-e8b23c9a058a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662Z6JL4LT%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221730Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC6qztqDfpXvlbtRM6cNg2yL3L0cnCoz2nNrkoN%2BpXHUAIhAPweg1XuRwDtPDOg1bOnTv9DlxVnsOq7JnS7I4Vghk%2BmKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw%2FRe79hTs45CA7PGIq3AOetPrXSbD0t91Yg1ZAarKlOvdIX1rKA48rvUjrLHzym3rkbJNP08dew0qbZP1kG1Wbpwn3bJkyHI0nsaPwRMsL7RXz9KreVUKpkSt63YNUSpGVaKXYfHyEPEV6MjQjGmrLNlj973jV8HL%2FnYxov8sDH%2FAZTM3CUTLJCc8%2FbXvgfJiZX%2BfXBn5GnLRBT9EEPFyHdft1p94mfFb8nzVYOu%2BfF53RASEzwjB9Ay1gIBvnlM9qKE4p6E7RD7YdfDClYkFNT0eGZqTssmk842AohGdTyFnaGoV9wjcE%2BJmcJlqHPTtUmywbfmUwcqGmg9iNQNPeMyeF4radfjBHEB%2BHlXUxv3LIaj%2BL1jEoppu00xUiFNaUjjpIOTKjBqn%2FrWxKAG05eWbA7hRK0GX10mqUz17glS1HtZHxvK2FF8IcY2K9Y1QfFBdlzONdUUQEOW%2BjVD2THvpw7KaSfMeMlU4C6gZxombIK3XZaSp6iLovz%2FdOXfBm%2BXF0mR0VGoArqgDxs3RuVEYtUiyYGV4NGs5IoCp46p%2Bg6r4PwZx1sGU8%2BgOGkqHZqgBMESdxrB4LH%2Ba4f79P6fjQHcu68Ug%2B9vASb78vCw3iY%2BnTZhtClq38mLgn1Rd1AEB539m4nx33wDD8g6PUBjqkAQcy%2F%2Bqhx7PmSjQFKxjM8zjdxcYyKwQ%2BirYq4BDf1V%2F92Rm8JVBXtLtOD5eepnvfDnV32dQoMcehWOdgXo6OpUnK61zuxBF7ZtH4VeShps3inOiMNX1kNpNgMyjSs9AVuVOMn7z%2BTOevGvTC658HuZfzkXM4JEAhfsn%2BgnSOmY4ndXlA8VLjvCvVBdupHHZDGKJ587V5zFFvS%2BaDe2cyWwLUEU0T&X-Amz-Signature=c998f969083473433fce0e373475d97154155673f259ed5ead1b68a0caed65d9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- As the **Update email** button is only displayed when you access the `/my-account` page in an authenticated state, we can use the presence or absence of
this button to determine whether we've successfully brute-forced the
cookie. On the **Settings** tab, add a grep match rule to flag any responses containing the string `Update email`. Start the attack.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/438df8f5-9407-4de1-82b5-5558ec74f5ec/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46645TZ2APV%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221728Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID7%2BXN3%2BNqHDKkQpZTw6XNuJrNE49%2F8U3wrpfkjB4ugMAiAo5fTeNqU%2FtKpHTOlgmQHzTc4FG7MY5M8D0zxm35R1jCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM7f3gnwXfCz1FroRyKtwDdzzuFSzxClgpjEud62JUry%2FweZrX6c5BT70Ve7yNiCLnVOj%2Bm2RMN2cjqhcUixCBerE1HkLX7%2FH5bN44ir814EtnMTLKj%2BQHuXY0YHy2M4v9QWXLGPDxTra1P8emBFPupEabm22J556NYLJAtqMtq2Ppr95RufjpaEGWeBcoz3DBCu2cfdR%2BbFCzySrOs5tvX2IAmkV2Fx4RyQ2CHCH8QJ%2B2RBbKLM26un%2BVg8uUKL%2F6bzaNcprFlc6pQjLA2mZ8jgxG1slhTQsLneTLSKBuKjijbaaHsuKh16ZztsG8YJfF3ghLbpX356lfr6WYvWfjBAl81nPd6K19erKbJfSgdOFseek203aRoquEtexYz%2FqIUOj7637RjTSX0Wh71V664jdF%2Fc1ebjg4wiXOLDailevFfLaccHefbp3bvQOX1aSQn7LUat68n2OL33%2FVuMNlB%2B5dCrAe4pcvc70iTEz0DlfRuFLsdQhL5WLTiNjd6czWWgm9A5IktJPd6B82Z48NWooupSWuRNhJRGyjmczUfXjsFsi5hclyBfgRR5okno2yaJoVUM1%2BQGSiPpjOWmKamZ1EroZh%2FSstWIVtygNmnINFBA9RQwIojarQ36XOECranYbvgkvo1VVc9KQw8YSj1AY6pgGO9QvaCIzRkuZq%2FZpcmQGvUj97pnr6umFmgoKQ7cA%2BAjZUidYSAx9awzGCtKaoZVVnu4HBeQrfTwSMlmtsoxO0vkQAv8e1%2F8pQdKBAcRHnwUIcb14wxQ4lY44ajI8G1Tj1T2Qw9HY%2BgX2pniErgu8SySkVHUhvefRH8ONZKDv8WyNKEQUaoYub%2BAeYlzpGUOHPO8yHq1APDDZekjsCz15LUjQ0c6dD&X-Amz-Signature=e0806e02f535bbc5957be8ebec84541dc038ffbe364e8e5a154fc904d0c38557&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- Notice that the generated payload was used to
successfully load your own account page. This confirms that the payload
processing rules work as expected and you were able to construct a valid cookie for your own account.
- Make the following adjustments and then repeat this attack:
  - Remove your own password from the payload list and add the list of [candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords) instead.
  - Change the **Add prefix** rule to add `carlos:` instead of `wiener:`.
- When the attack is finished, the lab will be
solved. Notice that only one request returned a response containing `Update email`. The payload from this request is the valid `stay-logged-in` cookie for Carlos's account.