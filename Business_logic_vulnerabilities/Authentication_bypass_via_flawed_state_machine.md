# Authentication bypass via flawed state machine

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

What immediately jumps to attention is that the login is a two-stage process. After providing the username and the password, I can select the role I want to login as:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8f85723a-9796-4bce-8951-94eb87058afa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SWWJDSBY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215615Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDBQsyKeNhQPF39Kck3nXRsWNyymfR7BlvoIKB%2Fi9mnBAiEA4bxo1zgVbmsIkRb%2BItWZRDZM9sdW52fn0YZ89zFrsD8qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJJJqgWMFvzukp%2BlUSrcA18pIbYyOllyC4aPsDJd7uk62RhsMJFSBtPSj%2BNYNtz%2Bk0sZJefnVaeD4vlKrIjMheExKCiAP9O86qCxkKJ%2FHRlKUGQ87NEVTceqYqnbQ2oTNI5j11aBRa1HqJuStlLrxT4l1DBsewZVfAzDpZ0yDWQvXzofuctdTsEHNxWcjM45i0Atxd4juO3xKvluc24XmSzXPRtgVccvzn9q2o6Qvo4VYvBQtRgyBSgPv47bYf88kTDYSneEF8P32oKhZwDA5yXpr1Z7FwyCjZvUUBGtRGU0OXgvJZz%2Bb9nhgfcp8F%2FWNWBaVflBxbD2XCQ8jIy%2FK3UnuRts7nD68aJdmcpA841V3RbYKmalKMAeldRwOB26E1yzY%2FgmOzQI%2B6cQAZuMCww%2F1fncD3gNrwyX9t%2FpkcDGoJNAZfVlZSrAbYc8Bd5v%2FjCznjW%2ByLKpaRqEUhPEnnX%2BDbMV%2F8rNKU%2FLexJiK1RhJioZdkxhnWbxlGk37HxcwRivRGAyDcL48I8kEXD%2FVZJ0mNfRSxu7C%2Fyu0t0uFsyElxQd3GACFHkTf0IG1UEy%2FlcFjdWm9tH5VQphmNhRsfvmC2KddHOeP6iOxBxyawF1IYhTVDyRqdDTJ6rSw7%2F0T%2FhVOiRnCtJwavPgMPOEo9QGOqUBwqrTdgXzCoMPPD5QVcST6froLuSi6bX73RgNzsk%2BfmnvIMLWFQJdfqg2OTsBZUZXwGh%2BcT6wKxKLCXBeiYgqhkh3hnw0Q7yDA33xnY76OHtU4XELKAY%2B7ioUH4kZ8Tne%2F75yCxo24GPxmFkqfT5CjwxQaU9p%2FaFnndF5Vw4oW99eWMM9SvgNVw3SxEwVtphb8ovFul1ieB%2F12g6t%2FBmsUvN3a6E%2F&X-Amz-Signature=910699914979a7144eefbf0af74f840391f763a0e2f4f874b5b6d8bee9c6a420&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Such an option does make sense. It allows users with higher privileges to restrict their permissions when they don't need them. This reduces both the attack surface during everyday activities as well as the risk of stupid and expensive mistakes. At least, if done properly. Having two dedicated accounts for this is both easier and less error-prone.

I select `user` and have a look at the `/role-selector` request in Burp Proxy:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7f5f1009-20d2-4c5a-a7c3-e6801b35ad10/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SWWJDSBY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215615Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDBQsyKeNhQPF39Kck3nXRsWNyymfR7BlvoIKB%2Fi9mnBAiEA4bxo1zgVbmsIkRb%2BItWZRDZM9sdW52fn0YZ89zFrsD8qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJJJqgWMFvzukp%2BlUSrcA18pIbYyOllyC4aPsDJd7uk62RhsMJFSBtPSj%2BNYNtz%2Bk0sZJefnVaeD4vlKrIjMheExKCiAP9O86qCxkKJ%2FHRlKUGQ87NEVTceqYqnbQ2oTNI5j11aBRa1HqJuStlLrxT4l1DBsewZVfAzDpZ0yDWQvXzofuctdTsEHNxWcjM45i0Atxd4juO3xKvluc24XmSzXPRtgVccvzn9q2o6Qvo4VYvBQtRgyBSgPv47bYf88kTDYSneEF8P32oKhZwDA5yXpr1Z7FwyCjZvUUBGtRGU0OXgvJZz%2Bb9nhgfcp8F%2FWNWBaVflBxbD2XCQ8jIy%2FK3UnuRts7nD68aJdmcpA841V3RbYKmalKMAeldRwOB26E1yzY%2FgmOzQI%2B6cQAZuMCww%2F1fncD3gNrwyX9t%2FpkcDGoJNAZfVlZSrAbYc8Bd5v%2FjCznjW%2ByLKpaRqEUhPEnnX%2BDbMV%2F8rNKU%2FLexJiK1RhJioZdkxhnWbxlGk37HxcwRivRGAyDcL48I8kEXD%2FVZJ0mNfRSxu7C%2Fyu0t0uFsyElxQd3GACFHkTf0IG1UEy%2FlcFjdWm9tH5VQphmNhRsfvmC2KddHOeP6iOxBxyawF1IYhTVDyRqdDTJ6rSw7%2F0T%2FhVOiRnCtJwavPgMPOEo9QGOqUBwqrTdgXzCoMPPD5QVcST6froLuSi6bX73RgNzsk%2BfmnvIMLWFQJdfqg2OTsBZUZXwGh%2BcT6wKxKLCXBeiYgqhkh3hnw0Q7yDA33xnY76OHtU4XELKAY%2B7ioUH4kZ8Tne%2F75yCxo24GPxmFkqfT5CjwxQaU9p%2FaFnndF5Vw4oW99eWMM9SvgNVw3SxEwVtphb8ovFul1ieB%2F12g6t%2FBmsUvN3a6E%2F&X-Amz-Signature=4e799790288955e7a2108a581a52c4bbc820a58adb8f7e1e36f43cc40008d7d3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Attempt 1: Adjust role

The second login stage contains the user role. The roles available to me are listed on the page. I don't know whether another check is done during the POST of this form.

What happens if I change the role to 'admin' or 'administrator'? Of course, I don't know the role names, but it is worth a try.

Unfortunately, this does not lead to anything, neither error nor more privileges. This indicates that on processing that POST, it validates against allowed roles and defaults to something that is not admin.

### Attempt 2: Drop request

Speaking about defaulting, what happens if the full second request is dropped? Common sense would indicate that the session is dropped if any request is made before the second stage is finished. Easy to find out.

Using Burp proxy I log in with `wiener:peter` but drop the `GET` request to `/role-selector` completely. Afterwards, then manually browse to `/my-account`. Observe that role has defaulted to the `administrator` role and have access to the admin panel.           

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa7cb002-4763-4034-85ee-5c15a07d2fd1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SWWJDSBY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215615Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDBQsyKeNhQPF39Kck3nXRsWNyymfR7BlvoIKB%2Fi9mnBAiEA4bxo1zgVbmsIkRb%2BItWZRDZM9sdW52fn0YZ89zFrsD8qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJJJqgWMFvzukp%2BlUSrcA18pIbYyOllyC4aPsDJd7uk62RhsMJFSBtPSj%2BNYNtz%2Bk0sZJefnVaeD4vlKrIjMheExKCiAP9O86qCxkKJ%2FHRlKUGQ87NEVTceqYqnbQ2oTNI5j11aBRa1HqJuStlLrxT4l1DBsewZVfAzDpZ0yDWQvXzofuctdTsEHNxWcjM45i0Atxd4juO3xKvluc24XmSzXPRtgVccvzn9q2o6Qvo4VYvBQtRgyBSgPv47bYf88kTDYSneEF8P32oKhZwDA5yXpr1Z7FwyCjZvUUBGtRGU0OXgvJZz%2Bb9nhgfcp8F%2FWNWBaVflBxbD2XCQ8jIy%2FK3UnuRts7nD68aJdmcpA841V3RbYKmalKMAeldRwOB26E1yzY%2FgmOzQI%2B6cQAZuMCww%2F1fncD3gNrwyX9t%2FpkcDGoJNAZfVlZSrAbYc8Bd5v%2FjCznjW%2ByLKpaRqEUhPEnnX%2BDbMV%2F8rNKU%2FLexJiK1RhJioZdkxhnWbxlGk37HxcwRivRGAyDcL48I8kEXD%2FVZJ0mNfRSxu7C%2Fyu0t0uFsyElxQd3GACFHkTf0IG1UEy%2FlcFjdWm9tH5VQphmNhRsfvmC2KddHOeP6iOxBxyawF1IYhTVDyRqdDTJ6rSw7%2F0T%2FhVOiRnCtJwavPgMPOEo9QGOqUBwqrTdgXzCoMPPD5QVcST6froLuSi6bX73RgNzsk%2BfmnvIMLWFQJdfqg2OTsBZUZXwGh%2BcT6wKxKLCXBeiYgqhkh3hnw0Q7yDA33xnY76OHtU4XELKAY%2B7ioUH4kZ8Tne%2F75yCxo24GPxmFkqfT5CjwxQaU9p%2FaFnndF5Vw4oW99eWMM9SvgNVw3SxEwVtphb8ovFul1ieB%2F12g6t%2FBmsUvN3a6E%2F&X-Amz-Signature=baee27dc7f1fc7e72655401e44c5bd41af30da6ba70b21d67f8d2c0e687260ca&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now simply go to the Admin panel and use the link to delete user `carlos`. 
