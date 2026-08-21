# CSRF with broken Referer validation

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QBEDU256%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGP759DTxJ%2FL7pbi1V7DRsvmadSwpIMqfgXYpLjpX6InAiBUBUpWl%2FgShwbFkQMyVwAWIHeKEVYKIJERpdrADEY6HSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOEw%2BpVW8TB%2B6sxMbKtwD11eH3FLX0kXnJMzF57HLQwFVPh1%2BclgfHzAt%2FpZq6QcZBAfthIJK6du5ZcwMsMZEMwzpi8AbrMFKmkPq6i4DfOfGDu5SmYo5Hyw3gnjlkJ3wC7ivxj537FLObJD%2BKxIogGMcSVDJDH%2FH6JkzxcQmBUNaVjh0aVq29gry7mVVEilYvAX3ZF0izFPdqE8XzkqELugIcLIfBqZQsanU7XXUzlNZe7Ilj4drjS0xA5R9zv20MkNMHALVGAqPQFNgs1ihS3CD2vPZOBSQs49zEVmWLVq5UxTbdp%2FJuYcqaaZyvDzZrLBxQZLhtReNsNQBM5KLPHrSrIg9cpo%2F%2Bc4RO8WWgVBY3OU%2F3Tfth73komRRAHj6VUXh5hUIVyTy%2FHkojYAAhjUvdx%2FAsOGnMaxskvyqk3XW1I8wlli4kTgz7YjGkmzOaUtBIGCBo8SvlmLDvFwBjFATWPn%2B3ELOZOZajJu04drU0luEy%2BSU%2FlPBFFMqRzAt%2BrtMF8Be%2BNz58GuoC9TdrDrmg%2BQ1Wl0D5UteiwltrQeu%2Fohg0IYLOROW1OokYMb0GejOW%2BdS27m9sSRivlj1UET%2BM9ZsHVZRSjLeVDG5IbMbcSnJbHlHmbibsRQRzK36lSzE7%2BlFvt%2FWzWcw5sai1AY6pgHvbVIHh1I7vu6mP2Sf5PGEZ2AUaxxkYdkFMCYhicYcswgNbTARTVqKnEqSdIlDjp9uEP7sKnQfAQmQJWcBNeGSGnefiL493tk8FDomJB67QDs4xj8LILltSoKwrsZhOXp5XQvZa22mULZ%2FpblPAwLt880zOz3nBEfGzTYSRhT8JKTMprBuz8ynqJ7yIISxhhn5pj1aq1iLNnXS91shAKsR%2F54aXPFs&X-Amz-Signature=3bd1bdc1426ba3e45dea0fa74eda056d283e943155b56702bcd0abce8d36ca3c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. v.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QBEDU256%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGP759DTxJ%2FL7pbi1V7DRsvmadSwpIMqfgXYpLjpX6InAiBUBUpWl%2FgShwbFkQMyVwAWIHeKEVYKIJERpdrADEY6HSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOEw%2BpVW8TB%2B6sxMbKtwD11eH3FLX0kXnJMzF57HLQwFVPh1%2BclgfHzAt%2FpZq6QcZBAfthIJK6du5ZcwMsMZEMwzpi8AbrMFKmkPq6i4DfOfGDu5SmYo5Hyw3gnjlkJ3wC7ivxj537FLObJD%2BKxIogGMcSVDJDH%2FH6JkzxcQmBUNaVjh0aVq29gry7mVVEilYvAX3ZF0izFPdqE8XzkqELugIcLIfBqZQsanU7XXUzlNZe7Ilj4drjS0xA5R9zv20MkNMHALVGAqPQFNgs1ihS3CD2vPZOBSQs49zEVmWLVq5UxTbdp%2FJuYcqaaZyvDzZrLBxQZLhtReNsNQBM5KLPHrSrIg9cpo%2F%2Bc4RO8WWgVBY3OU%2F3Tfth73komRRAHj6VUXh5hUIVyTy%2FHkojYAAhjUvdx%2FAsOGnMaxskvyqk3XW1I8wlli4kTgz7YjGkmzOaUtBIGCBo8SvlmLDvFwBjFATWPn%2B3ELOZOZajJu04drU0luEy%2BSU%2FlPBFFMqRzAt%2BrtMF8Be%2BNz58GuoC9TdrDrmg%2BQ1Wl0D5UteiwltrQeu%2Fohg0IYLOROW1OokYMb0GejOW%2BdS27m9sSRivlj1UET%2BM9ZsHVZRSjLeVDG5IbMbcSnJbHlHmbibsRQRzK36lSzE7%2BlFvt%2FWzWcw5sai1AY6pgHvbVIHh1I7vu6mP2Sf5PGEZ2AUaxxkYdkFMCYhicYcswgNbTARTVqKnEqSdIlDjp9uEP7sKnQfAQmQJWcBNeGSGnefiL493tk8FDomJB67QDs4xj8LILltSoKwrsZhOXp5XQvZa22mULZ%2FpblPAwLt880zOz3nBEfGzTYSRhT8JKTMprBuz8ynqJ7yIISxhhn5pj1aq1iLNnXS91shAKsR%2F54aXPFs&X-Amz-Signature=8f99dd4728c19caa5a13e0a9ba178ee04cea4becbaeeacb9a971a45f260517ab&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QBEDU256%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGP759DTxJ%2FL7pbi1V7DRsvmadSwpIMqfgXYpLjpX6InAiBUBUpWl%2FgShwbFkQMyVwAWIHeKEVYKIJERpdrADEY6HSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOEw%2BpVW8TB%2B6sxMbKtwD11eH3FLX0kXnJMzF57HLQwFVPh1%2BclgfHzAt%2FpZq6QcZBAfthIJK6du5ZcwMsMZEMwzpi8AbrMFKmkPq6i4DfOfGDu5SmYo5Hyw3gnjlkJ3wC7ivxj537FLObJD%2BKxIogGMcSVDJDH%2FH6JkzxcQmBUNaVjh0aVq29gry7mVVEilYvAX3ZF0izFPdqE8XzkqELugIcLIfBqZQsanU7XXUzlNZe7Ilj4drjS0xA5R9zv20MkNMHALVGAqPQFNgs1ihS3CD2vPZOBSQs49zEVmWLVq5UxTbdp%2FJuYcqaaZyvDzZrLBxQZLhtReNsNQBM5KLPHrSrIg9cpo%2F%2Bc4RO8WWgVBY3OU%2F3Tfth73komRRAHj6VUXh5hUIVyTy%2FHkojYAAhjUvdx%2FAsOGnMaxskvyqk3XW1I8wlli4kTgz7YjGkmzOaUtBIGCBo8SvlmLDvFwBjFATWPn%2B3ELOZOZajJu04drU0luEy%2BSU%2FlPBFFMqRzAt%2BrtMF8Be%2BNz58GuoC9TdrDrmg%2BQ1Wl0D5UteiwltrQeu%2Fohg0IYLOROW1OokYMb0GejOW%2BdS27m9sSRivlj1UET%2BM9ZsHVZRSjLeVDG5IbMbcSnJbHlHmbibsRQRzK36lSzE7%2BlFvt%2FWzWcw5sai1AY6pgHvbVIHh1I7vu6mP2Sf5PGEZ2AUaxxkYdkFMCYhicYcswgNbTARTVqKnEqSdIlDjp9uEP7sKnQfAQmQJWcBNeGSGnefiL493tk8FDomJB67QDs4xj8LILltSoKwrsZhOXp5XQvZa22mULZ%2FpblPAwLt880zOz3nBEfGzTYSRhT8JKTMprBuz8ynqJ7yIISxhhn5pj1aq1iLNnXS91shAKsR%2F54aXPFs&X-Amz-Signature=3f67bf9a5c744f454b959463cea65b11f657970b92be55e14a9d5cc6e6d816a4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QBEDU256%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGP759DTxJ%2FL7pbi1V7DRsvmadSwpIMqfgXYpLjpX6InAiBUBUpWl%2FgShwbFkQMyVwAWIHeKEVYKIJERpdrADEY6HSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOEw%2BpVW8TB%2B6sxMbKtwD11eH3FLX0kXnJMzF57HLQwFVPh1%2BclgfHzAt%2FpZq6QcZBAfthIJK6du5ZcwMsMZEMwzpi8AbrMFKmkPq6i4DfOfGDu5SmYo5Hyw3gnjlkJ3wC7ivxj537FLObJD%2BKxIogGMcSVDJDH%2FH6JkzxcQmBUNaVjh0aVq29gry7mVVEilYvAX3ZF0izFPdqE8XzkqELugIcLIfBqZQsanU7XXUzlNZe7Ilj4drjS0xA5R9zv20MkNMHALVGAqPQFNgs1ihS3CD2vPZOBSQs49zEVmWLVq5UxTbdp%2FJuYcqaaZyvDzZrLBxQZLhtReNsNQBM5KLPHrSrIg9cpo%2F%2Bc4RO8WWgVBY3OU%2F3Tfth73komRRAHj6VUXh5hUIVyTy%2FHkojYAAhjUvdx%2FAsOGnMaxskvyqk3XW1I8wlli4kTgz7YjGkmzOaUtBIGCBo8SvlmLDvFwBjFATWPn%2B3ELOZOZajJu04drU0luEy%2BSU%2FlPBFFMqRzAt%2BrtMF8Be%2BNz58GuoC9TdrDrmg%2BQ1Wl0D5UteiwltrQeu%2Fohg0IYLOROW1OokYMb0GejOW%2BdS27m9sSRivlj1UET%2BM9ZsHVZRSjLeVDG5IbMbcSnJbHlHmbibsRQRzK36lSzE7%2BlFvt%2FWzWcw5sai1AY6pgHvbVIHh1I7vu6mP2Sf5PGEZ2AUaxxkYdkFMCYhicYcswgNbTARTVqKnEqSdIlDjp9uEP7sKnQfAQmQJWcBNeGSGnefiL493tk8FDomJB67QDs4xj8LILltSoKwrsZhOXp5XQvZa22mULZ%2FpblPAwLt880zOz3nBEfGzTYSRhT8JKTMprBuz8ynqJ7yIISxhhn5pj1aq1iLNnXS91shAKsR%2F54aXPFs&X-Amz-Signature=45b9c48358965c62ad2b8800e6e56613c7799a098cb4f43b597cd0ef196e18a8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Since the `Referer` HTTP header can be fully controlled by the attacker, we can bypass this check!

send this request into Repeater 

> 💡 Testing Referer header for CSRF attacks:

  1. Remove the Referer header
  1. Check which portion of the referrer header is the application validating
1. Remove the Referer header
It still gives the same error "Invalid referer header”

1. Check which portion of the referrer header is the application validating
Copy the original domain of your lab instance and append it to the Referer header in the form of a query string. 

The website seems to accept any Referer header as long as it contains the expected domain somewhere in the string. 

> 💡 **According the **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState)**, we can use a JavaScript function called **`history.pushState()`**:**

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-12/images/Pasted%20image%2020221215054430.png)

To bypass that check, we can add the `history.pushState()` function in our exploit:

This will cause the `Referer` header in the generated request to contain the URL of the target site in the query string.

However, this still couldn’t work, as many browsers now strip the query string from the Referer header by default as a security measure.

**To bypass that, we can just add a new **`<meta>`** tag to override that behavior and ensure that the full URL is included in the request:**

> 💡 Fortunately, the documentation regarding referrer-policy on [mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy) shows the solution:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/12_cross_site_request_forgery_CSRF/CSRF_with_broken_Referer_validation/img/referrer_policy_docu.png)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b5868926-f66b-4b83-ab9f-7695e5f2d4bb/2024-02-27_17-27.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QBEDU256%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGP759DTxJ%2FL7pbi1V7DRsvmadSwpIMqfgXYpLjpX6InAiBUBUpWl%2FgShwbFkQMyVwAWIHeKEVYKIJERpdrADEY6HSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOEw%2BpVW8TB%2B6sxMbKtwD11eH3FLX0kXnJMzF57HLQwFVPh1%2BclgfHzAt%2FpZq6QcZBAfthIJK6du5ZcwMsMZEMwzpi8AbrMFKmkPq6i4DfOfGDu5SmYo5Hyw3gnjlkJ3wC7ivxj537FLObJD%2BKxIogGMcSVDJDH%2FH6JkzxcQmBUNaVjh0aVq29gry7mVVEilYvAX3ZF0izFPdqE8XzkqELugIcLIfBqZQsanU7XXUzlNZe7Ilj4drjS0xA5R9zv20MkNMHALVGAqPQFNgs1ihS3CD2vPZOBSQs49zEVmWLVq5UxTbdp%2FJuYcqaaZyvDzZrLBxQZLhtReNsNQBM5KLPHrSrIg9cpo%2F%2Bc4RO8WWgVBY3OU%2F3Tfth73komRRAHj6VUXh5hUIVyTy%2FHkojYAAhjUvdx%2FAsOGnMaxskvyqk3XW1I8wlli4kTgz7YjGkmzOaUtBIGCBo8SvlmLDvFwBjFATWPn%2B3ELOZOZajJu04drU0luEy%2BSU%2FlPBFFMqRzAt%2BrtMF8Be%2BNz58GuoC9TdrDrmg%2BQ1Wl0D5UteiwltrQeu%2Fohg0IYLOROW1OokYMb0GejOW%2BdS27m9sSRivlj1UET%2BM9ZsHVZRSjLeVDG5IbMbcSnJbHlHmbibsRQRzK36lSzE7%2BlFvt%2FWzWcw5sai1AY6pgHvbVIHh1I7vu6mP2Sf5PGEZ2AUaxxkYdkFMCYhicYcswgNbTARTVqKnEqSdIlDjp9uEP7sKnQfAQmQJWcBNeGSGnefiL493tk8FDomJB67QDs4xj8LILltSoKwrsZhOXp5XQvZa22mULZ%2FpblPAwLt880zOz3nBEfGzTYSRhT8JKTMprBuz8ynqJ7yIISxhhn5pj1aq1iLNnXS91shAKsR%2F54aXPFs&X-Amz-Signature=b701740c9128a49a19fc1705a1fe5fb6bd3e73646afc936abe284f891a6f4dd9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <head>
        <meta name="referrer" content="unsafe-url">
    </head>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0ab4004803380574938c5dbf00e200fa.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/?0ab4004803380574938c5dbf00e200fa.web-security-academy.net/my-account');
      document.forms[0].submit();
    </script>
  </body>
</html>

```

