# Race condition

## Contents

- [Limit overrun race conditions        ](./Limit_overrun_race_conditions/README.md)
- [Bypassing rate limits via race conditions](./Bypassing_rate_limits_via_race_conditions/README.md)
- [Multi-endpoint race conditions](./Multi-endpoint_race_conditions/README.md)
- [Single-endpoint race conditions](./Single-endpoint_race_conditions/README.md)
- [Exploiting time-sensitive vulnerabilities](./Exploiting_time-sensitive_vulnerabilities/README.md)
- [Partial construction race conditions](./Partial_construction_race_conditions/README.md)

### **What is a race condition?**

A race condition is when an application attempts to execute multiple independent processes (“threads”) simultaneously to accomplish multiple tasks at once rather than performing in the appropriate sequence. While running multiple processes (“multi-threading”) improves application performance by using computing resources more efficiently, running them simultaneously creates problems when both processes attempt to access the same resource at the same time, causing what’s known as a “collision.”

It occur when two computer program processes, or [threads](https://www.techtarget.com/whatis/definition/thread), attempt to access the same resource at the same time and cause problems in the system.

Race conditions are considered a common issue for multithreaded applications.

### Types of race conditions:

  - **Noncritical**: Both processes execute but cause no real issues with what the application does.
  - **Critical**: Both processes execute, which prevents the application from acting as intended  with unpredictable or undefined behavior. 
    - **Read-write-modify**: Both processes access the resource and return a different value, undermining data integrity.
    - **Check-then-act**: Both processes check a value, but the first one changes, which means the other process reads the value as null.

### **Examples of race conditions?**

In computer memory or storage, a race condition may occur if commands to read and write a large amount of data are received at almost the same instant, and the machine attempts to overwrite some or all of the old data while that old data is still being read. The result may be one or more of the following:

  - the computer crashes or identifies an illegal operation of the program
  - errors reading the old data
  - errors writing the new data

**A race condition can also occur if instructions are processed in the incorrect order.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10d8fb1b-688c-4acb-9e9d-139215f8662a/image1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662ZJFSCB2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215651Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHGs5%2BT%2BMH3LFrQK%2BwJhuY3CZRQkWaLW1I9kLD0vNuXvAiEA6QzKe9hfUJIZEipCtU11I0F2%2BrVL0yora6dzPkTE0yAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOsFRfCiBuhYYm5yYyrcAxad45AYU9GsGXVlM1ZUg4TuZMQsdQKr1IVDOy1NFLc%2FoVZEZr8oUq7GTaePfzvZKtO4J3kJff3vp%2FBDiyzLBVZlIwDu%2BhzsBeiCii9XgDhMF5qR5Xv1tprp4%2BbYFD3g4wbl4kw4q8dzEGGsV3qluELhTVXVIagZMOoRora0Cch9CcWF0VldbZpB%2FLMvBPWYCQSypoDOI2gYF1B8cP%2BM4MgbByEVxQtdCBoDUI2RR455wOaQC565w5y6vA3JWcaMPqiKh4yesBGjqmMNxoZhtIAy%2B5U2k%2FwKX8Zw6nb3Pn%2BE7sxhoU5wU73okEF7GwSH1P6ApV4ms5RRYE2QwaUSpnqAiiGGHm2KwpYkohGX1JoaHTKbo8s9FcOGNgb8xXSX0S4%2Fvw8FTtja5UIlh8WEpr%2F1DZE9AqK%2B5dPFKwDxMZJ82WJeaK2rFX5TzjlXyp1aTSZ1B3r3VmCWJBDACgDz%2Baxvr0JB1sLL90setrIeHVcXxvXALvTy8G2g%2BKmgCvYJ%2FklLezeulFSAAUQUUGtOWpso%2Bx28H3jIyEFUvKNS35M2LZYyjCgoxVmp%2F7fOjGjmzZsTNcfqGb1jqzsGPhsubvo9JtA2fybwNqG5%2FuWYaE6V%2BuEWcY6Yvyxr5cvuMIaEo9QGOqUB%2FgYVdsLHCLAme81q1xCOcirlA8WYL%2FvzVgJEZSOgFHKRjgo49%2FRlSoDNL8ZKzj6B2PUGYFvEt2eYjq3KOjDLFlqGvBgYT4BuWADljEufKbBJ1tRdWP35isRCgV9GcgzkghmfTbRkkdxeIEdW7Vllm30BvCtUY6n%2FdzN7m39NsKqnuNHlD85xBLcwx9el3vBEv5OODmKP%2B9tW11Y9QRwPgMcts4a5&X-Amz-Signature=72da8e06226132233a92906e536f575433b3731970db953fe6cde5ebe68a5fda&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 1. Process 1 performs a bit flip, changing the memory value from 0 to 1. Process 2 then performs a bit flip and changes the memory value from 1 to 0.*

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7d437d1f-db53-427c-83d4-48f53a1d1ad8/image2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RVHO7G4B%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215651Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGOGA6VE%2B29Ut2iwv3rLyAi1lbm9s4dfWRncp1Gy2RQOAiAMxGTgFbmZrG5%2FGt3MWZ2rUsoni3DtF0KhT%2BWmz0KbBSqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMolWvQ1gYyQJt8w5NKtwDc%2FZOxTJk%2B8AmPYTNCrmVNfHrE4pZeMMXOySPzFbCJi%2B6xJQ%2BL9zxn8SONSHvjkuTbBI2sokHQ%2BSq24WgCn1kbZLYAbaT7mlAs6ERUehno3yDn1e8A%2BybkuL%2BHok2h%2FpVuHpVxS2w7N0OXT%2Fv64FamNdwPG91nXU9DEntUxG7a4vVSVVOBjQ8E%2BnsguMd47a2a20N5wrtrxInG2pV5oGeyA2lrbXoEJDj9M%2F1o1bCVZRS4Pz%2B9plN71pR7ZyazuJc8%2Fl7F2SXTowlfE80LqlIumYGPJT9rIMUsZv14HOpZ%2B0X8vSUap6CLDjbAj7IhxKhd%2BkvW4Q6k3HsPgFUxjd32Sd6tK3hU%2BVtoikJsMv7ZcAR3if9YazgsQw2tdd8XltsBGg5nAj6%2FDPDgclGGZRvppIu8tS7lbPgqAYiDnS7HCjoOJ%2BLGlevlS6R%2BUzTCuKAG8BzvpbAw0kzmDVgR2KnM4xF5jHGP3tZcCQ4KBwd%2B9NVi3H4QOwX3MzpjuYvsjITPOf1CDKijRVfPbY4IHA0HXNDp0wfzYPOEkvJDVeiJNIP2VPXMzzAEMNyLKVUkCMvsd2E2a8%2Ft5hXDxVuomfLWNWWqvAnFawt6QJNNUKGhpOQ%2BWJFSFdgYbfMVv4wsYSj1AY6pgF%2F%2F8yxW2Z%2B%2FJqkZG5UzIkCDwjo%2FW4Km3FiO7cidZ0eYPlEqo9GptVU0ed3lZzXZqda7iOeOXKCh9sPwUfpjj3b418m3WR4eWMGOLhvxuKvG9hDvOP3BgLIVsKnXICllgxAgcW6edgNVFJi%2Ff%2BpeHTZ2Q7deQVHlDA%2FiLqAEsok5UQXhWJpjsRVz1P3dM2sUoqkHcbijnHMBl0Kc0wBno7XiFOFqz1K&X-Amz-Signature=ccc5a5587beda820d8d5c7bd8a65f515dcbc249416d31e39f3054af27f5b0b41&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 2. When Process 2 is unaware that Process 1 is performing a simultaneous bit flip, the bit has an ending value of 1 when its value should be 0.*

Suppose two processes need to perform a bit flip at a specific memory location. Under normal circumstances the operation should work as shown in Figure 1.

If a race condition occurred causing these two processes to overlap, the sequence of operations could potentially look more like what's shown in Figure 2.

Race conditions occasionally occur in [logic gates](https://www.techtarget.com/whatis/definition/logic-gate-AND-OR-XOR-NOT-NAND-NOR-and-XNOR) when inputs come into conflict. Because the gate output state takes a finite, nonzero amount of time to react to any change in input states, sensitive circuits or devices following the gate may be fooled by the state of the output and not operate properly.

> **Read-modify-write.** This kind of race condition happens when two processes read a value in a program and write back a new value. It often causes a software bug. Like the example above, the expectation is that the two processes will happen sequentially -- the first process produces its value and then the second process reads that value and returns a different one.

For example, if checks against a checking account are processed sequentially, the system will make sure there are enough funds in the account to process check A first and then look again to see if there are enough funds to process check B after processing check A. However, if the two checks are processed at the same time, the system may read the same account balance value for both processes and give an incorrect account balance value, causing the account to be overdrawn.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e175e155-8943-4713-b3cf-f21afb0f87b3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665I3FEXDL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215650Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIB9Q4O9wqJ3dGSc06yZ9c9q4xvSfcyC9TtgRaxUzDHFwAiEA3hLRzkDp%2BLcVRpRGZ%2BrUhYkFz2HvPwPXSdQoRB0ZkPcqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIWDJpxf5XlAZqY7uyrcA2rK7SuvV5kDfRegXVmqFnE4O5hJx7CuwBeiHRiyUUokfIR1uy%2B6yP5SkQt9qWbsFA906FpwTHAPtY9klR%2BiVLkApeJHLbti%2BfcaUGV%2FquPM6%2FbP%2Bla6qsmKsV%2BfUsbYOGwXW1znxUzUP%2B6uo%2B2ICqQYhlcWp%2BzD7AhxBzD%2B3a5H00l2bzC3b3nWLdZznYPebRggQswXjM9bozIHydh20kXYZ17LqayW09oIvg2XIj2h4pEieBWMq5%2FFxJHX8KySxMI2SFb8L6Km8C3zlBe0gFY49ecks5aqUCBEUklgy344xxEST3d1n7T0MEjOwvd28t%2FIdWMnlNFbkfQQwGek1bqKfS%2BFCoug25F7S7MgRZPC5LVWqIfEd4xeBNmukMqhMo%2BkvBhw8aUpl0YpGGeqy526TfosiGK2lIOI8tY1I%2FsVhepErGAoqY3wZpHGtDiRgTcfEopQ3g2FyPuvJzLWmFSew6HYaY8c%2FGysfrV9CFkwqcRb0%2F%2FYnG6DTj%2BCIYWyjY30iXlMb2WNdjO5SuKR1i2v4fRRE7sub4381NcpQ3ZKAqJ2zrttKEB4V8mB77VA0MEb83VY2HM9vqf2nRBmzP82sfuDii6rptVIqrbmGEyJv4XnFt7xVJ7HIy%2FbMKSGo9QGOqUBKuqT1VAS7i8FNTMcx3RZwODPLPpELZRLuu%2BoerGICBCs2c2F%2FCwIW0ZUjJcMQ7Rb%2F%2BeL%2BopriWaUekBxfMy3Z7LPEqFZ54APBSXodn9i2V79KIQNzgSqorF3wkrq25zxrdKjiG8UTbckQypmhoFUcJjbEy9JX%2FxCDdFI1Cz92gBlhrwO%2FMRKNJeqYhfhs%2FTKm7Iabre5rmGGk3Ws00KgaUE2T8hF&X-Amz-Signature=5f6e98644a8db5ac5c16b712fef85ac213083aad5ba0c0eaf4592248c285087a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*See how a race condition could develop if a bank receives two checks -- one for $1,000 and the other for $1,500 -- at about the same time, both drawn against a checking account with only $2,000 in it.*

> **Check-then-act.** This race condition happens when two processes check a value on which they will take each take an external action. The processes both check the value, but only one process can take the value with it. The later-occurring process will read the value as null. This results in a potentially out-of-date or unavailable observation being used to determine what the program will do next. For example, if a map application runs two processes simultaneously that require the same location data, one will take the value first so the other can't use it. The later process reads the data as null.

## Limit overrun race conditions

The most well-known type of race condition enables you to exceed some kind of limit imposed by the business logic of the application.

For example, consider an online store that lets you enter a promotional code during checkout to get a one-time discount on your order. To apply this discount, the application may perform the following high-level steps:

  1. Check that you haven't already used this code.
  1. Apply the discount to the order total.
  1. Update the record in the database to reflect the fact that you've now used this code.

If you later attempt to reuse this code, the initial checks performed at the start of the process should prevent you from doing this:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1e3a0241-6bcc-41c9-ac1d-f6152bc46418/image1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665I3FEXDL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215650Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIB9Q4O9wqJ3dGSc06yZ9c9q4xvSfcyC9TtgRaxUzDHFwAiEA3hLRzkDp%2BLcVRpRGZ%2BrUhYkFz2HvPwPXSdQoRB0ZkPcqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIWDJpxf5XlAZqY7uyrcA2rK7SuvV5kDfRegXVmqFnE4O5hJx7CuwBeiHRiyUUokfIR1uy%2B6yP5SkQt9qWbsFA906FpwTHAPtY9klR%2BiVLkApeJHLbti%2BfcaUGV%2FquPM6%2FbP%2Bla6qsmKsV%2BfUsbYOGwXW1znxUzUP%2B6uo%2B2ICqQYhlcWp%2BzD7AhxBzD%2B3a5H00l2bzC3b3nWLdZznYPebRggQswXjM9bozIHydh20kXYZ17LqayW09oIvg2XIj2h4pEieBWMq5%2FFxJHX8KySxMI2SFb8L6Km8C3zlBe0gFY49ecks5aqUCBEUklgy344xxEST3d1n7T0MEjOwvd28t%2FIdWMnlNFbkfQQwGek1bqKfS%2BFCoug25F7S7MgRZPC5LVWqIfEd4xeBNmukMqhMo%2BkvBhw8aUpl0YpGGeqy526TfosiGK2lIOI8tY1I%2FsVhepErGAoqY3wZpHGtDiRgTcfEopQ3g2FyPuvJzLWmFSew6HYaY8c%2FGysfrV9CFkwqcRb0%2F%2FYnG6DTj%2BCIYWyjY30iXlMb2WNdjO5SuKR1i2v4fRRE7sub4381NcpQ3ZKAqJ2zrttKEB4V8mB77VA0MEb83VY2HM9vqf2nRBmzP82sfuDii6rptVIqrbmGEyJv4XnFt7xVJ7HIy%2FbMKSGo9QGOqUBKuqT1VAS7i8FNTMcx3RZwODPLPpELZRLuu%2BoerGICBCs2c2F%2FCwIW0ZUjJcMQ7Rb%2F%2BeL%2BopriWaUekBxfMy3Z7LPEqFZ54APBSXodn9i2V79KIQNzgSqorF3wkrq25zxrdKjiG8UTbckQypmhoFUcJjbEy9JX%2FxCDdFI1Cz92gBlhrwO%2FMRKNJeqYhfhs%2FTKm7Iabre5rmGGk3Ws00KgaUE2T8hF&X-Amz-Signature=d364ede9e89ee8593ea429984a965050e9fa987be1229355810ed04c426e49b5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now consider what would happen if a user who has never applied this discount code before tried to apply it twice at almost exactly the same time:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce41f6a9-5e2d-4e47-9abc-0a26de9798f4/image2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665I3FEXDL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215650Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIB9Q4O9wqJ3dGSc06yZ9c9q4xvSfcyC9TtgRaxUzDHFwAiEA3hLRzkDp%2BLcVRpRGZ%2BrUhYkFz2HvPwPXSdQoRB0ZkPcqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIWDJpxf5XlAZqY7uyrcA2rK7SuvV5kDfRegXVmqFnE4O5hJx7CuwBeiHRiyUUokfIR1uy%2B6yP5SkQt9qWbsFA906FpwTHAPtY9klR%2BiVLkApeJHLbti%2BfcaUGV%2FquPM6%2FbP%2Bla6qsmKsV%2BfUsbYOGwXW1znxUzUP%2B6uo%2B2ICqQYhlcWp%2BzD7AhxBzD%2B3a5H00l2bzC3b3nWLdZznYPebRggQswXjM9bozIHydh20kXYZ17LqayW09oIvg2XIj2h4pEieBWMq5%2FFxJHX8KySxMI2SFb8L6Km8C3zlBe0gFY49ecks5aqUCBEUklgy344xxEST3d1n7T0MEjOwvd28t%2FIdWMnlNFbkfQQwGek1bqKfS%2BFCoug25F7S7MgRZPC5LVWqIfEd4xeBNmukMqhMo%2BkvBhw8aUpl0YpGGeqy526TfosiGK2lIOI8tY1I%2FsVhepErGAoqY3wZpHGtDiRgTcfEopQ3g2FyPuvJzLWmFSew6HYaY8c%2FGysfrV9CFkwqcRb0%2F%2FYnG6DTj%2BCIYWyjY30iXlMb2WNdjO5SuKR1i2v4fRRE7sub4381NcpQ3ZKAqJ2zrttKEB4V8mB77VA0MEb83VY2HM9vqf2nRBmzP82sfuDii6rptVIqrbmGEyJv4XnFt7xVJ7HIy%2FbMKSGo9QGOqUBKuqT1VAS7i8FNTMcx3RZwODPLPpELZRLuu%2BoerGICBCs2c2F%2FCwIW0ZUjJcMQ7Rb%2F%2BeL%2BopriWaUekBxfMy3Z7LPEqFZ54APBSXodn9i2V79KIQNzgSqorF3wkrq25zxrdKjiG8UTbckQypmhoFUcJjbEy9JX%2FxCDdFI1Cz92gBlhrwO%2FMRKNJeqYhfhs%2FTKm7Iabre5rmGGk3Ws00KgaUE2T8hF&X-Amz-Signature=302f8861e677fe37489775c8377dd0ad749238556e248ac1c5eb480dbe64c15e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

There are many variations of this kind of attack, including:

  - Redeeming a gift card multiple times
  - Rating a product multiple times
  - Withdrawing or transferring cash in excess of your account balance
  - Reusing a single CAPTCHA solution
  - Bypassing an anti-brute-force rate limit

Limit overruns are a subtype of so-called "time-of-check to time-of-use" (TOCTOU) flaws.

### **What security vulnerabilities do race conditions cause?**

A program that is designed to handle tasks in a specific sequence can experience security issues if it is asked to perform two or more operations simultaneously. A threat actor can take advantage of the time lapse between when the service is initiated and when a security control takes effect in order to create a deadlock or thread block situation.

A deadlock vulnerability is a severe form of a [denial-of-service](https://www.techtarget.com/searchsecurity/definition/denial-of-service) vulnerability. It can be made to occur when two or more threads must wait for one another to acquire or release a lock in a circular chain. This situation results in deadlock, where the entire software system comes to a halt because such locks can never be acquired or released if the chain is circular.

Thread block can also dramatically impact application performance. In this type of concurrency defect, one thread calls a long-running operation while holding a lock and preventing the progress of other threads.

### **How to identify race conditions**

Programmers use dynamic and static analysis tools to identify race conditions. [Static testing](https://www.techtarget.com/searchsoftwarequality/definition/static-testing) tools scan a program without running it. However, they produce many false reports. Dynamic analysis tools have fewer false reports, but they may not catch race conditions that aren't executed directly within the program.

Race conditions are sometimes produced by data races, which occur when two threads concurrently target the same memory location and at least one is a write operation. Data races are easier to detect than race conditions because specific conditions are required for them to occur. Tools, such as the Go Project's Data Race Detector, [monitor for data race situations](https://golang.org/doc/articles/race_detector). Race conditions are more closely tied to application semantics and pose broader problems.

### **How do you prevent race conditions?**

  - **Avoiding shared states:** Design code to minimize shared resources and use atomic operations or locking mechanisms.
  - **Immutable objects:** Use objects that cannot be altered after creation.
  - **Thread synchronization:** Ensure only one thread executes a specific code section at a time.
  - **Serialization:** Order read and write operations to avoid conflicts. (e.g., in storage access)
  - **Priority schemes:** In networking, prioritize access requests to prevent collisions.
