# Limit overrun race conditions        

### Goal - 

 Purchase a **Lightweight L33t Leather Jacket**.

### Analysis/Exploitation -

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/984b292b-8449-421b-a61f-4620e31b0ecc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WT5W3AN4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215653Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCly1wJ3Ewi5WLzOBMeMXkS9rlK9vjbN%2B4W94KCw1IOcgIhAJM92333glX1aXPANB7qb9%2F01Bq229gBEuW4%2FRAK%2FUd%2FKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzjmMX0KlPjbuQvHGsq3AP6Xd2%2B5W6ylSeW5cSbR%2BIt9YYsI2YVSMvSqOAtj2wAy0W6JoKjOB0uLlq4OQUZUv%2BT0XFexmrNMGb9wC%2FGJaqtd5TsOqRxkTuOD9zMVxHaeBEluu28YY9DDQlKEprmlrNHvi5DcjwRy42LSdsWORDQLUwkIfWtHKHbKOBPgsq5UBHx8qvqhK8eyHVn1ozJLfFUHjpyZDEa8GTaD4sLPd%2BcnPNdHOorbJpEf2LYA3yehXmz1NKIDP1tgEhv5LxiwLlLsoDDkDutaXaPT4XU0O%2BO9yoDfduDrWGQPz8FmQAWE3nXYtdG9HZei8sDzDT0PQve%2B%2B9c3vP9DfCndrrtsHzrPdrafrTLFgMkJm2qNvhb8UHfTATBEbe1%2F9FXqhWFGfawQyJD6mFt36%2BGTqozHUnarVTrqykb4fXPFdZcQN3T3z4wHMoi8%2F05rKFmK7utCEjLPSRoSiXjH%2FCgtY%2FzKJV5DQMh64wGiBzCDseXB6BYRpErshb1OzfvX9ysjBedEQXci7g3O6ZzU07GO8SyldMFlyOwF3NZmadhhZlxukJY9KN7UcMDT%2FJMCqrURHwedRsRTWcjokPw5KUeOzjzRwcZrkqW6Uu7laDw2yfVVaiJCzEUtOopN%2F44lGwDOzCMhqPUBjqkAbtunQbI%2BjSaVqaN3Z26GHuAIkng3Bc31jFAPySNC3kim%2FyKIHgGP4ceSNNyNvQEZkaDxRfLo5g1Me3zO9tPKT8bB4e2mTzbuRZWXExIzBgra1JeCGsOEfponqWcBhD3RDqf6tNTKVPPwzL2aaArMP7DgyDo4fi99YzNTEyrsGZ%2BkAo4a25J0qRCcYBd8bqUFqx4UE%2BVLah7jZSlTxZHWELHzNLS&X-Amz-Signature=80659a59d1a87398f4d207b1fbba778c1b9aa83c4826953e9b39c23af4b27cd1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In home page, we can see that the promotion code `PROMO20` for 20% off, and we can purchase some items.

**Login as user** `wiener`**:**

Now, let's try to purchase the "Lightweight L33t Leather Jacket":

**Apply the coupon code** `PROMO20`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b94b8ca6-42a4-4c20-bc37-95cbad195670/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WT5W3AN4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215653Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCly1wJ3Ewi5WLzOBMeMXkS9rlK9vjbN%2B4W94KCw1IOcgIhAJM92333glX1aXPANB7qb9%2F01Bq229gBEuW4%2FRAK%2FUd%2FKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzjmMX0KlPjbuQvHGsq3AP6Xd2%2B5W6ylSeW5cSbR%2BIt9YYsI2YVSMvSqOAtj2wAy0W6JoKjOB0uLlq4OQUZUv%2BT0XFexmrNMGb9wC%2FGJaqtd5TsOqRxkTuOD9zMVxHaeBEluu28YY9DDQlKEprmlrNHvi5DcjwRy42LSdsWORDQLUwkIfWtHKHbKOBPgsq5UBHx8qvqhK8eyHVn1ozJLfFUHjpyZDEa8GTaD4sLPd%2BcnPNdHOorbJpEf2LYA3yehXmz1NKIDP1tgEhv5LxiwLlLsoDDkDutaXaPT4XU0O%2BO9yoDfduDrWGQPz8FmQAWE3nXYtdG9HZei8sDzDT0PQve%2B%2B9c3vP9DfCndrrtsHzrPdrafrTLFgMkJm2qNvhb8UHfTATBEbe1%2F9FXqhWFGfawQyJD6mFt36%2BGTqozHUnarVTrqykb4fXPFdZcQN3T3z4wHMoi8%2F05rKFmK7utCEjLPSRoSiXjH%2FCgtY%2FzKJV5DQMh64wGiBzCDseXB6BYRpErshb1OzfvX9ysjBedEQXci7g3O6ZzU07GO8SyldMFlyOwF3NZmadhhZlxukJY9KN7UcMDT%2FJMCqrURHwedRsRTWcjokPw5KUeOzjzRwcZrkqW6Uu7laDw2yfVVaiJCzEUtOopN%2F44lGwDOzCMhqPUBjqkAbtunQbI%2BjSaVqaN3Z26GHuAIkng3Bc31jFAPySNC3kim%2FyKIHgGP4ceSNNyNvQEZkaDxRfLo5g1Me3zO9tPKT8bB4e2mTzbuRZWXExIzBgra1JeCGsOEfponqWcBhD3RDqf6tNTKVPPwzL2aaArMP7DgyDo4fi99YzNTEyrsGZ%2BkAo4a25J0qRCcYBd8bqUFqx4UE%2BVLah7jZSlTxZHWELHzNLS&X-Amz-Signature=24fd10013201c8b7dad2e11d1ae11a88280affae731bbc051fdcc8ed47be377f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we clicked the "Apply" button, it'll send a POST request to `/cart/coupon`, with parameter `csrf` and `coupon`.

We still do not have enough store credit for this purchase after applying coupon.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d91b1317-f0df-4c05-9498-795455384684/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WT5W3AN4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215653Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCly1wJ3Ewi5WLzOBMeMXkS9rlK9vjbN%2B4W94KCw1IOcgIhAJM92333glX1aXPANB7qb9%2F01Bq229gBEuW4%2FRAK%2FUd%2FKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzjmMX0KlPjbuQvHGsq3AP6Xd2%2B5W6ylSeW5cSbR%2BIt9YYsI2YVSMvSqOAtj2wAy0W6JoKjOB0uLlq4OQUZUv%2BT0XFexmrNMGb9wC%2FGJaqtd5TsOqRxkTuOD9zMVxHaeBEluu28YY9DDQlKEprmlrNHvi5DcjwRy42LSdsWORDQLUwkIfWtHKHbKOBPgsq5UBHx8qvqhK8eyHVn1ozJLfFUHjpyZDEa8GTaD4sLPd%2BcnPNdHOorbJpEf2LYA3yehXmz1NKIDP1tgEhv5LxiwLlLsoDDkDutaXaPT4XU0O%2BO9yoDfduDrWGQPz8FmQAWE3nXYtdG9HZei8sDzDT0PQve%2B%2B9c3vP9DfCndrrtsHzrPdrafrTLFgMkJm2qNvhb8UHfTATBEbe1%2F9FXqhWFGfawQyJD6mFt36%2BGTqozHUnarVTrqykb4fXPFdZcQN3T3z4wHMoi8%2F05rKFmK7utCEjLPSRoSiXjH%2FCgtY%2FzKJV5DQMh64wGiBzCDseXB6BYRpErshb1OzfvX9ysjBedEQXci7g3O6ZzU07GO8SyldMFlyOwF3NZmadhhZlxukJY9KN7UcMDT%2FJMCqrURHwedRsRTWcjokPw5KUeOzjzRwcZrkqW6Uu7laDw2yfVVaiJCzEUtOopN%2F44lGwDOzCMhqPUBjqkAbtunQbI%2BjSaVqaN3Z26GHuAIkng3Bc31jFAPySNC3kim%2FyKIHgGP4ceSNNyNvQEZkaDxRfLo5g1Me3zO9tPKT8bB4e2mTzbuRZWXExIzBgra1JeCGsOEfponqWcBhD3RDqf6tNTKVPPwzL2aaArMP7DgyDo4fi99YzNTEyrsGZ%2BkAo4a25J0qRCcYBd8bqUFqx4UE%2BVLah7jZSlTxZHWELHzNLS&X-Amz-Signature=274d44eeead5d507e05dd7c9f614b94726f7fc09d664486d883e593b7e4366d8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
