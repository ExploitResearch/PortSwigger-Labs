# Limit overrun race conditions        

### Goal - 

 Purchase a **Lightweight L33t Leather Jacket**.

### Analysis/Exploitation -

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/984b292b-8449-421b-a61f-4620e31b0ecc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QM75DEEE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222133Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIH7gc4wjbCA8yEkL38bP7xrzf%2B4lGv5l7Zbxta2ModKXAiEAjtb647KjbiCTHrYqCBNKvXqW%2BhCouf4ctpqqwnoTIFAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAfb1SIU9pDwtCYj%2ByrcA7nIPT17V3KYo85Z2Ml1S4g8SC3m5fO%2B22RVG458Yw7M%2FkuwNX12f8l8AlT1QloPkpCY1cBMTrS769IJgYQazjs7n9siFyV8l4szDPQUiFw23bo%2BhrdpkqwKP0XVWWJViJfmzt5ft2izHi8dcTSD0o19VfN4nHAbGxy041T%2FNpg3tvswBerQbnTJB8MR71kpf0SuEZHRflNTH4uesaBXGd%2FyED7gdvCcHF1I53Ln2EdTcDUJ8mDNrcRhay47AslKupU6OnI9JhTmyvPZWN9ANkbAZJRQ6%2FLS8yXlQb0vRn%2FObQdJCu68xsW28PmHZ8yWKLODP9hucDQi64UOuHKExzXULTxxsm42coF1rXHFj8Rq%2F%2Fo2sPvL79lG7K45xF5HckOjv0jQTRkDmwmbjT8sdbp1UfYYIRkxO9rQUn4jzwo8IjHVENX70wRxW26i0qwLRQWsv4%2BorFPyWa6YI%2BhNBPqNfJdB6WX5%2FcaGWjdvxjfTn0ryKgWq4FQd3xUapK3YE9gKt481gjZIKEODrfZZuvRouFYQpUxVgSIDv5IDQeI%2FZOaKguAE5eDr%2Bn%2BO6iBS0%2FjM%2F%2BUYKjD9IbiMwf0XXbd1BmW%2FOsVCFUaYBKxKS33sIBNHcdqfmSIsIcUlMPSDo9QGOqUBSm6QnDz%2Fz%2B1dR%2BS0m8Hbj1am6BCZWgqZoJUJ9sCk54RZA4%2FBEwAARLVEFYQLIYiFIFFg8c9Ff5CaYOELD2e4nQqNNcWsCXX9FzO4rHKKqizkv%2Fz%2B0ZLI51FA7DASVV%2FlKY0O%2BxlAyP8mtI%2B7ZcV59RLPgGMdLGp81%2F8gwq8FAm0HXu5qpDcfkqxYrQdhKUjLgHfTGl%2BoCf8usd0DRJ3cqg9jTMz0&X-Amz-Signature=2895ad3de3ff6874913d1e9ae255bc481c363ee4cedb7c2fc791c5c7dbe646bc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In home page, we can see that the promotion code `PROMO20` for 20% off, and we can purchase some items.

**Login as user** `wiener`**:**

Now, let's try to purchase the "Lightweight L33t Leather Jacket":

**Apply the coupon code** `PROMO20`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b94b8ca6-42a4-4c20-bc37-95cbad195670/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QM75DEEE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222133Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIH7gc4wjbCA8yEkL38bP7xrzf%2B4lGv5l7Zbxta2ModKXAiEAjtb647KjbiCTHrYqCBNKvXqW%2BhCouf4ctpqqwnoTIFAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAfb1SIU9pDwtCYj%2ByrcA7nIPT17V3KYo85Z2Ml1S4g8SC3m5fO%2B22RVG458Yw7M%2FkuwNX12f8l8AlT1QloPkpCY1cBMTrS769IJgYQazjs7n9siFyV8l4szDPQUiFw23bo%2BhrdpkqwKP0XVWWJViJfmzt5ft2izHi8dcTSD0o19VfN4nHAbGxy041T%2FNpg3tvswBerQbnTJB8MR71kpf0SuEZHRflNTH4uesaBXGd%2FyED7gdvCcHF1I53Ln2EdTcDUJ8mDNrcRhay47AslKupU6OnI9JhTmyvPZWN9ANkbAZJRQ6%2FLS8yXlQb0vRn%2FObQdJCu68xsW28PmHZ8yWKLODP9hucDQi64UOuHKExzXULTxxsm42coF1rXHFj8Rq%2F%2Fo2sPvL79lG7K45xF5HckOjv0jQTRkDmwmbjT8sdbp1UfYYIRkxO9rQUn4jzwo8IjHVENX70wRxW26i0qwLRQWsv4%2BorFPyWa6YI%2BhNBPqNfJdB6WX5%2FcaGWjdvxjfTn0ryKgWq4FQd3xUapK3YE9gKt481gjZIKEODrfZZuvRouFYQpUxVgSIDv5IDQeI%2FZOaKguAE5eDr%2Bn%2BO6iBS0%2FjM%2F%2BUYKjD9IbiMwf0XXbd1BmW%2FOsVCFUaYBKxKS33sIBNHcdqfmSIsIcUlMPSDo9QGOqUBSm6QnDz%2Fz%2B1dR%2BS0m8Hbj1am6BCZWgqZoJUJ9sCk54RZA4%2FBEwAARLVEFYQLIYiFIFFg8c9Ff5CaYOELD2e4nQqNNcWsCXX9FzO4rHKKqizkv%2Fz%2B0ZLI51FA7DASVV%2FlKY0O%2BxlAyP8mtI%2B7ZcV59RLPgGMdLGp81%2F8gwq8FAm0HXu5qpDcfkqxYrQdhKUjLgHfTGl%2BoCf8usd0DRJ3cqg9jTMz0&X-Amz-Signature=6a85781acdb208ba4f22799f4c35664502873b15bda45c6b495cb43009be20af&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we clicked the "Apply" button, it'll send a POST request to `/cart/coupon`, with parameter `csrf` and `coupon`.

We still do not have enough store credit for this purchase after applying coupon.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d91b1317-f0df-4c05-9498-795455384684/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QM75DEEE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222133Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIH7gc4wjbCA8yEkL38bP7xrzf%2B4lGv5l7Zbxta2ModKXAiEAjtb647KjbiCTHrYqCBNKvXqW%2BhCouf4ctpqqwnoTIFAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAfb1SIU9pDwtCYj%2ByrcA7nIPT17V3KYo85Z2Ml1S4g8SC3m5fO%2B22RVG458Yw7M%2FkuwNX12f8l8AlT1QloPkpCY1cBMTrS769IJgYQazjs7n9siFyV8l4szDPQUiFw23bo%2BhrdpkqwKP0XVWWJViJfmzt5ft2izHi8dcTSD0o19VfN4nHAbGxy041T%2FNpg3tvswBerQbnTJB8MR71kpf0SuEZHRflNTH4uesaBXGd%2FyED7gdvCcHF1I53Ln2EdTcDUJ8mDNrcRhay47AslKupU6OnI9JhTmyvPZWN9ANkbAZJRQ6%2FLS8yXlQb0vRn%2FObQdJCu68xsW28PmHZ8yWKLODP9hucDQi64UOuHKExzXULTxxsm42coF1rXHFj8Rq%2F%2Fo2sPvL79lG7K45xF5HckOjv0jQTRkDmwmbjT8sdbp1UfYYIRkxO9rQUn4jzwo8IjHVENX70wRxW26i0qwLRQWsv4%2BorFPyWa6YI%2BhNBPqNfJdB6WX5%2FcaGWjdvxjfTn0ryKgWq4FQd3xUapK3YE9gKt481gjZIKEODrfZZuvRouFYQpUxVgSIDv5IDQeI%2FZOaKguAE5eDr%2Bn%2BO6iBS0%2FjM%2F%2BUYKjD9IbiMwf0XXbd1BmW%2FOsVCFUaYBKxKS33sIBNHcdqfmSIsIcUlMPSDo9QGOqUBSm6QnDz%2Fz%2B1dR%2BS0m8Hbj1am6BCZWgqZoJUJ9sCk54RZA4%2FBEwAARLVEFYQLIYiFIFFg8c9Ff5CaYOELD2e4nQqNNcWsCXX9FzO4rHKKqizkv%2Fz%2B0ZLI51FA7DASVV%2FlKY0O%2BxlAyP8mtI%2B7ZcV59RLPgGMdLGp81%2F8gwq8FAm0HXu5qpDcfkqxYrQdhKUjLgHfTGl%2BoCf8usd0DRJ3cqg9jTMz0&X-Amz-Signature=6a7bb618f53abcd346bc285a5bd52dc5d1b7b9feaf2fd2f1fddf9444a6c6b914&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
