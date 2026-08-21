# Brute-forcing a stay-logged-in cookie

- With Burp running, log in to your own account with the **Stay logged in** option selected. Notice that this sets a `stay-logged-in` cookie.
- Examine this cookie in the [Inspector](https://portswigger.net/burp/documentation/desktop/tools/inspector) panel and notice that it is Base64-encoded. Its decoded value is `wiener:51dc30ddc473d43a6011e9ebba6ca770`. Study the length and character set of this string and notice that it could be an MD5 hash. Given that the plaintext is your username, you can make an educated guess that this may be a hash of your password. Hash
your password using MD5 to confirm that this is the case. We now know
that the cookie is constructed as follows: `base64(username+':'+md5HashOfPassword)`
- Log out of your account.
- Send the most recent `GET /my-account` request to Burp Intruder.
- In Burp Intruder, add a payload position to the `stay-logged-in` cookie and add your own password as a single payload.
- Under **Payload processing**, add the following rules in order. These rules will be applied sequentially to each payload before the request is submitted.
  - Hash: `MD5`
  - Add prefix: `wiener:`
  - Encode: `Base64-encode`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f91009d9-d88e-4a5e-9e1f-e8b23c9a058a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666RQJMNWD%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215353Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICCp4ypldPYzZHpeFTn6fY1S0xGn9DRhq5WtjsEsYrq7AiA%2Bub3JVPpNQ7%2BWRTB3YDPWAyWAlfeWi9j%2FreVQcUJHgiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM78IcO1ikI18iDpGoKtwDdPiPttuNMxh6ND0HTpHba69ZmYNhFmr0TmvFEOBeYrVcWYJnl05UlalFH71iA0Y1ynCiWkj1MxuM56XD5weDCvWzWOnQPBLV%2Fs%2FIu7vl4iH%2BW1njw7anjU4bdeF219XJNHLD5X2FkKLWFZ2I9VJbBshphQKhdWAxaFjzNxrSKPelzL3W2Sgy9QXl%2BMHg2dTUR6kCl5onhJoNvSwbQ%2Fb2OdRypMEPxTFyM30wcC%2Bz93OLJDaBRU7PsmRhEdP2rCYBc%2F%2B%2BxhTFp5H75YqJjaWjchp8MHZ6VuvcvxKVOjJuK%2FreB3y7oeH2fTOLxRvu7iEILPNd99uUlbG4ZI1wisNJz8qWZasmoPBEbPoi%2BrabNzVq7o9Nsel6H10XMCNZ6OW0VS0fA8ULccdD7kpaLuFryvieVa06QR1OVXJMPoOzDvmAiO5%2Fhk8R15qYjCjVMQZ8uv1JjQTbGCZl70t7v0srIVYyNnNutgl%2B5VFxJD7yGkV4p93hRyAQxrMLY41cpgHtOaMaRNNOfyz9K8yeWhIYxJ%2BG2QsnBKYg8AiQtWXwgg5Ejc4NhT3VqMuVP%2BjhGt7lVhjrGMvRcTjKxlIF4KnYk4ODg%2FK64LTj9WPutoqo3nfZoA%2B%2F6jYCHa9VWp4wiIaj1AY6pgH3oq%2BdJCmH1crEySKV6TPJruf7EY2%2FkcnuP1shtSKE53UqYZvXNO9LEHnW6eeXXVjzgXoRNi1q0T5hfv0QcJ4XqAPZihxvJNpL92VZx2NiE1prJqhOMuWHyRjTNtAFRj0JYt4mGE9RzB2LFQw9mV4Sd%2Bt4e8FJ5OKCStMdk%2FTr2UMk8lUgSpUtxCukGhTJYVRdR2AdCYrmaWiXWu0%2BNt5lB0cJiw58&X-Amz-Signature=5106b7242fc59ba592ae604c48e54b7454523e23ba316cbc6363ffff95929f4f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- As the **Update email** button is only displayed when you access the `/my-account` page in an authenticated state, we can use the presence or absence of
this button to determine whether we've successfully brute-forced the
cookie. On the **Settings** tab, add a grep match rule to flag any responses containing the string `Update email`. Start the attack.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/438df8f5-9407-4de1-82b5-5558ec74f5ec/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466USUROU4Z%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215353Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIAwwu1JY%2FkBPG404g%2Bhe2Kg3DAoCg5PgtyEFcYK7ShZQAiEA3RjKrBkIXrLFQv6caEgZ3gKD6Bx83hfucBmmgmRFLbMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJ1netVPabXsADtdIyrcA4%2F0aHGj%2FrPUwKJ0UHvOeOx6pt1vFv4NRCzjMfL%2FIMWm44wx3ZGumuIcw9Pk5OsncFc5lEAme8Om11tZPt%2FLUT9f8pgX%2Ff65%2B4ah8Muy566abzo6kGPJ0CLGGhwQj00LFdTJM%2FXAa5J4zS2Gq5mNGZhZDsk2tVFhHsj9%2BvkWT%2FzTCLGqaOPVGR09jwC1QIusToi5GdgnAEpzMpSG2JeH%2FghvZrGbaHkGs0NRe81U98eu7PO4WB28nwYbTAbQjI8ruExnU%2Bc9qiElNY5%2BgI00ChoY2CWxDK%2F10tizbSyOaYQ4icj%2FM7ly%2FTQVxrmiI1Z5MEKli%2F1l4pLDO0EYu%2FudlGdEQMR3m0QoOv66WCPckKUVSGzrEIvGvCM6l8wAmbG%2BA5%2FTQ9eGqIJ5eDfjDHi45yqNwhZ8AmBXAmX5XrEYSlMHk8hzn2yDHtEnShrEyH2Hzz1mThbpuaPdDZ8SRhNCB4H41%2FSiYORQv051CeFRIx5is9Mv1QTAOZF61JaagfwxLBfQSwU0R0CqEPBQNTKysLUz4EVqpgSoRV6eT4AK59f3MLS3gPvr%2F%2BCh%2FP7dyNkBpCTogiis0850i3TJ6TFyHOYbrMvZC9CGTtOzBCogWB6Tng7myJPNNdWEJ9g8MK6Eo9QGOqUB%2Fg%2FreBNb%2BLuO49HBogpj658TKYiseBLcBInRWZV3HjmnqyFJnFsyoWVp5XMTFPQiredCU%2BQJznyqrkqJXegKiZg5VA9WgJjkPC1lmHv61p1a%2F7uaiXInWfUH%2FcD0aZlQdvK2ScIgb0DIeTgSvzM6aN3zgJjXXzLcz60tCDfkTpCFxxCPJ1bNZ3FzFGDs70x0ptqpoBWlNOfRqTDcRxtBvruDucvo&X-Amz-Signature=d5ceb2e72543a35e6ea1eeff33fbc908eab71c94dec985f239901f31d56b7758&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- Notice that the generated payload was used to
successfully load your own account page. This confirms that the payload
processing rules work as expected and you were able to construct a valid cookie for your own account.
- Make the following adjustments and then repeat this attack:
  - Remove your own password from the payload list and add the list of [candidate passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords) instead.
  - Change the **Add prefix** rule to add `carlos:` instead of `wiener:`.
- When the attack is finished, the lab will be
solved. Notice that only one request returned a response containing `Update email`. The payload from this request is the valid `stay-logged-in` cookie for Carlos's account.