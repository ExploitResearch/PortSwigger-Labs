# Authentication bypass via flawed state machine

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

What immediately jumps to attention is that the login is a two-stage process. After providing the username and the password, I can select the role I want to login as:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8f85723a-9796-4bce-8951-94eb87058afa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QRZABZLF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204727Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHCnTjd4LZHAEspqLnpzsdFERfb%2BrwrSEb5z%2FhfE5YzWAiBvbk9gA3ez82Li1v2mXCj%2BDHxWSNxqi9fW2Lap66z7xyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMDANcQ%2FW%2FCBVO770cKtwDMZrWWgfkT3aKRchMFBfysd72%2FVh5jH6tolnswvMsn6CQcV6Ft4HzBmIyWWTBG6CH0y9sskR0DjxTBMJTa8ZnzInunO%2F06LPNfwKMxH5HE4nm6E1cevtauwBkpYv6bX7wVg8xxUCyo3OQwLEEwdGNEnV9Ukf24QxOIorS%2BZ8SzV2qxPpBT33m16TLOz%2FG%2BOaVy44Yu3PmINHcXvK2kdfEN0%2BUFBjgpmpivCAzF85TZS5CdyjkxKvE8CMpx96ZP6wkNwDVGbn9c%2BLCcun6Ig3rrN3UnSfVaVuqDb%2FTD1%2F5emGzlMUWbsqdaoEYD1w%2BHOxoWc5db6l61k071ChX7qKVsVmcEvSXSYLuZJE4uCthwoR0gwXQ5MwZpv8OUTJrT2Uz2FyCLbGg9RYPUL%2FRTKJvCci26gF35tbGX7Fsi3J6B9CmpOQB7gj0Tpl8kECiwOHl7RzzicvUMm1%2FwC5fMMKEaf%2BWvxu45WkhHxXFWYdRIgu6AaFJSJiEwrR%2FN%2FHx2m6ebF8L8RmZhe%2BbpeGtFuhnTPEZQ9njZ5yGGc7nYyv2Nuzs99XQdWxuts1LXqx%2BBqpgEaUxtmyQ3%2BfzczG8JW3hKtv9if307K32GYPMUpMTZBFSpxfIesWfCEs9cTwwpcai1AY6pgHkA3fhodyoOXmal%2FD94nuHdZUp5pucFH4ZandpGn5N5UqHJHHMOqOXrn1%2BQ%2B4sa7T68TdagaUnYbHKWcycDpHQEFI%2F1E8%2BUixhX6N9QrZw2AEkYqkiJ5ydmaXs%2Fy3dXJNtccchnZA6nMvASH6aEcqKart9LMQZ1jWerX4aBupQzwouWv915OiUCp58d2Cx0D%2FrLdLW60zJgxZQRYCUp8ECZB3nqDMn&X-Amz-Signature=67a89a98030fd87080ec3e41a800c7f02ce2d02e7e58405be1b240480f88ed2c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Such an option does make sense. It allows users with higher privileges to restrict their permissions when they don't need them. This reduces both the attack surface during everyday activities as well as the risk of stupid and expensive mistakes. At least, if done properly. Having two dedicated accounts for this is both easier and less error-prone.

I select `user` and have a look at the `/role-selector` request in Burp Proxy:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7f5f1009-20d2-4c5a-a7c3-e6801b35ad10/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QRZABZLF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204727Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHCnTjd4LZHAEspqLnpzsdFERfb%2BrwrSEb5z%2FhfE5YzWAiBvbk9gA3ez82Li1v2mXCj%2BDHxWSNxqi9fW2Lap66z7xyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMDANcQ%2FW%2FCBVO770cKtwDMZrWWgfkT3aKRchMFBfysd72%2FVh5jH6tolnswvMsn6CQcV6Ft4HzBmIyWWTBG6CH0y9sskR0DjxTBMJTa8ZnzInunO%2F06LPNfwKMxH5HE4nm6E1cevtauwBkpYv6bX7wVg8xxUCyo3OQwLEEwdGNEnV9Ukf24QxOIorS%2BZ8SzV2qxPpBT33m16TLOz%2FG%2BOaVy44Yu3PmINHcXvK2kdfEN0%2BUFBjgpmpivCAzF85TZS5CdyjkxKvE8CMpx96ZP6wkNwDVGbn9c%2BLCcun6Ig3rrN3UnSfVaVuqDb%2FTD1%2F5emGzlMUWbsqdaoEYD1w%2BHOxoWc5db6l61k071ChX7qKVsVmcEvSXSYLuZJE4uCthwoR0gwXQ5MwZpv8OUTJrT2Uz2FyCLbGg9RYPUL%2FRTKJvCci26gF35tbGX7Fsi3J6B9CmpOQB7gj0Tpl8kECiwOHl7RzzicvUMm1%2FwC5fMMKEaf%2BWvxu45WkhHxXFWYdRIgu6AaFJSJiEwrR%2FN%2FHx2m6ebF8L8RmZhe%2BbpeGtFuhnTPEZQ9njZ5yGGc7nYyv2Nuzs99XQdWxuts1LXqx%2BBqpgEaUxtmyQ3%2BfzczG8JW3hKtv9if307K32GYPMUpMTZBFSpxfIesWfCEs9cTwwpcai1AY6pgHkA3fhodyoOXmal%2FD94nuHdZUp5pucFH4ZandpGn5N5UqHJHHMOqOXrn1%2BQ%2B4sa7T68TdagaUnYbHKWcycDpHQEFI%2F1E8%2BUixhX6N9QrZw2AEkYqkiJ5ydmaXs%2Fy3dXJNtccchnZA6nMvASH6aEcqKart9LMQZ1jWerX4aBupQzwouWv915OiUCp58d2Cx0D%2FrLdLW60zJgxZQRYCUp8ECZB3nqDMn&X-Amz-Signature=08ff9649b7067ea3f6d9b8fd6a24780019da43a582f0832c74a6adb149cc7f67&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Attempt 1: Adjust role

The second login stage contains the user role. The roles available to me are listed on the page. I don't know whether another check is done during the POST of this form.

What happens if I change the role to 'admin' or 'administrator'? Of course, I don't know the role names, but it is worth a try.

Unfortunately, this does not lead to anything, neither error nor more privileges. This indicates that on processing that POST, it validates against allowed roles and defaults to something that is not admin.

### Attempt 2: Drop request

Speaking about defaulting, what happens if the full second request is dropped? Common sense would indicate that the session is dropped if any request is made before the second stage is finished. Easy to find out.

Using Burp proxy I log in with `wiener:peter` but drop the `GET` request to `/role-selector` completely. Afterwards, then manually browse to `/my-account`. Observe that role has defaulted to the `administrator` role and have access to the admin panel.           

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa7cb002-4763-4034-85ee-5c15a07d2fd1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QRZABZLF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204727Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHCnTjd4LZHAEspqLnpzsdFERfb%2BrwrSEb5z%2FhfE5YzWAiBvbk9gA3ez82Li1v2mXCj%2BDHxWSNxqi9fW2Lap66z7xyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMDANcQ%2FW%2FCBVO770cKtwDMZrWWgfkT3aKRchMFBfysd72%2FVh5jH6tolnswvMsn6CQcV6Ft4HzBmIyWWTBG6CH0y9sskR0DjxTBMJTa8ZnzInunO%2F06LPNfwKMxH5HE4nm6E1cevtauwBkpYv6bX7wVg8xxUCyo3OQwLEEwdGNEnV9Ukf24QxOIorS%2BZ8SzV2qxPpBT33m16TLOz%2FG%2BOaVy44Yu3PmINHcXvK2kdfEN0%2BUFBjgpmpivCAzF85TZS5CdyjkxKvE8CMpx96ZP6wkNwDVGbn9c%2BLCcun6Ig3rrN3UnSfVaVuqDb%2FTD1%2F5emGzlMUWbsqdaoEYD1w%2BHOxoWc5db6l61k071ChX7qKVsVmcEvSXSYLuZJE4uCthwoR0gwXQ5MwZpv8OUTJrT2Uz2FyCLbGg9RYPUL%2FRTKJvCci26gF35tbGX7Fsi3J6B9CmpOQB7gj0Tpl8kECiwOHl7RzzicvUMm1%2FwC5fMMKEaf%2BWvxu45WkhHxXFWYdRIgu6AaFJSJiEwrR%2FN%2FHx2m6ebF8L8RmZhe%2BbpeGtFuhnTPEZQ9njZ5yGGc7nYyv2Nuzs99XQdWxuts1LXqx%2BBqpgEaUxtmyQ3%2BfzczG8JW3hKtv9if307K32GYPMUpMTZBFSpxfIesWfCEs9cTwwpcai1AY6pgHkA3fhodyoOXmal%2FD94nuHdZUp5pucFH4ZandpGn5N5UqHJHHMOqOXrn1%2BQ%2B4sa7T68TdagaUnYbHKWcycDpHQEFI%2F1E8%2BUixhX6N9QrZw2AEkYqkiJ5ydmaXs%2Fy3dXJNtccchnZA6nMvASH6aEcqKart9LMQZ1jWerX4aBupQzwouWv915OiUCp58d2Cx0D%2FrLdLW60zJgxZQRYCUp8ECZB3nqDMn&X-Amz-Signature=199f015a43b16c4a6213d04e52c8b1c01f363680a8990888c2dab1656f211101&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now simply go to the Admin panel and use the link to delete user `carlos`. 

