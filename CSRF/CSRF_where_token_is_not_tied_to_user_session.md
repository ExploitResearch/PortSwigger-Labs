# CSRF where token is not tied to user session

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

Inspect the form and notice that when we refresh the page (ie: on each request of the`/my-account`) each time csrf token gets change even within a session

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e95bd7b7-9a3c-43e3-adad-9e0927b5aa0f/2024-02-14_15-36.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664QNPYBJQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215449Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGem4eO3qxW22nPglzxS%2BiZho0No42Gn6MMH4TJ71YvBAiEAvANJx6fSIW3b%2BnYm%2FjpWMb0euck9o8zo%2FB4XE0mRH1kqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEzgLDSZVYQ3UmYHPCrcA1a4cVKP1MkSDloHzthdfuot7TZIzZpQxxGoWuMCjWOOWAFcp%2BYwfqSym5%2BAOedaznR%2BZD77Mx9z2yxg%2FLJReQQ0s1KK9sV0m0bNvqsH3bPt4R1Frzll6L3xgwhtS6Kb5PigRbq7qXPH5%2BXpaFi0CeC46sm8KFG6xz0kAb9cWnVeouCP%2BLP%2Fid7v74cXJI7HKbHfZiG%2BNWP3TIsE8TCrkg1TJsx7GyzK8IiLlxbfBCNuOEe02S0uSVwQv7TwLJ9FDSHuYui7r94EKUVTV7K2l18uQ7pkyY2NWSgTHpZJfLkhzzwKx1Nz7O21F2Y%2BayYf1H%2BZafXgTD7LKXo5elze5BkUBnJZgX1PECsLb5kb6V9stIIn0yyyDUf9BhsvRNrOwFzgoLDB4gwOLS3wTOelXldfJhNkGZG12oXHJS4NIimwq5JN81f49ssJSYxb9t3ftf189beApWSF6OGTnLQldgf8T1hTqSsc%2BOC8L82YwlihwjkJQy4cFvhR%2BSeG1FBfD5IgYAFQEZms3E4hJSFQfSEVnRrwR88eeyOhI8YvR5q6ttHwteo4bu5oP9hNmvSWWT1FZNCo1AeWZ%2BM922dRLnnis0ADnB7DNbjPX4vm9ei9mc6bM9JsE88mqxT5MLSEo9QGOqUBgrGrom1mlmqVcvQR1pulgbPhFfE%2FyyG5EHUqKYLaQvI4IIzVkbughy6DYKsyYpAarZk1tgiOYRfz2q0zbvbEw0rEG%2FeAe6EzUwX3oXEhK8kQfgi5aXH8tSJlsJtXthlx49aKIt8q6wy5V7v3AeQau4wxo1YuvLrhISvey4HHiIvDkmcdJzG0m3lHqAXvYTxJ9DvP9tBqm95gcySpZ0r8CnhgGyPm&X-Amz-Signature=30f10884f6e2fdcc99c0f7be9af3c60f7e55551d6084ed33b6f87027420806ac&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Check whether the tokens are bound to the sessions. **

I reload the `/my-account` page a few times, logout and login again (all as `wiener`).

Now I use Repeater to take one of my old email change requests, copy the new session data from the fresh login inside and a CSRF-token from before the logout:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/12_cross_site_request_forgery_CSRF/CSRF_where_token_is_not_tied_to_user_session/img/change_email_old_token.png)

And the email change goes through. This means that the tokens are not bound to the current session, which is a serious flaw.

**The next step is to find out whether the tokens are bound to the user.**

Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use user **`wiener`** CSRF token in user **`carlos`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa9acce6-b9c9-4d08-95f5-8352bc22430e/2024-02-14_17-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664QNPYBJQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215449Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGem4eO3qxW22nPglzxS%2BiZho0No42Gn6MMH4TJ71YvBAiEAvANJx6fSIW3b%2BnYm%2FjpWMb0euck9o8zo%2FB4XE0mRH1kqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEzgLDSZVYQ3UmYHPCrcA1a4cVKP1MkSDloHzthdfuot7TZIzZpQxxGoWuMCjWOOWAFcp%2BYwfqSym5%2BAOedaznR%2BZD77Mx9z2yxg%2FLJReQQ0s1KK9sV0m0bNvqsH3bPt4R1Frzll6L3xgwhtS6Kb5PigRbq7qXPH5%2BXpaFi0CeC46sm8KFG6xz0kAb9cWnVeouCP%2BLP%2Fid7v74cXJI7HKbHfZiG%2BNWP3TIsE8TCrkg1TJsx7GyzK8IiLlxbfBCNuOEe02S0uSVwQv7TwLJ9FDSHuYui7r94EKUVTV7K2l18uQ7pkyY2NWSgTHpZJfLkhzzwKx1Nz7O21F2Y%2BayYf1H%2BZafXgTD7LKXo5elze5BkUBnJZgX1PECsLb5kb6V9stIIn0yyyDUf9BhsvRNrOwFzgoLDB4gwOLS3wTOelXldfJhNkGZG12oXHJS4NIimwq5JN81f49ssJSYxb9t3ftf189beApWSF6OGTnLQldgf8T1hTqSsc%2BOC8L82YwlihwjkJQy4cFvhR%2BSeG1FBfD5IgYAFQEZms3E4hJSFQfSEVnRrwR88eeyOhI8YvR5q6ttHwteo4bu5oP9hNmvSWWT1FZNCo1AeWZ%2BM922dRLnnis0ADnB7DNbjPX4vm9ei9mc6bM9JsE88mqxT5MLSEo9QGOqUBgrGrom1mlmqVcvQR1pulgbPhFfE%2FyyG5EHUqKYLaQvI4IIzVkbughy6DYKsyYpAarZk1tgiOYRfz2q0zbvbEw0rEG%2FeAe6EzUwX3oXEhK8kQfgi5aXH8tSJlsJtXthlx49aKIt8q6wy5V7v3AeQau4wxo1YuvLrhISvey4HHiIvDkmcdJzG0m3lHqAXvYTxJ9DvP9tBqm95gcySpZ0r8CnhgGyPm&X-Amz-Signature=480f86655ec7297807767afa78446f5520fe38cabb271ffd93bb96a959dfc8ec&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The request is accepted and carlos email get changed

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/41f8f42a-fe43-433c-8bfd-4ac1a5ced607/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664QNPYBJQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215449Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGem4eO3qxW22nPglzxS%2BiZho0No42Gn6MMH4TJ71YvBAiEAvANJx6fSIW3b%2BnYm%2FjpWMb0euck9o8zo%2FB4XE0mRH1kqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEzgLDSZVYQ3UmYHPCrcA1a4cVKP1MkSDloHzthdfuot7TZIzZpQxxGoWuMCjWOOWAFcp%2BYwfqSym5%2BAOedaznR%2BZD77Mx9z2yxg%2FLJReQQ0s1KK9sV0m0bNvqsH3bPt4R1Frzll6L3xgwhtS6Kb5PigRbq7qXPH5%2BXpaFi0CeC46sm8KFG6xz0kAb9cWnVeouCP%2BLP%2Fid7v74cXJI7HKbHfZiG%2BNWP3TIsE8TCrkg1TJsx7GyzK8IiLlxbfBCNuOEe02S0uSVwQv7TwLJ9FDSHuYui7r94EKUVTV7K2l18uQ7pkyY2NWSgTHpZJfLkhzzwKx1Nz7O21F2Y%2BayYf1H%2BZafXgTD7LKXo5elze5BkUBnJZgX1PECsLb5kb6V9stIIn0yyyDUf9BhsvRNrOwFzgoLDB4gwOLS3wTOelXldfJhNkGZG12oXHJS4NIimwq5JN81f49ssJSYxb9t3ftf189beApWSF6OGTnLQldgf8T1hTqSsc%2BOC8L82YwlihwjkJQy4cFvhR%2BSeG1FBfD5IgYAFQEZms3E4hJSFQfSEVnRrwR88eeyOhI8YvR5q6ttHwteo4bu5oP9hNmvSWWT1FZNCo1AeWZ%2BM922dRLnnis0ADnB7DNbjPX4vm9ei9mc6bM9JsE88mqxT5MLSEo9QGOqUBgrGrom1mlmqVcvQR1pulgbPhFfE%2FyyG5EHUqKYLaQvI4IIzVkbughy6DYKsyYpAarZk1tgiOYRfz2q0zbvbEw0rEG%2FeAe6EzUwX3oXEhK8kQfgi5aXH8tSJlsJtXthlx49aKIt8q6wy5V7v3AeQau4wxo1YuvLrhISvey4HHiIvDkmcdJzG0m3lHqAXvYTxJ9DvP9tBqm95gcySpZ0r8CnhgGyPm&X-Amz-Signature=4be2a978a1e21211f0f44deca6e2a8460d3a277bcd6cc15baaf85f3d786c5783&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
