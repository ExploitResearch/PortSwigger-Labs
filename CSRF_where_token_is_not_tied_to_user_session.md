# CSRF where token is not tied to user session

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

Inspect the form and notice that when we refresh the page (ie: on each request of the`/my-account`) each time csrf token gets change even within a session

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e95bd7b7-9a3c-43e3-adad-9e0927b5aa0f/2024-02-14_15-36.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666PUS5UW3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204625Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHDLjR5gGGs0CDXPWWLfMKM%2FbNfZVb41FgjZbdRtPNu2AiEA%2Foozvthj%2ByibDEz7cdir3jZOYLqWSvZypANSNbCZOvcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDD73QMC8yKaHRZaSVircA%2FdcfhHj0hyHoczh6KVVjhvNdvNNUMETSpx22qrGg9BHld9t8akj6kPw1wTzwBk5UUFLMyQBA2%2FCYi%2FGrYFC3ea9MohPWkmVt204WDTsNXJf2T8QA%2BzMz7mZbPdwkEkf5DxP%2F92apBLKY5KI0KuzXrbtdhs9%2FDBylhpCTN87K9%2F418qNg9ZSKX8CZtJEvalv%2FryOqTLahwgmz3NJuiVt3jxS75%2FsNiWD0ZuJME9Wb2dgj7WGqYfkQt9Es4AbPJ0f4zEQkB%2B8b%2F1JEJe6%2B0%2FieN4cas8X6KcDb0KSLNqbsombL1%2BkBZmdFOO8NKFqZgMQZfEixZw%2F6fLQ7BcOCY5SFuiukcaqTznXeIO9QUuzXvpQ0BkYICHqJKPLwaSnOU1eatC6GbF5dAlhndBx%2BI36YxAp0WTBxzwM1bhOKuZIgQEJYSCVrlLdm%2FJZOel6rgRjNHY1N3wbQkkejiWR%2BhIK15RK2iU5QGhyXHjUi%2Bkcag%2FrWN7KvJupFnFGDB7Ix97c64fWCKVx7OZk6RQHR%2F6KT1OprVwi67Mbaf%2FM92UavMJH2qMWtQGshj59tWVz6pFJBAePPTsL%2BEsnnPRIMmqNfej04sGx1zUqI%2BwvbGunFHgV3tomRh8cY6Xah%2F2fMJLGotQGOqUBKTpOymsUhz46esYtnlHUlCa1u799GxakVucdOoyoBwpb5g9MYaDyhTv%2FMdTUepKKy6WfzV2IviN7WSzGvKw4i%2BC%2BwCOC14EtNSwJ1hSkrq%2Fdb1jp%2FaT6Z4iZsj8CAanbFcJdcpWg9fZrWbT2zc%2FJATZZdmAUS0MZ4CUY3GkY9F3QNcFY4%2BVz0eNcsWnb6EVFr1CpHzkq1kkScg20KDEqNhH2XwWV&X-Amz-Signature=0eb6d253cd60d9a13d53016e0ff81d815b3faf0e000998fd644e353c019416d3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Check whether the tokens are bound to the sessions. **

I reload the `/my-account` page a few times, logout and login again (all as `wiener`).

Now I use Repeater to take one of my old email change requests, copy the new session data from the fresh login inside and a CSRF-token from before the logout:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/12_cross_site_request_forgery_CSRF/CSRF_where_token_is_not_tied_to_user_session/img/change_email_old_token.png)

And the email change goes through. This means that the tokens are not bound to the current session, which is a serious flaw.

**The next step is to find out whether the tokens are bound to the user.**

Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use user **`wiener`** CSRF token in user **`carlos`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa9acce6-b9c9-4d08-95f5-8352bc22430e/2024-02-14_17-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666PUS5UW3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204625Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHDLjR5gGGs0CDXPWWLfMKM%2FbNfZVb41FgjZbdRtPNu2AiEA%2Foozvthj%2ByibDEz7cdir3jZOYLqWSvZypANSNbCZOvcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDD73QMC8yKaHRZaSVircA%2FdcfhHj0hyHoczh6KVVjhvNdvNNUMETSpx22qrGg9BHld9t8akj6kPw1wTzwBk5UUFLMyQBA2%2FCYi%2FGrYFC3ea9MohPWkmVt204WDTsNXJf2T8QA%2BzMz7mZbPdwkEkf5DxP%2F92apBLKY5KI0KuzXrbtdhs9%2FDBylhpCTN87K9%2F418qNg9ZSKX8CZtJEvalv%2FryOqTLahwgmz3NJuiVt3jxS75%2FsNiWD0ZuJME9Wb2dgj7WGqYfkQt9Es4AbPJ0f4zEQkB%2B8b%2F1JEJe6%2B0%2FieN4cas8X6KcDb0KSLNqbsombL1%2BkBZmdFOO8NKFqZgMQZfEixZw%2F6fLQ7BcOCY5SFuiukcaqTznXeIO9QUuzXvpQ0BkYICHqJKPLwaSnOU1eatC6GbF5dAlhndBx%2BI36YxAp0WTBxzwM1bhOKuZIgQEJYSCVrlLdm%2FJZOel6rgRjNHY1N3wbQkkejiWR%2BhIK15RK2iU5QGhyXHjUi%2Bkcag%2FrWN7KvJupFnFGDB7Ix97c64fWCKVx7OZk6RQHR%2F6KT1OprVwi67Mbaf%2FM92UavMJH2qMWtQGshj59tWVz6pFJBAePPTsL%2BEsnnPRIMmqNfej04sGx1zUqI%2BwvbGunFHgV3tomRh8cY6Xah%2F2fMJLGotQGOqUBKTpOymsUhz46esYtnlHUlCa1u799GxakVucdOoyoBwpb5g9MYaDyhTv%2FMdTUepKKy6WfzV2IviN7WSzGvKw4i%2BC%2BwCOC14EtNSwJ1hSkrq%2Fdb1jp%2FaT6Z4iZsj8CAanbFcJdcpWg9fZrWbT2zc%2FJATZZdmAUS0MZ4CUY3GkY9F3QNcFY4%2BVz0eNcsWnb6EVFr1CpHzkq1kkScg20KDEqNhH2XwWV&X-Amz-Signature=b9d88230bfba0bef53061d16ec32e75927c6c3e1a72c2fb863c3210d1ea81c3c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The request is accepted and carlos email get changed

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/41f8f42a-fe43-433c-8bfd-4ac1a5ced607/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666PUS5UW3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204625Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHDLjR5gGGs0CDXPWWLfMKM%2FbNfZVb41FgjZbdRtPNu2AiEA%2Foozvthj%2ByibDEz7cdir3jZOYLqWSvZypANSNbCZOvcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDD73QMC8yKaHRZaSVircA%2FdcfhHj0hyHoczh6KVVjhvNdvNNUMETSpx22qrGg9BHld9t8akj6kPw1wTzwBk5UUFLMyQBA2%2FCYi%2FGrYFC3ea9MohPWkmVt204WDTsNXJf2T8QA%2BzMz7mZbPdwkEkf5DxP%2F92apBLKY5KI0KuzXrbtdhs9%2FDBylhpCTN87K9%2F418qNg9ZSKX8CZtJEvalv%2FryOqTLahwgmz3NJuiVt3jxS75%2FsNiWD0ZuJME9Wb2dgj7WGqYfkQt9Es4AbPJ0f4zEQkB%2B8b%2F1JEJe6%2B0%2FieN4cas8X6KcDb0KSLNqbsombL1%2BkBZmdFOO8NKFqZgMQZfEixZw%2F6fLQ7BcOCY5SFuiukcaqTznXeIO9QUuzXvpQ0BkYICHqJKPLwaSnOU1eatC6GbF5dAlhndBx%2BI36YxAp0WTBxzwM1bhOKuZIgQEJYSCVrlLdm%2FJZOel6rgRjNHY1N3wbQkkejiWR%2BhIK15RK2iU5QGhyXHjUi%2Bkcag%2FrWN7KvJupFnFGDB7Ix97c64fWCKVx7OZk6RQHR%2F6KT1OprVwi67Mbaf%2FM92UavMJH2qMWtQGshj59tWVz6pFJBAePPTsL%2BEsnnPRIMmqNfej04sGx1zUqI%2BwvbGunFHgV3tomRh8cY6Xah%2F2fMJLGotQGOqUBKTpOymsUhz46esYtnlHUlCa1u799GxakVucdOoyoBwpb5g9MYaDyhTv%2FMdTUepKKy6WfzV2IviN7WSzGvKw4i%2BC%2BwCOC14EtNSwJ1hSkrq%2Fdb1jp%2FaT6Z4iZsj8CAanbFcJdcpWg9fZrWbT2zc%2FJATZZdmAUS0MZ4CUY3GkY9F3QNcFY4%2BVz0eNcsWnb6EVFr1CpHzkq1kkScg20KDEqNhH2XwWV&X-Amz-Signature=004267a5d26935f8564ded71c68733b485b1a7953644dd5ac6117e6cd3cf9b72&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
