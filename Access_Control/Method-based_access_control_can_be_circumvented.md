# Method-based access control can be circumvented

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator

### Analysis/Exploitation -

<details><summary>Summary</summary>

We can see this request with administrator user.

```text
POST /admin-roles HTTP/1.1
...
username=carlos&action=upgrade

```

```text

POST /admin-roles - HTTP/1.1   -->401 Unauthorized
GET /admin - HTTP/1.1   -->400 Missing parameter'username'
```

With non privileged user, we  get 401 Unauthorized error.

But we can bypass the error with another type of request instead of using POST.

```text
GET /admin-roles?username=wiener&action=upgrade HTTP/1.1 --> 302 Found
GET /admin --> 200 OK
```

</details>

familiarize yourself with the admin panel by logging in using the credentials `administrator:admin` 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3fea78d0-0b43-4ccf-a7b7-0409c6c0b92b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZNDRZ3K7%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221920Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIEKsPiWNEIhZsDFsQBq2QMCwFmNVxtpM2iCEvQ%2B2czGUAiBtA5YlEZWMVknrqfAnPBuKe4OTtk4%2BpEu5ByyVBMYcGiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMl4Dv%2Bn0wGLWH2zouKtwDHezXFK64yxly1TQEgmnADhhMKgUL19TndX718IoBPIPD%2BjD9kfyAoYCU76ZD5fdtLva9wu7PUm1yfWdkRrmXKOweGiSfpE%2BhL49pfdj0WpJREUmop3thuFXpwjc6EEHbY2EJU6HIM2S9AH4XxvBq3SG%2FS48f9TCJbAHMe29IIbcgbMpbK2%2B1BblaTLFOnL%2Bw2iANaXWV%2Bpse%2FGmXchwBIQtOsN8Su7JlvM4pu06Dxe9zyl8K%2F2A6MKO9wGOAm7FsZFHykIROIopNhM8wtZJfd509tTavAsehIRW8X%2FGmWZN1hVF1ZAxXZhGFfFgImhf0HcOOlWMYItWXqWbM6BTbQJZ9ktvJ%2FswzxjO1piwl5M%2FdcEoE7JWwKSWsUOLTfl%2B9cWW9p845YA6IGVXDr2KN1Lr02XbM4hCR%2BnYhf8WF6IFuEvjYdS62%2BN%2FD0OYYYxoExHDJXjKttA4XP1rV0aaHKH4SJBHS4jaV1efxuAEqp2gpQ%2FkbPpf52HOtyR3aygpCYHfrUL0eTFcVsDxnXP2wFW2yBif3iCFAD1OglrtxS4UMt6yITIX0xUg6A42gnerC485NSre6XMxQIFtUv5R0SBtH3Y2HUPvg8UOApioKjFyHioAKAlxQxg8HZjgww4Oj1AY6pgFisbMtjrwSWVrpnvpwX5DXCLD4%2B5%2FyuHcZfvXYjh%2FzZQQj6vC4OGmlrO%2FUXcrPlCrQxHPyIfS0S%2Fht1LudQLnD8vD6wZc9G%2BSwectx2ayvt2n64BoEwRwutGInW6MBfrwPdgusV36iBDl3hOIrtnlV1RvskoHQyV0dSfGYqHdiq6nAQu20LOw131OW2h6GpMCWVfDzKJjf3h0jrH1IVtua8W3GVp2O&X-Amz-Signature=62c8f0f3b840f1d0f792623ae8c63eeef626b48e4f4531f713cbbe8d5e013aa3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Here, administrator can upgrade or downgrade a user.

When we try to upgrade a user:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bf966fe2-5feb-4e1c-a3a5-452eb29a929e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZNDRZ3K7%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221920Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIEKsPiWNEIhZsDFsQBq2QMCwFmNVxtpM2iCEvQ%2B2czGUAiBtA5YlEZWMVknrqfAnPBuKe4OTtk4%2BpEu5ByyVBMYcGiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMl4Dv%2Bn0wGLWH2zouKtwDHezXFK64yxly1TQEgmnADhhMKgUL19TndX718IoBPIPD%2BjD9kfyAoYCU76ZD5fdtLva9wu7PUm1yfWdkRrmXKOweGiSfpE%2BhL49pfdj0WpJREUmop3thuFXpwjc6EEHbY2EJU6HIM2S9AH4XxvBq3SG%2FS48f9TCJbAHMe29IIbcgbMpbK2%2B1BblaTLFOnL%2Bw2iANaXWV%2Bpse%2FGmXchwBIQtOsN8Su7JlvM4pu06Dxe9zyl8K%2F2A6MKO9wGOAm7FsZFHykIROIopNhM8wtZJfd509tTavAsehIRW8X%2FGmWZN1hVF1ZAxXZhGFfFgImhf0HcOOlWMYItWXqWbM6BTbQJZ9ktvJ%2FswzxjO1piwl5M%2FdcEoE7JWwKSWsUOLTfl%2B9cWW9p845YA6IGVXDr2KN1Lr02XbM4hCR%2BnYhf8WF6IFuEvjYdS62%2BN%2FD0OYYYxoExHDJXjKttA4XP1rV0aaHKH4SJBHS4jaV1efxuAEqp2gpQ%2FkbPpf52HOtyR3aygpCYHfrUL0eTFcVsDxnXP2wFW2yBif3iCFAD1OglrtxS4UMt6yITIX0xUg6A42gnerC485NSre6XMxQIFtUv5R0SBtH3Y2HUPvg8UOApioKjFyHioAKAlxQxg8HZjgww4Oj1AY6pgFisbMtjrwSWVrpnvpwX5DXCLD4%2B5%2FyuHcZfvXYjh%2FzZQQj6vC4OGmlrO%2FUXcrPlCrQxHPyIfS0S%2Fht1LudQLnD8vD6wZc9G%2BSwectx2ayvt2n64BoEwRwutGInW6MBfrwPdgusV36iBDl3hOIrtnlV1RvskoHQyV0dSfGYqHdiq6nAQu20LOw131OW2h6GpMCWVfDzKJjf3h0jrH1IVtua8W3GVp2O&X-Amz-Signature=041fedce4a67f805f9490019c89ccf7459885cc2b5a94c1f283afcd746a2f17c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**It’s sending a POST request to **`/admin-roles`**, and with the **`username`** and **`action`**.**

Now, let’s log out and login as user `wiener` to do vertical privilege escalation!

After login send any GET request to repeater and change the ** **location to** **`/admin-roles`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/db04fb1e-ff4c-44b9-9f91-323f66a393fd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZNDRZ3K7%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221920Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIEKsPiWNEIhZsDFsQBq2QMCwFmNVxtpM2iCEvQ%2B2czGUAiBtA5YlEZWMVknrqfAnPBuKe4OTtk4%2BpEu5ByyVBMYcGiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMl4Dv%2Bn0wGLWH2zouKtwDHezXFK64yxly1TQEgmnADhhMKgUL19TndX718IoBPIPD%2BjD9kfyAoYCU76ZD5fdtLva9wu7PUm1yfWdkRrmXKOweGiSfpE%2BhL49pfdj0WpJREUmop3thuFXpwjc6EEHbY2EJU6HIM2S9AH4XxvBq3SG%2FS48f9TCJbAHMe29IIbcgbMpbK2%2B1BblaTLFOnL%2Bw2iANaXWV%2Bpse%2FGmXchwBIQtOsN8Su7JlvM4pu06Dxe9zyl8K%2F2A6MKO9wGOAm7FsZFHykIROIopNhM8wtZJfd509tTavAsehIRW8X%2FGmWZN1hVF1ZAxXZhGFfFgImhf0HcOOlWMYItWXqWbM6BTbQJZ9ktvJ%2FswzxjO1piwl5M%2FdcEoE7JWwKSWsUOLTfl%2B9cWW9p845YA6IGVXDr2KN1Lr02XbM4hCR%2BnYhf8WF6IFuEvjYdS62%2BN%2FD0OYYYxoExHDJXjKttA4XP1rV0aaHKH4SJBHS4jaV1efxuAEqp2gpQ%2FkbPpf52HOtyR3aygpCYHfrUL0eTFcVsDxnXP2wFW2yBif3iCFAD1OglrtxS4UMt6yITIX0xUg6A42gnerC485NSre6XMxQIFtUv5R0SBtH3Y2HUPvg8UOApioKjFyHioAKAlxQxg8HZjgww4Oj1AY6pgFisbMtjrwSWVrpnvpwX5DXCLD4%2B5%2FyuHcZfvXYjh%2FzZQQj6vC4OGmlrO%2FUXcrPlCrQxHPyIfS0S%2Fht1LudQLnD8vD6wZc9G%2BSwectx2ayvt2n64BoEwRwutGInW6MBfrwPdgusV36iBDl3hOIrtnlV1RvskoHQyV0dSfGYqHdiq6nAQu20LOw131OW2h6GpMCWVfDzKJjf3h0jrH1IVtua8W3GVp2O&X-Amz-Signature=212300039ef0f92e25bc095b3a7e888d7eafd883ecc319065dfc7f1233dd72a4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As you can see, looks like we can access `/admin-roles` when we’re sending a GET request to `/admin-roles` without any parameters.

If we change it to POST method we  get 401 Unauthorized . **So we’re allowed to send a GET request to **`/admin-roles`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0d60d2ee-8640-49ac-b6b5-46faa4aa89f6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466V6XVFZPC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221922Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHXM8p63gKb2SzmT9tuTEG5H2f%2BoIFlkJiGT56kw9KZLAiA2uTZs0JNqKI2GGeB5%2BXDNS1vCmwH2qK48SpIBMjoY4SqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM%2FuEHfnQ3R4k7BK8GKtwDVEXa%2FuDcqcby9QkpwjMZiqiPi2NResCudKjBSG8wnUzlagBxmozUpSTIzp4AhUFEU1g%2FTw0wW9S5%2B8i2UfILBBsT5ESeAHog5PFySG%2F3TtxUF7chdFKdy9jOLpvSmVxSsPO%2FESk7Qd%2Frosus0ku7F6bLgy6bm2J6lTe6SCkWC5oX7n1fh0B1neKxmRqAO2grXqpuVYchglbdTzSXTWVfSVRdmFY2d3GeDTOD2%2FzmJJ8NWWmJLko%2FJyAXgRcx%2Fj1f2djNw1QFZBE2RipUeU%2FDXMfqV3MYFxz18GTTTRoGPfsjaS9upokljafZbe65Pchvd4yMohifGaOGfXfzqecvYl5hKTgOB%2Bssr2Uhlko4yznllmleJi8SCfCbYvmhSoWyv54Nyo2vV1Qx35wOdtOqgb07RjC79ymVhZRfc7slES9%2FxSq2qaoRVRlVo17nM5q07tYF1c4ur8ZO2Kpijuv5YDOyMIVuvnNXbv%2FzdoYOFIQps3kxJhfBiuYZU6BIM9bnXSJm9JYGi7OhG1wiRhh79JgGlkXdwpTIN0WTv71zBmbaiAcuLHQx7nR7g0bOWhUa8ilI0w8hz05bAaVdqTEAJkqVIe2KHgQ5b%2FlmPUvgfqLgSwXgyKXKHPEiW0owm4aj1AY6pgH4AsqnCUMpbfArnWLD0NVyEn0OqcXmX8LSbHtLwidNhih%2BwU3nySFFY5czTdqRwT5nfO9Y9OoaPs3ScxobTz2of9wABrXcY%2FXKBWKwfkxMMTCr%2FKy3g%2Bzury3CyHL6hHTnbt9AtlHH8TDi0B8u4QyYINh8Y4uIa%2FzulPGPCJC22dSsrB07koR%2Bv6mTh%2BsuUI0I9drVri6JS8SovR9jTCGvmSpAM57G&X-Amz-Signature=fd45349bdba51965eedabc3a5f4421e41417f560e37750acce2a148516fa8b32&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**send a GET request to **`/admin-roles`**, with parameters: **`username=wiener&action=upgrade`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6012c499-f073-4ec4-873a-0494ba2fd88f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZNDRZ3K7%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221920Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIEKsPiWNEIhZsDFsQBq2QMCwFmNVxtpM2iCEvQ%2B2czGUAiBtA5YlEZWMVknrqfAnPBuKe4OTtk4%2BpEu5ByyVBMYcGiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMl4Dv%2Bn0wGLWH2zouKtwDHezXFK64yxly1TQEgmnADhhMKgUL19TndX718IoBPIPD%2BjD9kfyAoYCU76ZD5fdtLva9wu7PUm1yfWdkRrmXKOweGiSfpE%2BhL49pfdj0WpJREUmop3thuFXpwjc6EEHbY2EJU6HIM2S9AH4XxvBq3SG%2FS48f9TCJbAHMe29IIbcgbMpbK2%2B1BblaTLFOnL%2Bw2iANaXWV%2Bpse%2FGmXchwBIQtOsN8Su7JlvM4pu06Dxe9zyl8K%2F2A6MKO9wGOAm7FsZFHykIROIopNhM8wtZJfd509tTavAsehIRW8X%2FGmWZN1hVF1ZAxXZhGFfFgImhf0HcOOlWMYItWXqWbM6BTbQJZ9ktvJ%2FswzxjO1piwl5M%2FdcEoE7JWwKSWsUOLTfl%2B9cWW9p845YA6IGVXDr2KN1Lr02XbM4hCR%2BnYhf8WF6IFuEvjYdS62%2BN%2FD0OYYYxoExHDJXjKttA4XP1rV0aaHKH4SJBHS4jaV1efxuAEqp2gpQ%2FkbPpf52HOtyR3aygpCYHfrUL0eTFcVsDxnXP2wFW2yBif3iCFAD1OglrtxS4UMt6yITIX0xUg6A42gnerC485NSre6XMxQIFtUv5R0SBtH3Y2HUPvg8UOApioKjFyHioAKAlxQxg8HZjgww4Oj1AY6pgFisbMtjrwSWVrpnvpwX5DXCLD4%2B5%2FyuHcZfvXYjh%2FzZQQj6vC4OGmlrO%2FUXcrPlCrQxHPyIfS0S%2Fht1LudQLnD8vD6wZc9G%2BSwectx2ayvt2n64BoEwRwutGInW6MBfrwPdgusV36iBDl3hOIrtnlV1RvskoHQyV0dSfGYqHdiq6nAQu20LOw131OW2h6GpMCWVfDzKJjf3h0jrH1IVtua8W3GVp2O&X-Amz-Signature=2ccaf3a40a4f681f9de1011bdfef41304a746274f63d9f81856ebfc88bb69163&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
