# Limit overrun race conditions        

### Goal - 

 Purchase a **Lightweight L33t Leather Jacket**.

### Analysis/Exploitation -

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/984b292b-8449-421b-a61f-4620e31b0ecc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X6FENCYS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204758Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGWCKU%2BC0teGmSFzvDGekvumeRebw%2Bu%2Fy%2FXEFSsAhw5EAiBDXxSaSlClSKeBjwS%2FGQkY0DrvNnTs5v5SHKXE6UhhJiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlnyzgBqzKvRb7qDvKtwDj4%2FOwWymBDlUyPz7qspNcQBIcgVabCF5SJP4sKgi9Lhs4jG%2B1G9%2Bh15UiIt%2B3Nh4Qc3SuGOOgeQU7a1FrHRgg4Y9IzpNG2HBCb%2Ban4iRf5yHTNABfIpMqE%2FYt%2B%2B314cH7hfhWKaKSQ6C0%2FZG2x%2BBuXkU4kJZHoE4Q2tKsV%2FRIfcH8Jqq%2FqU06jDu8EDLXVzUlYbt%2ByX3QXSzJWAHuKPjal8l3VBqDFKLuEjzF5ib1BtxzwJR7i81dqhcSs%2BQSI5W2%2FqUR3Q4SyfKzCKD8iY79So9kOsHp1uKOsVDPft%2FXKxc8BOXReVbyVX9NJrnwZbT2lUMK2yWPnwa90FkBBEtyNpiKL%2BCD%2BghjR9AOMmdLN7EwMX0ywDk8G%2B71p96GMa6As3zqfewa2JEabHJjSEr%2B69jqpSC5WDJBOkersosYFUbhtQ99PrKtOR%2B0FAXJPsCZp6vg1260V0l%2FeJ7eITR97FUP2ZdXyrn7t2cpMbTnjSNXYH%2BsIx4oDUhSkix7BFVA4Y8m93AwEwqsDebh37ybFK5fOXIsy%2B2%2BAcUVIpJRIBKISaOBfM5C6vMiiIiGA0DBsTMk88mHZVZyR8f%2FPAoWq8ExY0K%2FO6x0pW9C3qnsrtzGWy%2BiZhGkZfoZMkwscai1AY6pgEQ9im9CTkA%2BXn2bKAh5exZ%2BPZ5TFVabK%2FInV7HYlvEOu99TPEd297E%2BdzEBdC0%2Fb2ncXsNabatmP6OD%2Fu%2B%2Fd8dA6Ohy2cYKL%2BcsArb%2BJc1RaZrkDGFrfaKFB3n40FfgjDw9obcgBAiEyalDZ6POmEMI0Tt7k0p2rnW3fQ2D%2BmyPiH0kVmc%2BEMWMrmWeuxxt3ev8JmZas9VxIJtSHT06Z72%2BCcxM6sv&X-Amz-Signature=d8a63e0d3eed697ed653acd55d7c15702876af20ebed1b2ea5740c62f4f4aa31&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In home page, we can see that the promotion code `PROMO20` for 20% off, and we can purchase some items.

**Login as user** `wiener`**:**

Now, let's try to purchase the "Lightweight L33t Leather Jacket":

**Apply the coupon code** `PROMO20`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b94b8ca6-42a4-4c20-bc37-95cbad195670/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X6FENCYS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204758Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGWCKU%2BC0teGmSFzvDGekvumeRebw%2Bu%2Fy%2FXEFSsAhw5EAiBDXxSaSlClSKeBjwS%2FGQkY0DrvNnTs5v5SHKXE6UhhJiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlnyzgBqzKvRb7qDvKtwDj4%2FOwWymBDlUyPz7qspNcQBIcgVabCF5SJP4sKgi9Lhs4jG%2B1G9%2Bh15UiIt%2B3Nh4Qc3SuGOOgeQU7a1FrHRgg4Y9IzpNG2HBCb%2Ban4iRf5yHTNABfIpMqE%2FYt%2B%2B314cH7hfhWKaKSQ6C0%2FZG2x%2BBuXkU4kJZHoE4Q2tKsV%2FRIfcH8Jqq%2FqU06jDu8EDLXVzUlYbt%2ByX3QXSzJWAHuKPjal8l3VBqDFKLuEjzF5ib1BtxzwJR7i81dqhcSs%2BQSI5W2%2FqUR3Q4SyfKzCKD8iY79So9kOsHp1uKOsVDPft%2FXKxc8BOXReVbyVX9NJrnwZbT2lUMK2yWPnwa90FkBBEtyNpiKL%2BCD%2BghjR9AOMmdLN7EwMX0ywDk8G%2B71p96GMa6As3zqfewa2JEabHJjSEr%2B69jqpSC5WDJBOkersosYFUbhtQ99PrKtOR%2B0FAXJPsCZp6vg1260V0l%2FeJ7eITR97FUP2ZdXyrn7t2cpMbTnjSNXYH%2BsIx4oDUhSkix7BFVA4Y8m93AwEwqsDebh37ybFK5fOXIsy%2B2%2BAcUVIpJRIBKISaOBfM5C6vMiiIiGA0DBsTMk88mHZVZyR8f%2FPAoWq8ExY0K%2FO6x0pW9C3qnsrtzGWy%2BiZhGkZfoZMkwscai1AY6pgEQ9im9CTkA%2BXn2bKAh5exZ%2BPZ5TFVabK%2FInV7HYlvEOu99TPEd297E%2BdzEBdC0%2Fb2ncXsNabatmP6OD%2Fu%2B%2Fd8dA6Ohy2cYKL%2BcsArb%2BJc1RaZrkDGFrfaKFB3n40FfgjDw9obcgBAiEyalDZ6POmEMI0Tt7k0p2rnW3fQ2D%2BmyPiH0kVmc%2BEMWMrmWeuxxt3ev8JmZas9VxIJtSHT06Z72%2BCcxM6sv&X-Amz-Signature=67f84bb3dcfa2a218560d2ae77a2823d7da75afd186d12c8456ae6efbe8d8037&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we clicked the "Apply" button, it'll send a POST request to `/cart/coupon`, with parameter `csrf` and `coupon`.

We still do not have enough store credit for this purchase after applying coupon.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d91b1317-f0df-4c05-9498-795455384684/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X6FENCYS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204758Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGWCKU%2BC0teGmSFzvDGekvumeRebw%2Bu%2Fy%2FXEFSsAhw5EAiBDXxSaSlClSKeBjwS%2FGQkY0DrvNnTs5v5SHKXE6UhhJiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlnyzgBqzKvRb7qDvKtwDj4%2FOwWymBDlUyPz7qspNcQBIcgVabCF5SJP4sKgi9Lhs4jG%2B1G9%2Bh15UiIt%2B3Nh4Qc3SuGOOgeQU7a1FrHRgg4Y9IzpNG2HBCb%2Ban4iRf5yHTNABfIpMqE%2FYt%2B%2B314cH7hfhWKaKSQ6C0%2FZG2x%2BBuXkU4kJZHoE4Q2tKsV%2FRIfcH8Jqq%2FqU06jDu8EDLXVzUlYbt%2ByX3QXSzJWAHuKPjal8l3VBqDFKLuEjzF5ib1BtxzwJR7i81dqhcSs%2BQSI5W2%2FqUR3Q4SyfKzCKD8iY79So9kOsHp1uKOsVDPft%2FXKxc8BOXReVbyVX9NJrnwZbT2lUMK2yWPnwa90FkBBEtyNpiKL%2BCD%2BghjR9AOMmdLN7EwMX0ywDk8G%2B71p96GMa6As3zqfewa2JEabHJjSEr%2B69jqpSC5WDJBOkersosYFUbhtQ99PrKtOR%2B0FAXJPsCZp6vg1260V0l%2FeJ7eITR97FUP2ZdXyrn7t2cpMbTnjSNXYH%2BsIx4oDUhSkix7BFVA4Y8m93AwEwqsDebh37ybFK5fOXIsy%2B2%2BAcUVIpJRIBKISaOBfM5C6vMiiIiGA0DBsTMk88mHZVZyR8f%2FPAoWq8ExY0K%2FO6x0pW9C3qnsrtzGWy%2BiZhGkZfoZMkwscai1AY6pgEQ9im9CTkA%2BXn2bKAh5exZ%2BPZ5TFVabK%2FInV7HYlvEOu99TPEd297E%2BdzEBdC0%2Fb2ncXsNabatmP6OD%2Fu%2B%2Fd8dA6Ohy2cYKL%2BcsArb%2BJc1RaZrkDGFrfaKFB3n40FfgjDw9obcgBAiEyalDZ6POmEMI0Tt7k0p2rnW3fQ2D%2BmyPiH0kVmc%2BEMWMrmWeuxxt3ev8JmZas9VxIJtSHT06Z72%2BCcxM6sv&X-Amz-Signature=9950149dbe379c945ea840f18300555b023161b9764657ae8375fe7f9591fa23&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

If we try to apply the coupon again, it show an error message **"Coupon already applied"**:

In our case, the race window is the time of checking the coupon has been applied or not.

**To exploit this limit overruns race condition:**

1. Remove the applied coupon first
1. Then send the `/cart/coupon` POST request to Burp Suite's Repeater 30 times 
1. Add those tabs to group
1. Select "Send group in parallel"
1. After that, send the requests in parallel
The coupon reduced the original price a lot more! Therefore, the application's apply coupon function is indeed vulnerable to limit overruns race condition!

Now Place the order to solve the lab


