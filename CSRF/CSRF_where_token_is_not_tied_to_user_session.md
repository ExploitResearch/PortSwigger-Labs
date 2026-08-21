# CSRF where token is not tied to user session

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

Inspect the form and notice that when we refresh the page (ie: on each request of the`/my-account`) each time csrf token gets change even within a session

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e95bd7b7-9a3c-43e3-adad-9e0927b5aa0f/2024-02-14_15-36.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665VYZR6JC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221847Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCGv7KsDhoVB7OZRe6i8Xh1JmcOMY0QEXmI6srqKYLdqQIgMPovIOPlh4M8jTjmUe99zxOVWFv0dKTFdI9p%2B%2FBugfwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJ%2FveKdPVr6wc3sQYCrcA6xd4g2FNlfA5Pw8QGH69ASIN4UgapV9RJRHXvUjpLA8sDcjWgZ9gmiibNBBS7UeaXkRVXA4FOGo2VUWcGr%2FbuzaotuV%2BdyHaQWEU7Hz1ccaT5vYSvEwFeLx2z8rjudMjrNKoHcVeIab%2FAVGBNARBICG6E3OIQtzgMiUa1%2BfDfG4V%2BIh0gpapa%2BV5WLK%2FBn4gHochenSo8g4uma82SzYr6KPwzTVDQ6y5P3mVhLiQOV%2FZ0xwUAHYVnhozMQEWBCqjEFJL%2FYJ9%2BuWeWfuP0%2BPeNzQIlGEP51zZUBRbyCIRn1g10%2BxiPY6TqqQU5qp3%2Fjy%2FTiCpP4d6ZA1duUnXv4I0TzsBXLXPVt46FHJsVxJGzLobN2b3osV3Ff9%2BGqZ9JHQN98Qx%2F5rOAoCTJeC8vZ1ULOF191KkWgj1b11cCQVxIhNzpwK8UJwlMEuedxi0KQo7WVPdYBeC2su4rM65LEQ5i7maES449dXU8UP6TWTvf8wc6UkOrsUe3lGbMhtcEpqlE7lqOfoxUWIVFIAJajc88Bz2aYNUW74%2B%2BWz2R5vvU4wZ5WCeKs4Q3coX1s2AD%2FyrNbS5X%2FmtwSRV9uObQB6ezgB0wgiiWa5U2XXzHvS9HO63fJshV3GLv%2Bi9CKYMM6Fo9QGOqUB%2BF9MrSNS%2FA%2Bj7L%2BzxzjpynrF5ZPmwfAi2z3eJXRYsco9t5hj6LYiw6YacIbTTgBD0ZUD2X7UA7UGzN82%2BSjnREcoAGP%2FycnCEuLur1I7%2Bet93W%2BS5QNdddzfFm4Fth96Qm%2FPYgVP0A5KM9YwVHvFaO3qtf1tLFtvrCIGutnq1sPwczWt9ICkrHCOGBOwlbqRd4VXpPuO65yHb7t4HHiLTQOOOXTW&X-Amz-Signature=d96b574148080b6f9a479cb14036528744e057a4446b65aa324adbdebbb0278a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Check whether the tokens are bound to the sessions. **

I reload the `/my-account` page a few times, logout and login again (all as `wiener`).

Now I use Repeater to take one of my old email change requests, copy the new session data from the fresh login inside and a CSRF-token from before the logout:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/12_cross_site_request_forgery_CSRF/CSRF_where_token_is_not_tied_to_user_session/img/change_email_old_token.png)

And the email change goes through. This means that the tokens are not bound to the current session, which is a serious flaw.

**The next step is to find out whether the tokens are bound to the user.**

Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use user **`wiener`** CSRF token in user **`carlos`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa9acce6-b9c9-4d08-95f5-8352bc22430e/2024-02-14_17-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665VYZR6JC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221847Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCGv7KsDhoVB7OZRe6i8Xh1JmcOMY0QEXmI6srqKYLdqQIgMPovIOPlh4M8jTjmUe99zxOVWFv0dKTFdI9p%2B%2FBugfwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJ%2FveKdPVr6wc3sQYCrcA6xd4g2FNlfA5Pw8QGH69ASIN4UgapV9RJRHXvUjpLA8sDcjWgZ9gmiibNBBS7UeaXkRVXA4FOGo2VUWcGr%2FbuzaotuV%2BdyHaQWEU7Hz1ccaT5vYSvEwFeLx2z8rjudMjrNKoHcVeIab%2FAVGBNARBICG6E3OIQtzgMiUa1%2BfDfG4V%2BIh0gpapa%2BV5WLK%2FBn4gHochenSo8g4uma82SzYr6KPwzTVDQ6y5P3mVhLiQOV%2FZ0xwUAHYVnhozMQEWBCqjEFJL%2FYJ9%2BuWeWfuP0%2BPeNzQIlGEP51zZUBRbyCIRn1g10%2BxiPY6TqqQU5qp3%2Fjy%2FTiCpP4d6ZA1duUnXv4I0TzsBXLXPVt46FHJsVxJGzLobN2b3osV3Ff9%2BGqZ9JHQN98Qx%2F5rOAoCTJeC8vZ1ULOF191KkWgj1b11cCQVxIhNzpwK8UJwlMEuedxi0KQo7WVPdYBeC2su4rM65LEQ5i7maES449dXU8UP6TWTvf8wc6UkOrsUe3lGbMhtcEpqlE7lqOfoxUWIVFIAJajc88Bz2aYNUW74%2B%2BWz2R5vvU4wZ5WCeKs4Q3coX1s2AD%2FyrNbS5X%2FmtwSRV9uObQB6ezgB0wgiiWa5U2XXzHvS9HO63fJshV3GLv%2Bi9CKYMM6Fo9QGOqUB%2BF9MrSNS%2FA%2Bj7L%2BzxzjpynrF5ZPmwfAi2z3eJXRYsco9t5hj6LYiw6YacIbTTgBD0ZUD2X7UA7UGzN82%2BSjnREcoAGP%2FycnCEuLur1I7%2Bet93W%2BS5QNdddzfFm4Fth96Qm%2FPYgVP0A5KM9YwVHvFaO3qtf1tLFtvrCIGutnq1sPwczWt9ICkrHCOGBOwlbqRd4VXpPuO65yHb7t4HHiLTQOOOXTW&X-Amz-Signature=2f1f7abc4dc9f47872cb0af7b3cdedc5914a9d2b9550e993901c42adb6c87ecb&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The request is accepted and carlos email get changed

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/41f8f42a-fe43-433c-8bfd-4ac1a5ced607/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665VYZR6JC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221847Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCGv7KsDhoVB7OZRe6i8Xh1JmcOMY0QEXmI6srqKYLdqQIgMPovIOPlh4M8jTjmUe99zxOVWFv0dKTFdI9p%2B%2FBugfwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJ%2FveKdPVr6wc3sQYCrcA6xd4g2FNlfA5Pw8QGH69ASIN4UgapV9RJRHXvUjpLA8sDcjWgZ9gmiibNBBS7UeaXkRVXA4FOGo2VUWcGr%2FbuzaotuV%2BdyHaQWEU7Hz1ccaT5vYSvEwFeLx2z8rjudMjrNKoHcVeIab%2FAVGBNARBICG6E3OIQtzgMiUa1%2BfDfG4V%2BIh0gpapa%2BV5WLK%2FBn4gHochenSo8g4uma82SzYr6KPwzTVDQ6y5P3mVhLiQOV%2FZ0xwUAHYVnhozMQEWBCqjEFJL%2FYJ9%2BuWeWfuP0%2BPeNzQIlGEP51zZUBRbyCIRn1g10%2BxiPY6TqqQU5qp3%2Fjy%2FTiCpP4d6ZA1duUnXv4I0TzsBXLXPVt46FHJsVxJGzLobN2b3osV3Ff9%2BGqZ9JHQN98Qx%2F5rOAoCTJeC8vZ1ULOF191KkWgj1b11cCQVxIhNzpwK8UJwlMEuedxi0KQo7WVPdYBeC2su4rM65LEQ5i7maES449dXU8UP6TWTvf8wc6UkOrsUe3lGbMhtcEpqlE7lqOfoxUWIVFIAJajc88Bz2aYNUW74%2B%2BWz2R5vvU4wZ5WCeKs4Q3coX1s2AD%2FyrNbS5X%2FmtwSRV9uObQB6ezgB0wgiiWa5U2XXzHvS9HO63fJshV3GLv%2Bi9CKYMM6Fo9QGOqUB%2BF9MrSNS%2FA%2Bj7L%2BzxzjpynrF5ZPmwfAi2z3eJXRYsco9t5hj6LYiw6YacIbTTgBD0ZUD2X7UA7UGzN82%2BSjnREcoAGP%2FycnCEuLur1I7%2Bet93W%2BS5QNdddzfFm4Fth96Qm%2FPYgVP0A5KM9YwVHvFaO3qtf1tLFtvrCIGutnq1sPwczWt9ICkrHCOGBOwlbqRd4VXpPuO65yHb7t4HHiLTQOOOXTW&X-Amz-Signature=285e49d3c3379d537ed606bf9cf0edcfa27f8e3c21402c3c87054619376493f5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: csrf token is not tied to user session

Testing CSRF Tokens:

  1. Remove the CSRF token and see if application accepts request
  1. Change the request method from POST to GET
  1. See if csrf token is tied to user session

> 💡 Note that the CSRF tokens are single-use, so you'll need to include a fresh one.
we also need to use new email and can’t use email assigned to other users.

The next steps are easy:

- Prepare the HTML form for the email change
- Use one of the existing but not used CSRF-tokens
- Add an auto-submit feature

In Burp Suite Professional, right-click on the request, and from the context menu select Engagement tools / Generate CSRF PoC. Enable the option to include an auto-submit script and click "Regenerate".

Go to the exploit server, paste your exploit HTML into the "Body" section, and click "Store".

We can test it locally via the `View exploit` button

- Change the email address in your exploit so that it doesn't match your own or in use of other user and use new csrf token
- Store the exploit, then click "Deliver to victim" to solve the lab.
