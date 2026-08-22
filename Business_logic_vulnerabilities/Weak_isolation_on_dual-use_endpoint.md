# Weak isolation on dual-use endpoint

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

One thing that catches my eye is the password change functionality:

Why does it contain the username as an input field? I'd expect either the password to be changed for the logged-in user, `wiener`. In this case, the input field for the username would be unnecessary.

What happens if I use it and simply change the username to `administrator`?

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb5a0148-e37a-4709-9b8f-4255565d4c2e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZOT3M463%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222026Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFq3P6TDYNJbw%2F4CGyWXINj4ax3%2BPY0goSevVnqViJoRAiB5yMIPvFqHS47ipvoTjMc7rkdBa50mf3nF3rkhCLbw4iqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzKAC%2B5Zx5qjJ53BQKtwDHOMRJ7YWgljloz4LApOCbrhfD%2B%2F9uMcOod%2F3KDY5b6F4yAwrkUoZ6PZUCoj4y0tfDxIZ3do6L7zk2X%2Bin8zgEbTGczs8ipvmfEs7P%2FnmkU49WcThY54nlywlM4z8rrNG59qP%2BRAY2HH8RMvckAYjDEp69oyF0MSB0hzJhi5IHt5%2Fe8h3QWQDl9Y%2FH%2FhQuXAbo2pdVDpnG2y4G1spj%2BBBdlK7FR3BD1QkBIgmjgNfnhaTLOUl%2Fvuccb%2FBAs6YJXNngKog5Y1ofwLMlgdOs%2FQQ1zF8QDxxGj4sKrCdfeiMUTKvP0ApXbwbiuZXNGUWt3iVlAIeTCc9dpbQQmmHE2hDUh1mZPF37ymtFG%2B9i67ccsk9rqgtMOs1KC7y4XstwUhOC2swuFocfeuCkzLPXG4m5CbfEyMfsUTbxwzaq9D3FT2vaokpehCVVWqB9mT1kgt3pHzRfHnqrvE%2FU37rCV9X19WBGt30jZ2pK2iP7XLWz3ZXGSN%2BvuE4hxT21GDW8NgoeRvvT2b%2FhvSbInnqm6Jsu0ChUp2IHsbJGQ5vTsMXF9q1R9%2F5UPS5kbIqwMrA6ZRduST%2Fv05Ng3WUpDZAsrMfjv%2BrK8xhZ6st7i3rm4Yjx7MJFmWklODhPkAX0ZkwmYaj1AY6pgGskSJGblAxpt4iw%2FD4ABCr0be1EWq6M3GMRZM7ZHMMNnSfI0x3sycIpb%2FttXj3d8mBwA7GF1H4pAEKEOeotJXmzmhexyZ%2BWhpzn%2F5fyhnq6n5oBLVmo3Ehi%2BWWRWncy13Qg%2FY2w7JCnzTmuS35vp64ruEIe89u78Ll0xHSi7Y0FaEf22lJOFDEOxiEOfoUF7JWz%2FXamONgcvCkBPXgyxkjloJ9QttP&X-Amz-Signature=1af8d8d9ea311041d4eb34cfdf28d1dffa0ade2f1284224aee08a62aad5a9ccf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We get error Current password is incorrect:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e6e26397-57bd-4650-a628-543c7609a0a8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VUB7SRAY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222027Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDo6lvq0TawbDmaFgJcYqHEYFrijJX8RuxcofoRs8I8ywIgGXZse8pUPORyWBQLqhLzN8xYMCH%2F1po8G9QFsfOIjSgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJ41exZRl%2FkgLCr3PCrcA3Ns%2B%2FSFTkuSwu5AhzwmgFwV08W%2BMt7XCaxcxxtjPjpIVlalYjw1QQIHhlA7VyiT%2F8CkvWk1DP3hnUpCA%2F6MYBhFtClfLnxmcYl8bySwQBhqE46OO2ftxM3EGobuhkruUs13X4Gl9sqYbptb8m%2FSEijy%2BgOJ7CtRSuIfhS4pvNJFi%2F7MONBctM5W6uiRDphMs2yWw%2FXBXnAGoaHebA9omurlkfKxuAURutSasJMepbqufVfWefoWN4rzgcoUcIPDRHYxs9yZb7vWwQHjNOlwBN%2FsjoHP1%2BQp3IEuPPx7cpRgCusXw%2BXJySbZwqsQO%2FOY23n1Rc8IWY%2F0lHwzrqciLFWgkfQhJ96cj5R5WXphQAXNa%2BDYxIPuVrfSrRfc09pR8CwH6PG8Mz%2BMQWFvCXQf9Q7J7Pm%2FMr80HtPHGLD2Y4OCk6QTQJWg2zxaXTN712w5VjdmvOwArdza0na4Ir%2BkDmtQeQAp23IwD73wz%2BjCHQDtkpkzUrGFFTplxk3Xm0amI6NyqTSndTyWG8fUHQb%2BN3ut8qacl%2BGQA9lYYv1waAzFb%2BPlJGTTmyx2bmeVrXDrXeXur44wBXGhCy9WdjLXuAaFhxWtmkOhJzl2Jom4LzH439qlMhOtldRaStYiMKSFo9QGOqUBm4lcCP7oBIhcK7fXsNYG9seuE1EEcKadO2mwPA8pokQAgEiKRCn1ms%2BXzmOqcmLXtjzl725FOQkkhM4gOxZsqFiGtBnA3Hk0wxW6nv5qBIWgdY%2BeEplNfe5PXyjhJ0eRFqCMbc%2BPSmF4GDNuzPq6zJ7qzqz0ZtrcwchfoTGErBTPYVykRGP5dEJ2jdcGRBWIH4SMhcd0nkFOdJWDxeIQfW4Nbp0R&X-Amz-Signature=3892da3c3eaf4e841d2582cd60c0e9280d5f995e06f322c8d6093f4124a97f12&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From this result I can derive a few pieces of information:

1. The password change failed due to a wrong current password.
1. The password comparison was not performed with the password account that is logged in but with the password of the account set in `Username`
1. At the point the 'Update password' form was generated, the application did use the logged-in user again.

But at some point during the generation of the response, the application assumed that my username is `administrator`. This points to some weird logic behind the scenes that warrant further investigation.

To verify that no password was changed despite the error message, I attempt to log in with both `wiener` and `administrator` using the newly set password. It fails as expected.

### Analyzing the traffic

When we clicked the `Change password` button, **it send a POST request to **`/my-account/change-password`**, with parameter **`csrf`**, **`username`**, **`current-password`**, **`new-password-1`**, and **`new-password-2`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/81e66630-f649-477b-94d3-afd5f40c0120/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZOT3M463%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222026Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFq3P6TDYNJbw%2F4CGyWXINj4ax3%2BPY0goSevVnqViJoRAiB5yMIPvFqHS47ipvoTjMc7rkdBa50mf3nF3rkhCLbw4iqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzKAC%2B5Zx5qjJ53BQKtwDHOMRJ7YWgljloz4LApOCbrhfD%2B%2F9uMcOod%2F3KDY5b6F4yAwrkUoZ6PZUCoj4y0tfDxIZ3do6L7zk2X%2Bin8zgEbTGczs8ipvmfEs7P%2FnmkU49WcThY54nlywlM4z8rrNG59qP%2BRAY2HH8RMvckAYjDEp69oyF0MSB0hzJhi5IHt5%2Fe8h3QWQDl9Y%2FH%2FhQuXAbo2pdVDpnG2y4G1spj%2BBBdlK7FR3BD1QkBIgmjgNfnhaTLOUl%2Fvuccb%2FBAs6YJXNngKog5Y1ofwLMlgdOs%2FQQ1zF8QDxxGj4sKrCdfeiMUTKvP0ApXbwbiuZXNGUWt3iVlAIeTCc9dpbQQmmHE2hDUh1mZPF37ymtFG%2B9i67ccsk9rqgtMOs1KC7y4XstwUhOC2swuFocfeuCkzLPXG4m5CbfEyMfsUTbxwzaq9D3FT2vaokpehCVVWqB9mT1kgt3pHzRfHnqrvE%2FU37rCV9X19WBGt30jZ2pK2iP7XLWz3ZXGSN%2BvuE4hxT21GDW8NgoeRvvT2b%2FhvSbInnqm6Jsu0ChUp2IHsbJGQ5vTsMXF9q1R9%2F5UPS5kbIqwMrA6ZRduST%2Fv05Ng3WUpDZAsrMfjv%2BrK8xhZ6st7i3rm4Yjx7MJFmWklODhPkAX0ZkwmYaj1AY6pgGskSJGblAxpt4iw%2FD4ABCr0be1EWq6M3GMRZM7ZHMMNnSfI0x3sycIpb%2FttXj3d8mBwA7GF1H4pAEKEOeotJXmzmhexyZ%2BWhpzn%2F5fyhnq6n5oBLVmo3Ehi%2BWWRWncy13Qg%2FY2w7JCnzTmuS35vp64ruEIe89u78Ll0xHSi7Y0FaEf22lJOFDEOxiEOfoUF7JWz%2FXamONgcvCkBPXgyxkjloJ9QttP&X-Amz-Signature=18cc519e12f88938ea250d956fba446a967a0a97747c8050b00a373ef4dfdda0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

OK, so I have the csrf token, username and the three password parameters.

While the application generated the response, at the moment my username was embedded, I was the `administrator` user. I was also considered `administrator` while the current password was checked and the error message got inserted. As such, the password change failed as it was not the correct password for that user.

So what happens if I remove the current-password parameter from the form?

This depends on whether it always checks the current password on password change. If this is the case, then it will fail as well, as it should.

However, if the password check only occurs when the parameter is present, then it will be bad for the application but good for me.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2fc35871-6a2d-4cb6-92f8-1016672f0b1d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZOT3M463%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222026Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIFq3P6TDYNJbw%2F4CGyWXINj4ax3%2BPY0goSevVnqViJoRAiB5yMIPvFqHS47ipvoTjMc7rkdBa50mf3nF3rkhCLbw4iqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzKAC%2B5Zx5qjJ53BQKtwDHOMRJ7YWgljloz4LApOCbrhfD%2B%2F9uMcOod%2F3KDY5b6F4yAwrkUoZ6PZUCoj4y0tfDxIZ3do6L7zk2X%2Bin8zgEbTGczs8ipvmfEs7P%2FnmkU49WcThY54nlywlM4z8rrNG59qP%2BRAY2HH8RMvckAYjDEp69oyF0MSB0hzJhi5IHt5%2Fe8h3QWQDl9Y%2FH%2FhQuXAbo2pdVDpnG2y4G1spj%2BBBdlK7FR3BD1QkBIgmjgNfnhaTLOUl%2Fvuccb%2FBAs6YJXNngKog5Y1ofwLMlgdOs%2FQQ1zF8QDxxGj4sKrCdfeiMUTKvP0ApXbwbiuZXNGUWt3iVlAIeTCc9dpbQQmmHE2hDUh1mZPF37ymtFG%2B9i67ccsk9rqgtMOs1KC7y4XstwUhOC2swuFocfeuCkzLPXG4m5CbfEyMfsUTbxwzaq9D3FT2vaokpehCVVWqB9mT1kgt3pHzRfHnqrvE%2FU37rCV9X19WBGt30jZ2pK2iP7XLWz3ZXGSN%2BvuE4hxT21GDW8NgoeRvvT2b%2FhvSbInnqm6Jsu0ChUp2IHsbJGQ5vTsMXF9q1R9%2F5UPS5kbIqwMrA6ZRduST%2Fv05Ng3WUpDZAsrMfjv%2BrK8xhZ6st7i3rm4Yjx7MJFmWklODhPkAX0ZkwmYaj1AY6pgGskSJGblAxpt4iw%2FD4ABCr0be1EWq6M3GMRZM7ZHMMNnSfI0x3sycIpb%2FttXj3d8mBwA7GF1H4pAEKEOeotJXmzmhexyZ%2BWhpzn%2F5fyhnq6n5oBLVmo3Ehi%2BWWRWncy13Qg%2FY2w7JCnzTmuS35vp64ruEIe89u78Ll0xHSi7Y0FaEf22lJOFDEOxiEOfoUF7JWz%2FXamONgcvCkBPXgyxkjloJ9QttP&X-Amz-Signature=68e72c8eef5fd35040fa1b496c32f1a0cbcfac41fa3b9565cfee236b3fd4ecce&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We successfully changed `administrator`’s password!

Try to logout and login again, this time with the credentials `administrator:peter`:

And I appear to be inside the administrator account. The application states that my username is `administrator` and it provides me with a link to an `Admin panel`. I access it, delete `carlos` and receive a confirmation:
