# Limit overrun race conditions        

### Goal - 

 Purchase a **Lightweight L33t Leather Jacket**.

### Analysis/Exploitation -

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/984b292b-8449-421b-a61f-4620e31b0ecc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S626HQRQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210531Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIENFEbXBPeuxmOwKpXnlRMgVUcYd7krCxcm%2Fg9AobXieAiEAp9%2FbFTzdDilIUKnwXs2IGOWFuBgomsUUXfjzsGiBoy8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKEKEIFo2mnzhb6kKSrcA%2FU5PAdm%2FdVIX07jevr1ToaKlb7guF0LwUo6zz9fqhyfSRMa%2BTe1q4360yPkQh2B5NcDeCEt4DAKWHwhbCGzIMVXsjHmhxTQBAKzJtKH8RIvdSQflqIBgb6%2FY2bF84FtRy7eQ5cB%2BvtepC%2BciP4spuiT7bMolA4LqokXEDvjxJBwbwIDFoTsKADsdzt6%2BXBb2dSBCBzB%2FVMDKpFCMesokWE81Ch6Wutum3KxqMrI7ICnjSIuYiH4c%2BeLj%2B6kHAs0rIikOfqspSNhMmCONFJLYo5h1nkvEDZAMtqA%2FinNiwNN6jL%2FLh9ydILnhtRUVesDI%2B2A8aRB%2BihVG%2FWJbr8Vn4nY6oya10PgZse9lcfj3KAVBv3U7RZvLaaDZjTMq015J%2BPYl3n%2B2rQ4nQjHEaizrLfYvnsad8wBd4j7dRszKWJLxsngE6AilEOoVRBDCjVrXnfC8lfhvCClZbmF0lwl6ulOxgOSWIquhzD6cud9aWDan2R6Wys2Yp2xMQa%2B75Te%2FB0BNVc4NKiDF78VltV%2FhlR01iHMEE8XCNalptZRU7W9QFp5px9laPkClZ7%2F8q%2BFYDPVaaj0sWRIrVi5NNa7P%2F2xhSIon7lpxCVHxq%2F0pgFtOutwB0%2FuQ90JyGiYMKfGotQGOqUBqQXbqXxbhkZJIAHZtW8Y0rkBiqzD5w6N8gqlBj8N5wm3P38Z1WrMU4oUykxiXx9Rl%2FhpVYL%2B%2FfDPT289p6hLcrvucM0lComW6l9JvffokCn3c%2F6HbmDZ48uCN1zdxrYe1p1B4eds6BgRsAYXZV5bD%2Blsd6wYb5ghpx5BRKx36tZPZSHTYIPqoaYKGRYTVbHDwv6BqO0YLF9vn02juzFrsjjczRKL&X-Amz-Signature=86e227afd519c6e5f88017be0b2fa670900a8a1d340306905a8a0052c8d7078b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In home page, we can see that the promotion code `PROMO20` for 20% off, and we can purchase some items.

**Login as user** `wiener`**:**

Now, let's try to purchase the "Lightweight L33t Leather Jacket":

**Apply the coupon code** `PROMO20`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b94b8ca6-42a4-4c20-bc37-95cbad195670/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S626HQRQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210531Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIENFEbXBPeuxmOwKpXnlRMgVUcYd7krCxcm%2Fg9AobXieAiEAp9%2FbFTzdDilIUKnwXs2IGOWFuBgomsUUXfjzsGiBoy8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKEKEIFo2mnzhb6kKSrcA%2FU5PAdm%2FdVIX07jevr1ToaKlb7guF0LwUo6zz9fqhyfSRMa%2BTe1q4360yPkQh2B5NcDeCEt4DAKWHwhbCGzIMVXsjHmhxTQBAKzJtKH8RIvdSQflqIBgb6%2FY2bF84FtRy7eQ5cB%2BvtepC%2BciP4spuiT7bMolA4LqokXEDvjxJBwbwIDFoTsKADsdzt6%2BXBb2dSBCBzB%2FVMDKpFCMesokWE81Ch6Wutum3KxqMrI7ICnjSIuYiH4c%2BeLj%2B6kHAs0rIikOfqspSNhMmCONFJLYo5h1nkvEDZAMtqA%2FinNiwNN6jL%2FLh9ydILnhtRUVesDI%2B2A8aRB%2BihVG%2FWJbr8Vn4nY6oya10PgZse9lcfj3KAVBv3U7RZvLaaDZjTMq015J%2BPYl3n%2B2rQ4nQjHEaizrLfYvnsad8wBd4j7dRszKWJLxsngE6AilEOoVRBDCjVrXnfC8lfhvCClZbmF0lwl6ulOxgOSWIquhzD6cud9aWDan2R6Wys2Yp2xMQa%2B75Te%2FB0BNVc4NKiDF78VltV%2FhlR01iHMEE8XCNalptZRU7W9QFp5px9laPkClZ7%2F8q%2BFYDPVaaj0sWRIrVi5NNa7P%2F2xhSIon7lpxCVHxq%2F0pgFtOutwB0%2FuQ90JyGiYMKfGotQGOqUBqQXbqXxbhkZJIAHZtW8Y0rkBiqzD5w6N8gqlBj8N5wm3P38Z1WrMU4oUykxiXx9Rl%2FhpVYL%2B%2FfDPT289p6hLcrvucM0lComW6l9JvffokCn3c%2F6HbmDZ48uCN1zdxrYe1p1B4eds6BgRsAYXZV5bD%2Blsd6wYb5ghpx5BRKx36tZPZSHTYIPqoaYKGRYTVbHDwv6BqO0YLF9vn02juzFrsjjczRKL&X-Amz-Signature=11f4bd391a60f3564254921991c1b52152a164b64a0bb1a77a06ee54c10e6276&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we clicked the "Apply" button, it'll send a POST request to `/cart/coupon`, with parameter `csrf` and `coupon`.

We still do not have enough store credit for this purchase after applying coupon.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d91b1317-f0df-4c05-9498-795455384684/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S626HQRQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210531Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIENFEbXBPeuxmOwKpXnlRMgVUcYd7krCxcm%2Fg9AobXieAiEAp9%2FbFTzdDilIUKnwXs2IGOWFuBgomsUUXfjzsGiBoy8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKEKEIFo2mnzhb6kKSrcA%2FU5PAdm%2FdVIX07jevr1ToaKlb7guF0LwUo6zz9fqhyfSRMa%2BTe1q4360yPkQh2B5NcDeCEt4DAKWHwhbCGzIMVXsjHmhxTQBAKzJtKH8RIvdSQflqIBgb6%2FY2bF84FtRy7eQ5cB%2BvtepC%2BciP4spuiT7bMolA4LqokXEDvjxJBwbwIDFoTsKADsdzt6%2BXBb2dSBCBzB%2FVMDKpFCMesokWE81Ch6Wutum3KxqMrI7ICnjSIuYiH4c%2BeLj%2B6kHAs0rIikOfqspSNhMmCONFJLYo5h1nkvEDZAMtqA%2FinNiwNN6jL%2FLh9ydILnhtRUVesDI%2B2A8aRB%2BihVG%2FWJbr8Vn4nY6oya10PgZse9lcfj3KAVBv3U7RZvLaaDZjTMq015J%2BPYl3n%2B2rQ4nQjHEaizrLfYvnsad8wBd4j7dRszKWJLxsngE6AilEOoVRBDCjVrXnfC8lfhvCClZbmF0lwl6ulOxgOSWIquhzD6cud9aWDan2R6Wys2Yp2xMQa%2B75Te%2FB0BNVc4NKiDF78VltV%2FhlR01iHMEE8XCNalptZRU7W9QFp5px9laPkClZ7%2F8q%2BFYDPVaaj0sWRIrVi5NNa7P%2F2xhSIon7lpxCVHxq%2F0pgFtOutwB0%2FuQ90JyGiYMKfGotQGOqUBqQXbqXxbhkZJIAHZtW8Y0rkBiqzD5w6N8gqlBj8N5wm3P38Z1WrMU4oUykxiXx9Rl%2FhpVYL%2B%2FfDPT289p6hLcrvucM0lComW6l9JvffokCn3c%2F6HbmDZ48uCN1zdxrYe1p1B4eds6BgRsAYXZV5bD%2Blsd6wYb5ghpx5BRKx36tZPZSHTYIPqoaYKGRYTVbHDwv6BqO0YLF9vn02juzFrsjjczRKL&X-Amz-Signature=79ca9a38139e9fff6e1169f89dd658b1ce16108005be0907723a37a34a3adbc8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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


