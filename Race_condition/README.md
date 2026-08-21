# Race condition

## Contents

- [Limit overrun race conditions        ](./Limit_overrun_race_conditions.md)
- [Bypassing rate limits via race conditions](./Bypassing_rate_limits_via_race_conditions.md)
- [Multi-endpoint race conditions](./Multi-endpoint_race_conditions.md)
- [Single-endpoint race conditions](./Single-endpoint_race_conditions.md)
- [Exploiting time-sensitive vulnerabilities](./Exploiting_time-sensitive_vulnerabilities.md)
- [Partial construction race conditions](./Partial_construction_race_conditions.md)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10d8fb1b-688c-4acb-9e9d-139215f8662a/image1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666DURXU3N%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222123Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDYLNWNFQqLYC%2FSTp8iGd6VOZKnwvo3uTfgv0TkY%2F8d6wIhANRnHk7AtYbp9x5nHkT0Q2kKFURKp8fTIyiMeHnGC5zxKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzoqPn%2BwOTWlZcrWr0q3AMlXpPVSQLm0G2HCYn8adgb0PS%2FmaDZlk5LdVs31QtkxnnPslhTIn4utznoiFQ9BOMqahUJhTnpsFxX4rOFUHsYfk58GBlmZ8ueg01OgoVErtqVsWnZPQz8h0z6b1vf6pM4viDYGCfoS5GweNjIPIkOK69L73k1WwTy4Ny69RV6W0gie92fL4BwZ26L0B10pV29MkAmkOwKYJ67Pd1Ssy9bQ9zM%2BE46TiLRythP9t7Oigq%2Big3BsFkoyrQ68JVapQHJT7hNaamlC9P1Hobzw7yKhKEhXQoyKd%2F31L5VFZI8Gv%2BEjKAEvbPSjsY8x%2B%2BpBrfCDILT%2B16YFimFpFP5Ukt8xunQY6M28zY9WtTMgrnlk%2FtfeWUvtqvCWhnD%2FNQJMfR29GXBEp%2Bsm7MNywhYxzhyz2R3N45tzfRDIDv9jDpAr3GCZ%2B%2B5zA21iNGM6z3m8LO8WtIKK2SyT3ZNlLdqoS8%2FshdCMk6UX1t62FQHibG2uwRH1pFqWyu3n6Wp3fzgiFlJOMwy2P4%2BzLPka%2B7HuH7PANW6od4KWrZup7e5lh%2FgxKyqzyBizYYirIAKcAsvYplSw66eYmog8ib43VmOh%2Bbxcfkj0OzvDmdtI370onFyGaTVFi0RUMIPPMErbzDPhaPUBjqkAZGZ7k9ZwPwZBigQ7oUvMZWGuvXzJ%2BlMCxyKLL7DH4RdjWdHrS9zpaegp5YMiOcOLn%2BDfKydrtlNF7KtJj3blfduBW1UwGc7X5KdXJKB5NqCrWiCplRt3p%2FrfUmg7mQGzQs9xmVgN2yeHK%2BbrA0WYGDQNHhTt%2FAjTbP5xMTGWCQeBFcTp%2FvNkI3lkCZXqZcomLnQ1Yk%2FH92vVCTS4EMThi94%2B83C&X-Amz-Signature=866c93b3362c54f4e9b0a7bd2727fb0ced615d8da6d5b6022d3f46b1f5a3c2e0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 1. Process 1 performs a bit flip, changing the memory value from 0 to 1. Process 2 then performs a bit flip and changes the memory value from 1 to 0.*

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7d437d1f-db53-427c-83d4-48f53a1d1ad8/image2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZXXA424P%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222124Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC1p6RBQytUeHV6C9cXmAT7%2Br6PnHb2KOpPd87SqUVdKgIhAINLEcxgAr%2FJX3n6bqaY5hx5qRWRSmnBD0TKz2Ou%2BC3vKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxxB7gtdvWCXwJXpvQq3AMLPpXxo9nBU%2BLznrV41yKlP%2BgNo8TWe2Nw8OPKgX0fAtLFyrWkOcBh8lptLujAzc7t3GS4b9HIB50jIO6Z21jWxDMLem9Y9JNSXnKEMej%2Fpp6mL%2FSfYGzGupvAExUDUeYhojWaMEr0s79dCn%2BFyyiJOglYx2LjoGVu2GHy9q49lmiXW6kfsUkXeWWls0GVvfzasDQbtFDG2YWbsSrNKitg%2FE5%2BZ%2BhZ9asNCEfqfgx0Vk%2BKAaJAHz6JyXzR22mtYhU0RKy8t5nOW8S%2BJ1Uyxce839qgyGNOcO3j0J5izTHqTy%2FyGfcpSy4GWKoHd73vF1WgKMh7N2YfGYwlvh6DedlI3%2FuZ4vyk5EQQah6liQ5KV4oQAyr%2FuO4AXmJju715FRS%2FFQ0lmdNl5ctj72oGKlfihbylbD2xZtpOkFcVKt5RkJx%2FgWw%2B9gHfCpyQ9%2FFHpT7VzxGf7ljepgfcivqxGXLHDkbJOkd5l%2B%2BmzqTNQXoiXugGE8Uy9EzUAGYCeTADQaQBlt93AZ7xELSbErdNaX2KNBK%2FoaA65JwdU0lcyALEIno0l6aGZeA%2FijbhdPbpdT3r0kDI5uuWqtUCjrp6WXX2Ekc2UjMnEVTclR7quH0o2rS5KhleqRbZEX9k8TDgg6PUBjqkAXzRtEaUufjg%2FT2Xexr0x0Bt4X2H1yS1q5y6fihFf%2FbSazj8IpMySRzq1ty3f5fyl37YOT3Wj73q26VJ8pbLDhJ3UMjhzLnOO0Nq%2FW9mAUWGwqdWSoLJ9jH%2BpHrzSoOFk%2FDgCR%2BAjfYnmYgtAwZsLs8S99OyZqpK3REykmmzvrpq9lttRBBnouWjw4wKXsGy8YnJ2X%2BHqCgmk4zB59Zs4cnU0I1d&X-Amz-Signature=58b2eb0d7efef99fd70632c0705bfeef00317d303b8ef0b6a6e89a33c091fd09&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 2. When Process 2 is unaware that Process 1 is performing a simultaneous bit flip, the bit has an ending value of 1 when its value should be 0.*

Suppose two processes need to perform a bit flip at a specific memory location. Under normal circumstances the operation should work as shown in Figure 1.

If a race condition occurred causing these two processes to overlap, the sequence of operations could potentially look more like what's shown in Figure 2.

Race conditions occasionally occur in [logic gates](https://www.techtarget.com/whatis/definition/logic-gate-AND-OR-XOR-NOT-NAND-NOR-and-XNOR) when inputs come into conflict. Because the gate output state takes a finite, nonzero amount of time to react to any change in input states, sensitive circuits or devices following the gate may be fooled by the state of the output and not operate properly.

> **Read-modify-write.** This kind of race condition happens when two processes read a value in a program and write back a new value. It often causes a software bug. Like the example above, the expectation is that the two processes will happen sequentially -- the first process produces its value and then the second process reads that value and returns a different one.

For example, if checks against a checking account are processed sequentially, the system will make sure there are enough funds in the account to process check A first and then look again to see if there are enough funds to process check B after processing check A. However, if the two checks are processed at the same time, the system may read the same account balance value for both processes and give an incorrect account balance value, causing the account to be overdrawn.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e175e155-8943-4713-b3cf-f21afb0f87b3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LICXFL6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222123Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIE90c2ur5Y4MICFaBxqKr%2F1SEr6ob81bQpLJfgUto77HAiAhP5E0%2FBTenX5cAZPxImIOzQgmhuQ3UO1P2xWTj1CgkCqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMExQz6mMoBBfjp1s0KtwDBoknkiCIZtNjhOCljB7Yh2t0ZQ4RN%2Fm1cSPjk9y1TZ9jdhFM7DaZ2BdgAOUaGGIGmDmCeyo2YJRGAlHv5Loi2rl3OfZKrs%2BKYvCkl1TzXl%2FRSoU2CQrO%2BC3U%2B2BQltE%2F6vnXoK4PHV7Zdu08%2BF05q9US%2B6W%2B%2FaHHXITWCu7tUkYEzTl8h5Kkalb9znD%2F%2B6G%2Fe6rgPbxAmvUNcCZCan2%2FAB0j2U7tvig2SX0WPamkMC1QoqYNMLTltzzFqkwRfOOM9YuCEMRf%2FAjzAamhyTxaw27jpYHBTa2weKOalLF34z1pqnI%2F%2FhHvqnw0ycUZMOqXXQMcO5HX%2F79yhOJ3aH6tzMrlawLii%2F9PzT4RFVHtQX%2BZQkaKbowiZC8JZqCs8NQiM%2FLXWlWRXGEssQK2C01pLdMEeTrOXYNxqKL4XdiCCdx8vbrIK%2BMmbKd7sgCrpYsSIIINBiOYZQEUoTeBlFzvzsvR%2BrRTvPPNB%2FnQRpWmMovvsYF%2BHdtqu3vqs01dl8gipUpeg3YPIjvLs38MtvtBQWmcY9ZMTTL7nXPufN0vZkKIzyzYRgK20sll7PXr8RjoQGOQXWzwlVtXHJl%2BLOEBGeZh1jauCf18awQHbQvonu0PI0JEHU9XU6wtzE4wsoSj1AY6pgGfsD%2FtneRCRWu%2Bte9bT0WOZjeh96hQmR1Vdu8Oc%2Be%2BEYhETtbX1zQDoTo7fjcxuDKculn3VejSs3Apkjv3Ix0IDrMSIm8Kc8%2BzQjiFd09RO8SMzQBERGUabpWjpHXg20zKSA1VjsrYc2DNKHgyGMUSU5nsqCv6kqVRmXaIduk0y1fokyDIUhlHmv9EVxSESNBqH6p6rEaj0w%2FhkcNPFQNDKc%2FQd%2FcL&X-Amz-Signature=709ff16aa480b5c60d51debadb13b4762b33095f366d41dd90781cf8685079ba&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*See how a race condition could develop if a bank receives two checks -- one for $1,000 and the other for $1,500 -- at about the same time, both drawn against a checking account with only $2,000 in it.*

> **Check-then-act.** This race condition happens when two processes check a value on which they will take each take an external action. The processes both check the value, but only one process can take the value with it. The later-occurring process will read the value as null. This results in a potentially out-of-date or unavailable observation being used to determine what the program will do next. For example, if a map application runs two processes simultaneously that require the same location data, one will take the value first so the other can't use it. The later process reads the data as null.

## Limit overrun race conditions

The most well-known type of race condition enables you to exceed some kind of limit imposed by the business logic of the application.

For example, consider an online store that lets you enter a promotional code during checkout to get a one-time discount on your order. To apply this discount, the application may perform the following high-level steps:

  1. Check that you haven't already used this code.
  1. Apply the discount to the order total.
  1. Update the record in the database to reflect the fact that you've now used this code.

If you later attempt to reuse this code, the initial checks performed at the start of the process should prevent you from doing this:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1e3a0241-6bcc-41c9-ac1d-f6152bc46418/image1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LICXFL6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222123Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIE90c2ur5Y4MICFaBxqKr%2F1SEr6ob81bQpLJfgUto77HAiAhP5E0%2FBTenX5cAZPxImIOzQgmhuQ3UO1P2xWTj1CgkCqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMExQz6mMoBBfjp1s0KtwDBoknkiCIZtNjhOCljB7Yh2t0ZQ4RN%2Fm1cSPjk9y1TZ9jdhFM7DaZ2BdgAOUaGGIGmDmCeyo2YJRGAlHv5Loi2rl3OfZKrs%2BKYvCkl1TzXl%2FRSoU2CQrO%2BC3U%2B2BQltE%2F6vnXoK4PHV7Zdu08%2BF05q9US%2B6W%2B%2FaHHXITWCu7tUkYEzTl8h5Kkalb9znD%2F%2B6G%2Fe6rgPbxAmvUNcCZCan2%2FAB0j2U7tvig2SX0WPamkMC1QoqYNMLTltzzFqkwRfOOM9YuCEMRf%2FAjzAamhyTxaw27jpYHBTa2weKOalLF34z1pqnI%2F%2FhHvqnw0ycUZMOqXXQMcO5HX%2F79yhOJ3aH6tzMrlawLii%2F9PzT4RFVHtQX%2BZQkaKbowiZC8JZqCs8NQiM%2FLXWlWRXGEssQK2C01pLdMEeTrOXYNxqKL4XdiCCdx8vbrIK%2BMmbKd7sgCrpYsSIIINBiOYZQEUoTeBlFzvzsvR%2BrRTvPPNB%2FnQRpWmMovvsYF%2BHdtqu3vqs01dl8gipUpeg3YPIjvLs38MtvtBQWmcY9ZMTTL7nXPufN0vZkKIzyzYRgK20sll7PXr8RjoQGOQXWzwlVtXHJl%2BLOEBGeZh1jauCf18awQHbQvonu0PI0JEHU9XU6wtzE4wsoSj1AY6pgGfsD%2FtneRCRWu%2Bte9bT0WOZjeh96hQmR1Vdu8Oc%2Be%2BEYhETtbX1zQDoTo7fjcxuDKculn3VejSs3Apkjv3Ix0IDrMSIm8Kc8%2BzQjiFd09RO8SMzQBERGUabpWjpHXg20zKSA1VjsrYc2DNKHgyGMUSU5nsqCv6kqVRmXaIduk0y1fokyDIUhlHmv9EVxSESNBqH6p6rEaj0w%2FhkcNPFQNDKc%2FQd%2FcL&X-Amz-Signature=9fcac3f72b573a460d5f8754e2277e87e80211c6bfe047743db36943c26ae6d1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now consider what would happen if a user who has never applied this discount code before tried to apply it twice at almost exactly the same time:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce41f6a9-5e2d-4e47-9abc-0a26de9798f4/image2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LICXFL6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222123Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIE90c2ur5Y4MICFaBxqKr%2F1SEr6ob81bQpLJfgUto77HAiAhP5E0%2FBTenX5cAZPxImIOzQgmhuQ3UO1P2xWTj1CgkCqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMExQz6mMoBBfjp1s0KtwDBoknkiCIZtNjhOCljB7Yh2t0ZQ4RN%2Fm1cSPjk9y1TZ9jdhFM7DaZ2BdgAOUaGGIGmDmCeyo2YJRGAlHv5Loi2rl3OfZKrs%2BKYvCkl1TzXl%2FRSoU2CQrO%2BC3U%2B2BQltE%2F6vnXoK4PHV7Zdu08%2BF05q9US%2B6W%2B%2FaHHXITWCu7tUkYEzTl8h5Kkalb9znD%2F%2B6G%2Fe6rgPbxAmvUNcCZCan2%2FAB0j2U7tvig2SX0WPamkMC1QoqYNMLTltzzFqkwRfOOM9YuCEMRf%2FAjzAamhyTxaw27jpYHBTa2weKOalLF34z1pqnI%2F%2FhHvqnw0ycUZMOqXXQMcO5HX%2F79yhOJ3aH6tzMrlawLii%2F9PzT4RFVHtQX%2BZQkaKbowiZC8JZqCs8NQiM%2FLXWlWRXGEssQK2C01pLdMEeTrOXYNxqKL4XdiCCdx8vbrIK%2BMmbKd7sgCrpYsSIIINBiOYZQEUoTeBlFzvzsvR%2BrRTvPPNB%2FnQRpWmMovvsYF%2BHdtqu3vqs01dl8gipUpeg3YPIjvLs38MtvtBQWmcY9ZMTTL7nXPufN0vZkKIzyzYRgK20sll7PXr8RjoQGOQXWzwlVtXHJl%2BLOEBGeZh1jauCf18awQHbQvonu0PI0JEHU9XU6wtzE4wsoSj1AY6pgGfsD%2FtneRCRWu%2Bte9bT0WOZjeh96hQmR1Vdu8Oc%2Be%2BEYhETtbX1zQDoTo7fjcxuDKculn3VejSs3Apkjv3Ix0IDrMSIm8Kc8%2BzQjiFd09RO8SMzQBERGUabpWjpHXg20zKSA1VjsrYc2DNKHgyGMUSU5nsqCv6kqVRmXaIduk0y1fokyDIUhlHmv9EVxSESNBqH6p6rEaj0w%2FhkcNPFQNDKc%2FQd%2FcL&X-Amz-Signature=7a40bbac2871fb31dc6fbf219d27a4afd9e180fdf84baef751268aac5409e61c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
