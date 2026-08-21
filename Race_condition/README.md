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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10d8fb1b-688c-4acb-9e9d-139215f8662a/image1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XKOT25AT%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBrv4Qq4s5HFGzINkHPZDet6JvxXl7tcp9pYXAHIhMafAiB7lR5VVixWej%2FibyP8CnwmxYOoI7h%2F%2Bta4bQOxov5DCSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMTE40M4OlJFapCpSnKtwDlLwqEupvW4kGNvGPydq3RpYU%2Bdao4LK3HBpRarPxmUiZ3ZF8mtJm5CnFNPWRM0UjvY7%2FwAF8jdms195jnNWcE%2BFKyMwOMtHpZQTKJuPisPvyVeX4MyfOObSLp2NXCXfsH1CCFkYUGRu5dHm0D1FSQIoLPU8KUhfJyZtvJGb7LEBKlQ83H5ruvmaerZwVeQcswMC8kR2jetxr4e%2BjKyoD12o6Im83PuaOuIAQSoIjPWb7V0kBhr0%2BgF6txEDAs%2FOeb8baSn9rP2t5a%2B58%2Fyxjtdrpf811ajO%2BmhxiVZCZ3gul0IjYAI3uF0GDUOHSPiQjB4HbMQ5FWT030KUlPG6S1C1xbuOKYB2N3kfhagWFQZeINPyjLh6dXhduUQUjkuf7IYrr1APYW50rlCpDAE8KmW2SplDCgbyFVOYT4iIcLGCbhYlS63xVv%2BE1m9304B3y0Ou%2FbtRE%2FYYA08K3YXd873t3gjWBkQUIcZHD5YA3jHnI%2BUpx7YqZ%2BK7Sj6twcSG7aKknzapJ6HiU9%2BpEGLzny4DAPo9YrqHn6IjVvGGbhK8ZUudbQrgs666RyBECHdoxWHbAayl8jaisxtVZKU0dJhTHm3at8bcafY0FmsUAKxHd5lDLYJjq2CCfQU8wkcai1AY6pgGsTQqgriA%2Bc3XamH5u7tr8NqggeABd8msKwNDDu%2FQRAFx4OtTDyi%2F9h3qQ8ZLMGNN9GiwXIFI1J9ZjpVYUmMXdB7Th1pA05o1yKkiQBDTPr%2BH7mblwnBFfE5czpOciqdFQnwFfNEhSe5MfD7AGomthSI7%2BpHAeI5hnOYhLYm4RuYKKS%2FoAc0WM6DPkYFMksUVQMZON%2BAYMMda%2Fx2tjyK8DhVi84A5f&X-Amz-Signature=6d6fc10c097189f42773dd157ed2db04293817c71334fda4005e6b07d08cbb3e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 1. Process 1 performs a bit flip, changing the memory value from 0 to 1. Process 2 then performs a bit flip and changes the memory value from 1 to 0.*

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7d437d1f-db53-427c-83d4-48f53a1d1ad8/image2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SSMGD64K%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210529Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIB7DBMql1%2BDV1cOO1vbYWOOEX%2FG8PaLho%2FFN4g4L5piSAiBj4ZirAeYulbvoWP4GSLtUqVbPlTbjIR%2FAshz9SOCgZCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMbUyJ2y6BTp304Lq9KtwDGWL8U7xvm60gqZbZfkP7ct6O2MsxqK%2BdEy%2Br81iSDvLM8mffYHoZoQ1%2BZ2Jid3C3amArYBgk5zo8zD4wOpzwLKS2%2Fpw4nhayxzV%2B9ElgvUreD%2FXqvGnX25khZteMMux2%2F3axfgXb827wLZEGy2m9FiOtd7zquknB8h%2B865fo3SFCt5fDzQu7Bud081n3dswHdEG2NFZHHWEn2NSniHlFaGyX029yhzAxj2kWPDgd4dvcp6jYmLVKPrnzsK4GP8gDDVK9RGRq5Caj26XQicEntKAvE3itv3htB2I2y%2F2w%2FR0StAqXXz%2FzG9fyTbz76vaOiPM6btI4uliTRdvc5qIqICXvNCWcZIYRxoZLeDq%2FKctAYBDXvX93gPTefBlXs4subosNTEjztm6tKVHqne0dDOILpzkw2HsdNbAd023VmpaN2V2tnkYfgghaY1cBgsN2VJP38LlAdlPT3iAMSa31YSL8IKJZSDj7SV8bZSAD8y%2BZUsj0vjYNw%2B4LfGsci%2BwR3%2FGEvlko77g0IvyzAPJ14OObCqpRcxUZwE8%2B6510UQcqQwlqXcTnq8ZvDBb16GJYpx9U3dO6JLhYORhEgktl1hBnsHGpJdg%2FZyeCqNcxxxxHvzXRGlM4yxn9uQQw%2FMqi1AY6pgGVaDYNCYmoFOiLUtsGcbu2gpZc1XoMBSX6pXtX2ER%2FpZXG%2FUAmG5SFFWMCULkMfbkjD2vOyQzlNqo6aE%2FGZy22nU8PlR7cbSv3dENL5C4DZvDloXkPGVDGgMgj8iJ4WdhoIrdUPeJCBNT6zVKqQOmljKMsojkemXM96jBbaYzqG6e1F19pqpAH6VU4YDh4kBKHVh4tVDvsHNHrk1nj3Lw%2FNR9lMOER&X-Amz-Signature=f5f013393eabede2a0dc2543f31fb3ee23b1a8fa0285ed4f2bcd055976d68bfc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 2. When Process 2 is unaware that Process 1 is performing a simultaneous bit flip, the bit has an ending value of 1 when its value should be 0.*

Suppose two processes need to perform a bit flip at a specific memory location. Under normal circumstances the operation should work as shown in Figure 1.

If a race condition occurred causing these two processes to overlap, the sequence of operations could potentially look more like what's shown in Figure 2.

Race conditions occasionally occur in [logic gates](https://www.techtarget.com/whatis/definition/logic-gate-AND-OR-XOR-NOT-NAND-NOR-and-XNOR) when inputs come into conflict. Because the gate output state takes a finite, nonzero amount of time to react to any change in input states, sensitive circuits or devices following the gate may be fooled by the state of the output and not operate properly.

> **Read-modify-write.** This kind of race condition happens when two processes read a value in a program and write back a new value. It often causes a software bug. Like the example above, the expectation is that the two processes will happen sequentially -- the first process produces its value and then the second process reads that value and returns a different one.

For example, if checks against a checking account are processed sequentially, the system will make sure there are enough funds in the account to process check A first and then look again to see if there are enough funds to process check B after processing check A. However, if the two checks are processed at the same time, the system may read the same account balance value for both processes and give an incorrect account balance value, causing the account to be overdrawn.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e175e155-8943-4713-b3cf-f21afb0f87b3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665B67U6BI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210528Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIA2RFtX3ArtL2dw03xQzgh2GMN2mue2Ic9Q6nI%2Ff2nssAiEAoIheMo90kB6PxXKOxpB8kqy5sZpyUNGy%2BfcGq4bzOBEqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI%2Fsn5BiCeNid6dhSircA6li%2B9xUkYkoFyC2%2F4PSlSjE0dqIo%2BRo871HGhaydbT%2BNVVjkBGZtl77r7PbaUNbjkDtw9h%2FQN9NQxRC1NfZFigRM10wsqIGp0iJJf9TD7tTVZEDdnFtJpEpy0EbkX%2B0ecoxmKcs7LhfiEmuP1loTFj%2FXNN2xXWSLP4W%2FWbQs0SUCLoQwQVyDteB8BGiwhbx1T58RDfn0qNGr7%2B8uHSIjiizq8g6bqcoxVa3eLr2mJPt2RQ27j7J74e0xVVnkicmP%2FydEScea4HeJb5zn2P9TuRMpM9XvpB2%2BC7f3C1jfaoSoSCocRRNVBjNNpht1XTFOC3yH65god0p%2BeGPbTTHJNNh4Bt9SdrDLOxVaf04afYhyTJuuKeWikuD9wmAu1y%2B33TZb1oIxF%2FSMHmKstx2HKmEtDQI7HKhJWonZOFtAimQPKCzzquM22FVHMLx3nG3lGlHUQ1JmrV2j4q7HkeKt7jawAFD80yZxK7IH1kL1o0%2BrrbZdSgjUG7imHmKdRUnEh%2BTyKqdXF4ojMehjr%2Bo0DO5DD2lXikK54ICKNNTs82UCenFqY%2BFDHzOC5eKnMYmzwoHun8a7%2FQRlDtyKZqdqa2f1swzeJYxkEQV90bbxLsRtJ4uc4AjoEk7unbeMMzGotQGOqUBgBJPgW%2FsGb1w6nKmAHfvf0Z5h1pSrBjkq8A5Mwgg2Ac0wk0ZEB0VYRj5Y10mW7owxkXtFOMTnrAueWUGUn3Vlx0F4ZJzZVuUpPKaa352g5%2B56hvxdjtDIRwxCXX1Gg0g0GD1JIyn3TEeDgCJsCaQGAWBr9ODkqXY%2BGzzZFbWbB%2BOxa0yNBj9zeXgEGusRJVp%2FKFgK0LMx%2FH87WjNvFvB76EUYkLa&X-Amz-Signature=7c95ece7fb17cc34a1ca128935e348de4f662e760c0bf97d53ac12ae1e0c33b9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*See how a race condition could develop if a bank receives two checks -- one for $1,000 and the other for $1,500 -- at about the same time, both drawn against a checking account with only $2,000 in it.*

> **Check-then-act.** This race condition happens when two processes check a value on which they will take each take an external action. The processes both check the value, but only one process can take the value with it. The later-occurring process will read the value as null. This results in a potentially out-of-date or unavailable observation being used to determine what the program will do next. For example, if a map application runs two processes simultaneously that require the same location data, one will take the value first so the other can't use it. The later process reads the data as null.

## Limit overrun race conditions

The most well-known type of race condition enables you to exceed some kind of limit imposed by the business logic of the application.

For example, consider an online store that lets you enter a promotional code during checkout to get a one-time discount on your order. To apply this discount, the application may perform the following high-level steps:

  1. Check that you haven't already used this code.
  1. Apply the discount to the order total.
  1. Update the record in the database to reflect the fact that you've now used this code.
If you later attempt to reuse this code, the initial checks performed at the start of the process should prevent you from doing this:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1e3a0241-6bcc-41c9-ac1d-f6152bc46418/image1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665B67U6BI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210528Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIA2RFtX3ArtL2dw03xQzgh2GMN2mue2Ic9Q6nI%2Ff2nssAiEAoIheMo90kB6PxXKOxpB8kqy5sZpyUNGy%2BfcGq4bzOBEqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI%2Fsn5BiCeNid6dhSircA6li%2B9xUkYkoFyC2%2F4PSlSjE0dqIo%2BRo871HGhaydbT%2BNVVjkBGZtl77r7PbaUNbjkDtw9h%2FQN9NQxRC1NfZFigRM10wsqIGp0iJJf9TD7tTVZEDdnFtJpEpy0EbkX%2B0ecoxmKcs7LhfiEmuP1loTFj%2FXNN2xXWSLP4W%2FWbQs0SUCLoQwQVyDteB8BGiwhbx1T58RDfn0qNGr7%2B8uHSIjiizq8g6bqcoxVa3eLr2mJPt2RQ27j7J74e0xVVnkicmP%2FydEScea4HeJb5zn2P9TuRMpM9XvpB2%2BC7f3C1jfaoSoSCocRRNVBjNNpht1XTFOC3yH65god0p%2BeGPbTTHJNNh4Bt9SdrDLOxVaf04afYhyTJuuKeWikuD9wmAu1y%2B33TZb1oIxF%2FSMHmKstx2HKmEtDQI7HKhJWonZOFtAimQPKCzzquM22FVHMLx3nG3lGlHUQ1JmrV2j4q7HkeKt7jawAFD80yZxK7IH1kL1o0%2BrrbZdSgjUG7imHmKdRUnEh%2BTyKqdXF4ojMehjr%2Bo0DO5DD2lXikK54ICKNNTs82UCenFqY%2BFDHzOC5eKnMYmzwoHun8a7%2FQRlDtyKZqdqa2f1swzeJYxkEQV90bbxLsRtJ4uc4AjoEk7unbeMMzGotQGOqUBgBJPgW%2FsGb1w6nKmAHfvf0Z5h1pSrBjkq8A5Mwgg2Ac0wk0ZEB0VYRj5Y10mW7owxkXtFOMTnrAueWUGUn3Vlx0F4ZJzZVuUpPKaa352g5%2B56hvxdjtDIRwxCXX1Gg0g0GD1JIyn3TEeDgCJsCaQGAWBr9ODkqXY%2BGzzZFbWbB%2BOxa0yNBj9zeXgEGusRJVp%2FKFgK0LMx%2FH87WjNvFvB76EUYkLa&X-Amz-Signature=2b97e9fc2e0399ad9b958058c91eefe54a8d7f411a677da467c1d2f39158ee79&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now consider what would happen if a user who has never applied this discount code before tried to apply it twice at almost exactly the same time:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce41f6a9-5e2d-4e47-9abc-0a26de9798f4/image2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665B67U6BI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210528Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIA2RFtX3ArtL2dw03xQzgh2GMN2mue2Ic9Q6nI%2Ff2nssAiEAoIheMo90kB6PxXKOxpB8kqy5sZpyUNGy%2BfcGq4bzOBEqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI%2Fsn5BiCeNid6dhSircA6li%2B9xUkYkoFyC2%2F4PSlSjE0dqIo%2BRo871HGhaydbT%2BNVVjkBGZtl77r7PbaUNbjkDtw9h%2FQN9NQxRC1NfZFigRM10wsqIGp0iJJf9TD7tTVZEDdnFtJpEpy0EbkX%2B0ecoxmKcs7LhfiEmuP1loTFj%2FXNN2xXWSLP4W%2FWbQs0SUCLoQwQVyDteB8BGiwhbx1T58RDfn0qNGr7%2B8uHSIjiizq8g6bqcoxVa3eLr2mJPt2RQ27j7J74e0xVVnkicmP%2FydEScea4HeJb5zn2P9TuRMpM9XvpB2%2BC7f3C1jfaoSoSCocRRNVBjNNpht1XTFOC3yH65god0p%2BeGPbTTHJNNh4Bt9SdrDLOxVaf04afYhyTJuuKeWikuD9wmAu1y%2B33TZb1oIxF%2FSMHmKstx2HKmEtDQI7HKhJWonZOFtAimQPKCzzquM22FVHMLx3nG3lGlHUQ1JmrV2j4q7HkeKt7jawAFD80yZxK7IH1kL1o0%2BrrbZdSgjUG7imHmKdRUnEh%2BTyKqdXF4ojMehjr%2Bo0DO5DD2lXikK54ICKNNTs82UCenFqY%2BFDHzOC5eKnMYmzwoHun8a7%2FQRlDtyKZqdqa2f1swzeJYxkEQV90bbxLsRtJ4uc4AjoEk7unbeMMzGotQGOqUBgBJPgW%2FsGb1w6nKmAHfvf0Z5h1pSrBjkq8A5Mwgg2Ac0wk0ZEB0VYRj5Y10mW7owxkXtFOMTnrAueWUGUn3Vlx0F4ZJzZVuUpPKaa352g5%2B56hvxdjtDIRwxCXX1Gg0g0GD1JIyn3TEeDgCJsCaQGAWBr9ODkqXY%2BGzzZFbWbB%2BOxa0yNBj9zeXgEGusRJVp%2FKFgK0LMx%2FH87WjNvFvB76EUYkLa&X-Amz-Signature=5e2fd000bc805c19d88cb84abf91c438deb69ded0473237c9a3e7614cc15ffc3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

