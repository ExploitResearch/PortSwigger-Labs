# CSRF where token is not tied to user session

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

Inspect the form and notice that when we refresh the page (ie: on each request of the`/my-account`) each time csrf token gets change even within a session

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e95bd7b7-9a3c-43e3-adad-9e0927b5aa0f/2024-02-14_15-36.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VR4D3BY3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210324Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAGH79ctq3s%2Fb5FlIO4sop%2FpEoltFLRKWgEcxstRC%2BmTAiBcW8c9UJrGcaRiJoLgWGYiWRM0cSzTmvRYw39kfv0VKCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMIhqgg93nzfJGmMTKKtwDgk2spTaulBZCYLfPQ9oihHzwieHPcoCiCm9RQB2tHeI5IeiR3DulN3J%2BaFqQ1k%2BA%2BsA9QJI0CAM26gFjX%2F1i0HhGenXmHpHHB1dhosBEUiiv1lvYd1GlBKif3xuDU4i1H3HQIbi2DVu6AtHQLq%2FGC%2B2NV7Kcx%2BD5aP8TjhYZhzIV28cqpdMM7KKRvhlAjLZbAf5taSOIP%2B79F2%2BHnybCVGIQ2MEtloZ3Ve2JMyf6XIoox6NSFxfRm9PX8QASvvgcvpb1KU6rN88%2BLkQjpt8n0LL16NKCbSuf4%2BAFb%2B%2Bp21rDx%2BcjlPLsnRcJUZk51NytkxCxtVJzNZlvT6tfjbWvNYMypdOcLf3tBOGWabFcwjf0zAZefDdvge9L%2B4HgP1R%2BwLmzrI%2Fw79ttcOdQJbK2057fCK%2FbCsE0jOISXRWIN14t9np1my21mYKChQiFpyZKJH3XIUl6OoYl5ibCZ2WrNN%2Fr47Np05erFxieACSjKqCvQZ9cJ%2F3Pk9EUloVID4ScqLhQZOgK3nxyIjWHRZ39RXbn2H2lk9XQtzeB1cnFJ5sFOf%2B5%2Bp6W%2FrXtG64rE%2FIborZSLXnvtQCOxu1SZsUHCwY8PhaTIbCAQQ13J2UeWcP2Mnl2ce1woK837Tswx8mi1AY6pgFR7%2F%2FCwM8oGyb7FcgFw2KdsKj6AxoBNYyDoDk8seKqie3AprZdxghHWas8y6NZhOM3%2FB%2BNY%2Bj0yvy4N0INHFywwY80s%2Fo4rsT9TnO0EumnBi0WTAdyVCMnNPSnavhVuGciUGcg3blqGk9jM8zFLLwjIZc0NmLM%2FFdZCyn0bdATra%2FdoFaAmnCUw9rY6dTxzkJbVYAx%2BzC2UlSkcGsLXAzjHFMkAqXk&X-Amz-Signature=79c126e7992b30488468aa727644165e028ad4eba1de0c7e382a71a65e781786&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Check whether the tokens are bound to the sessions. **

I reload the `/my-account` page a few times, logout and login again (all as `wiener`).

Now I use Repeater to take one of my old email change requests, copy the new session data from the fresh login inside and a CSRF-token from before the logout:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/12_cross_site_request_forgery_CSRF/CSRF_where_token_is_not_tied_to_user_session/img/change_email_old_token.png)

And the email change goes through. This means that the tokens are not bound to the current session, which is a serious flaw.

**The next step is to find out whether the tokens are bound to the user.**

Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use user **`wiener`** CSRF token in user **`carlos`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa9acce6-b9c9-4d08-95f5-8352bc22430e/2024-02-14_17-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VR4D3BY3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210324Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAGH79ctq3s%2Fb5FlIO4sop%2FpEoltFLRKWgEcxstRC%2BmTAiBcW8c9UJrGcaRiJoLgWGYiWRM0cSzTmvRYw39kfv0VKCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMIhqgg93nzfJGmMTKKtwDgk2spTaulBZCYLfPQ9oihHzwieHPcoCiCm9RQB2tHeI5IeiR3DulN3J%2BaFqQ1k%2BA%2BsA9QJI0CAM26gFjX%2F1i0HhGenXmHpHHB1dhosBEUiiv1lvYd1GlBKif3xuDU4i1H3HQIbi2DVu6AtHQLq%2FGC%2B2NV7Kcx%2BD5aP8TjhYZhzIV28cqpdMM7KKRvhlAjLZbAf5taSOIP%2B79F2%2BHnybCVGIQ2MEtloZ3Ve2JMyf6XIoox6NSFxfRm9PX8QASvvgcvpb1KU6rN88%2BLkQjpt8n0LL16NKCbSuf4%2BAFb%2B%2Bp21rDx%2BcjlPLsnRcJUZk51NytkxCxtVJzNZlvT6tfjbWvNYMypdOcLf3tBOGWabFcwjf0zAZefDdvge9L%2B4HgP1R%2BwLmzrI%2Fw79ttcOdQJbK2057fCK%2FbCsE0jOISXRWIN14t9np1my21mYKChQiFpyZKJH3XIUl6OoYl5ibCZ2WrNN%2Fr47Np05erFxieACSjKqCvQZ9cJ%2F3Pk9EUloVID4ScqLhQZOgK3nxyIjWHRZ39RXbn2H2lk9XQtzeB1cnFJ5sFOf%2B5%2Bp6W%2FrXtG64rE%2FIborZSLXnvtQCOxu1SZsUHCwY8PhaTIbCAQQ13J2UeWcP2Mnl2ce1woK837Tswx8mi1AY6pgFR7%2F%2FCwM8oGyb7FcgFw2KdsKj6AxoBNYyDoDk8seKqie3AprZdxghHWas8y6NZhOM3%2FB%2BNY%2Bj0yvy4N0INHFywwY80s%2Fo4rsT9TnO0EumnBi0WTAdyVCMnNPSnavhVuGciUGcg3blqGk9jM8zFLLwjIZc0NmLM%2FFdZCyn0bdATra%2FdoFaAmnCUw9rY6dTxzkJbVYAx%2BzC2UlSkcGsLXAzjHFMkAqXk&X-Amz-Signature=db40361889aa53d76553579a64e31c7ddab32bdd0fea8302c669abb23dd13308&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The request is accepted and carlos email get changed

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/41f8f42a-fe43-433c-8bfd-4ac1a5ced607/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VR4D3BY3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210324Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAGH79ctq3s%2Fb5FlIO4sop%2FpEoltFLRKWgEcxstRC%2BmTAiBcW8c9UJrGcaRiJoLgWGYiWRM0cSzTmvRYw39kfv0VKCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMIhqgg93nzfJGmMTKKtwDgk2spTaulBZCYLfPQ9oihHzwieHPcoCiCm9RQB2tHeI5IeiR3DulN3J%2BaFqQ1k%2BA%2BsA9QJI0CAM26gFjX%2F1i0HhGenXmHpHHB1dhosBEUiiv1lvYd1GlBKif3xuDU4i1H3HQIbi2DVu6AtHQLq%2FGC%2B2NV7Kcx%2BD5aP8TjhYZhzIV28cqpdMM7KKRvhlAjLZbAf5taSOIP%2B79F2%2BHnybCVGIQ2MEtloZ3Ve2JMyf6XIoox6NSFxfRm9PX8QASvvgcvpb1KU6rN88%2BLkQjpt8n0LL16NKCbSuf4%2BAFb%2B%2Bp21rDx%2BcjlPLsnRcJUZk51NytkxCxtVJzNZlvT6tfjbWvNYMypdOcLf3tBOGWabFcwjf0zAZefDdvge9L%2B4HgP1R%2BwLmzrI%2Fw79ttcOdQJbK2057fCK%2FbCsE0jOISXRWIN14t9np1my21mYKChQiFpyZKJH3XIUl6OoYl5ibCZ2WrNN%2Fr47Np05erFxieACSjKqCvQZ9cJ%2F3Pk9EUloVID4ScqLhQZOgK3nxyIjWHRZ39RXbn2H2lk9XQtzeB1cnFJ5sFOf%2B5%2Bp6W%2FrXtG64rE%2FIborZSLXnvtQCOxu1SZsUHCwY8PhaTIbCAQQ13J2UeWcP2Mnl2ce1woK837Tswx8mi1AY6pgFR7%2F%2FCwM8oGyb7FcgFw2KdsKj6AxoBNYyDoDk8seKqie3AprZdxghHWas8y6NZhOM3%2FB%2BNY%2Bj0yvy4N0INHFywwY80s%2Fo4rsT9TnO0EumnBi0WTAdyVCMnNPSnavhVuGciUGcg3blqGk9jM8zFLLwjIZc0NmLM%2FFdZCyn0bdATra%2FdoFaAmnCUw9rY6dTxzkJbVYAx%2BzC2UlSkcGsLXAzjHFMkAqXk&X-Amz-Signature=491a8a062c4de5bca3c9c52259319b0240ed6776de77ddff45e9a9b9ae8e3b7f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
