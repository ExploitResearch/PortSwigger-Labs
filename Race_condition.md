# Race condition


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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10d8fb1b-688c-4acb-9e9d-139215f8662a/image1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VRSZ6UIT%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204757Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBLalabWmkhOIRG5giSXHcg72%2F04cNgvRURcWmCUjyLGAiEAxaXlDqkmSV4evcaty29jQp8gXIndoFglx2TZE51nTU4qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAzREQgz7XRJrapirCrcA2aKlcza5ZJvhciPD6X2ZtR7YvsX08%2Fuj%2F5wa%2BoXyi5rQ%2BwIzTJpKk%2FCW6ONZB%2BjTEDDDWw%2BWW8ZtCoJH6vTUu%2B1LnFxQEEAruiX0QkIHilz3RQH4hqlQYMUF4xSN8TRgD27QWpJWnw3crakwFcX1T5Si2wm2v8dL%2F%2FLdWC3JnVKzI9Fx%2F6%2BDGE%2BUsqXrUXnt9Yrwg0QZ6u9ZhAAVwN2c6dBxqBUnt%2Bn0dJBUDCWss1c3QsFbGIpV7ae%2FM6uZxzy0EPMoioeo%2FZAoul7o%2B5aY8QMN%2FkJNXsj9XtUN7q2Cu14Ng6Dt2sVSJMQZMm%2BtR9cPR45zp%2BHq5A81BZpAMtCWLK8JUiEakh%2FQWtDxUUgLVhAX7bEdlXwNeq35eozWdF8IFS0r9Wm0sFOzbAzUxNe1BLhLFIUAUJvb30jge6SYoo4XWbRlU94ugqv004xyprTGYa%2B5jHYoUx19ke8vDXAlZQcoVSOPCboskMJ6XoosDoYGkP1AXWlOVaXzf9BNvznkaXH0CBx63LVNSqFuQBoRFLWDPxR0G6jMjDxF1FaW0yQSJLHFRsuoZL4k2nHM%2Brd9VIq9TA90htLPRGyx9v%2FjqY1pZ8eXaA64jE7oayj1aVsMNWDcQzxx8txpNDOMKfGotQGOqUBYeq%2BMSM4A1udXBvlNI0Iz41OXBEpWryRgXtnCSCRnIexfbKrG4nVDQtQr0katiDQGxmZD8Rgtp8FdsDRoVi0FRvC9Y7zqsXJMdRU8KUlzs63%2F1XMB2UUFO%2B7DAg0%2FRDC6cfo3EgkS2b7M%2B3gLRyIWz%2BITwlIdC45PV9%2B9v6aKJl79BNfMiTiUJQQlU%2F%2BPDrCgc4s7QSq1Qa6h5HPief3rcvuFp5E&X-Amz-Signature=49927951ce145617b20dc5959e0ecf2de347102e9b06e4ac510ae0ce1b2c4c45&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 1. Process 1 performs a bit flip, changing the memory value from 0 to 1. Process 2 then performs a bit flip and changes the memory value from 1 to 0.*

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7d437d1f-db53-427c-83d4-48f53a1d1ad8/image2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XLZSUZTZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204757Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEcoWzRJFccclXFrua7HF6ULmFEiuaLUqdMG08EaK6DgAiEAyinBypWg6owaUmoDDBkNS1H8r6r%2FYU4Y24dzqK%2F2QEIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDF3Jk%2FwStXm9TdFctCrcA0QCu%2ByG6hol5Yk5FxsKUOFSHyTUvzrOMN2oGcDElJSiKQHf4dr%2B%2BbWDnObtvKa9Kj1mLSiiGTpdbJnFqG1tZtzifxSecQZMhRm3KRptrHFix5Pm1MDXtwkzE5hnuB%2FY6UwYPwuo9kNtFoM%2BKfKmG7o6gycv2lqDWmsSDIOCA2BixSydJ64UcghOmbKqSSEjehmtj3TqKulOmG0fQvJJgtLf%2B%2FkCGACBC0jni9zYmOmDoYIf37yxXKjNJcmbNF53EfPgPQbiYEqJurpHPxXg9jXBl5izT36Mm2MPVzQR75VHxAXIi1Xdq%2FoVRVGAQ2r4Oegx%2F%2F5VpBbtubXDIeLruQ5OQ%2FAenjLEkKteK4016ZRc7ipeTNy3TTXhu9BGWD9D96bcfkTXx%2FtX6Qh6t6c65pFakjXyYNumwdgm%2Ff3ROSc%2FdsueOc5II34qzHtZ8laB9v08wEm7x4Tnwo2kKBPoCdUaLhzVKkuEvtkZ6NNiGk3pDBkw%2BuO4IopwnUrP1qLAlkASfDizUiNyFa%2BOv7L%2FqpqraN6gV6wuTUAC33qYtC0fHOgKJb1nhrdeCdbj%2F8NHhCDmf1JaLoSWGz7o5EM4GvyQLYZOA%2FnMuxOxWQ4BRLHbXDlHNwLX7KTnbsI6MK%2FJotQGOqUBCiG6cZZO51WcwaroVKxR4Ty1%2B7eKMxBF13ch%2F8pu904eFifu7jqqLT7ESjHomIlVu8EvPRXnA%2BkjG4xhSjU4Cd3M3ni6n2xAzBjSEipvVXKZEPwQFe7rGQt%2BKxOxsnI8Dexz24fL6psNWu8JDEWB6CVFcXQkW3GTxmBXEFY3AnuaKsFti8hj2T%2FpjeXI1rnDfVkG%2B7u4XyEMp%2BATyCTucenRdewI&X-Amz-Signature=968ffcae61a6109318b2435097bfd082119948363ba3d3503c279a2902c2a4fd&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*Figure 2. When Process 2 is unaware that Process 1 is performing a simultaneous bit flip, the bit has an ending value of 1 when its value should be 0.*

Suppose two processes need to perform a bit flip at a specific memory location. Under normal circumstances the operation should work as shown in Figure 1.

If a race condition occurred causing these two processes to overlap, the sequence of operations could potentially look more like what's shown in Figure 2.

Race conditions occasionally occur in [logic gates](https://www.techtarget.com/whatis/definition/logic-gate-AND-OR-XOR-NOT-NAND-NOR-and-XNOR) when inputs come into conflict. Because the gate output state takes a finite, nonzero amount of time to react to any change in input states, sensitive circuits or devices following the gate may be fooled by the state of the output and not operate properly.

> **Read-modify-write.** This kind of race condition happens when two processes read a value in a program and write back a new value. It often causes a software bug. Like the example above, the expectation is that the two processes will happen sequentially -- the first process produces its value and then the second process reads that value and returns a different one.

For example, if checks against a checking account are processed sequentially, the system will make sure there are enough funds in the account to process check A first and then look again to see if there are enough funds to process check B after processing check A. However, if the two checks are processed at the same time, the system may read the same account balance value for both processes and give an incorrect account balance value, causing the account to be overdrawn.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e175e155-8943-4713-b3cf-f21afb0f87b3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XJEJRYGI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204756Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCSArA35Yp6iFc8c8Dl818GA7NgeF9Cv472gYtAxNjsXAIgceJx6vSl2mugXTw5MKaMMMonhwN18G2FMFXZCGpNOOYqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLN5PKCsK0Pyp9%2FbHCrcA%2FCKYIyyo%2FXmijsGoW3uIJdSFQp%2BOOjcbnG0BUAyVmd47BDV0luF1UCpmEuppBr2HKOX6lCnii4mqGulsJ2dk28nACGw84D9%2BtH0UiCAtXzFHuTbJLBU7juJkfrPPydGXbuJ7JZi89SbGXim4%2Fio6XuIXGQsI8kTrIJC7%2Bj0WWz21f7W4MeUlVXG3lDVdo65DmtLzLSaKnJTNccSwv8NkxehqU3zr5xlXZ5K3ThZDaJEyUQG%2BSX74bjFVWAJgC5JG5OVVOtHKSYoqnzJsb31KuUHy3sivVb7s925hCzf%2FnzzosaJA90c65i44AaTSRziEKV3rcIIvXWgyASX6XGeObxllLknDbemwa4sW13C2%2BkECUMGW6Bem9jPJXcUOc8BRwox6eI8BW9x1czEhJLPHSlf4MEE8B76vywi%2BUr%2BB6VE56iqIGBxdMu4glslE%2FwbAvzGcekF77C0j9QwVkpVeXZMxVJdKBqNQsA46jOD1RdzJwlmGNr4Eq6QVSXqtbwrhv11eKbJO%2FluBA46fYh3iMthSyjG2PDSHw0lSc8W4OtXrYIc0NI3b%2FbnXHnx8RbSYhlcueqdItLxHgB%2FhfKD05vYlkwOkH7VgTLWszzwbl%2FqJTUQVyi8FJjMTnESMKfIotQGOqUBGtZgiOzBbygNw7oRtoe1Q5AAid9YxoZ86FIdi9nTHFvGDP8QB6VoOdToGvCdR9KgTwQPFfbgLR2uGayIcrR3FOTeoT07MDaRP6l8aSmwPUy%2B%2ByvfYRYnrEKhiTjUtYfkL0Itq5PheO2u3frW9PLU3dUsWZrM7oYOFYDrO9U0b%2F%2FCguyAPx14Oxq6VLM%2BU%2B6S9K3Lx95HmIfAjrsg1pEYIJnMHIEh&X-Amz-Signature=59a9475e776682db3fea5ea67ef43809930f42ecd12896f2e9ad62f51cbfa15d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

*See how a race condition could develop if a bank receives two checks -- one for $1,000 and the other for $1,500 -- at about the same time, both drawn against a checking account with only $2,000 in it.*

> **Check-then-act.** This race condition happens when two processes check a value on which they will take each take an external action. The processes both check the value, but only one process can take the value with it. The later-occurring process will read the value as null. This results in a potentially out-of-date or unavailable observation being used to determine what the program will do next. For example, if a map application runs two processes simultaneously that require the same location data, one will take the value first so the other can't use it. The later process reads the data as null.

## Limit overrun race conditions

The most well-known type of race condition enables you to exceed some kind of limit imposed by the business logic of the application.

For example, consider an online store that lets you enter a promotional code during checkout to get a one-time discount on your order. To apply this discount, the application may perform the following high-level steps:

  1. Check that you haven't already used this code.
  1. Apply the discount to the order total.
  1. Update the record in the database to reflect the fact that you've now used this code.
If you later attempt to reuse this code, the initial checks performed at the start of the process should prevent you from doing this:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1e3a0241-6bcc-41c9-ac1d-f6152bc46418/image1.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XJEJRYGI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204756Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCSArA35Yp6iFc8c8Dl818GA7NgeF9Cv472gYtAxNjsXAIgceJx6vSl2mugXTw5MKaMMMonhwN18G2FMFXZCGpNOOYqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLN5PKCsK0Pyp9%2FbHCrcA%2FCKYIyyo%2FXmijsGoW3uIJdSFQp%2BOOjcbnG0BUAyVmd47BDV0luF1UCpmEuppBr2HKOX6lCnii4mqGulsJ2dk28nACGw84D9%2BtH0UiCAtXzFHuTbJLBU7juJkfrPPydGXbuJ7JZi89SbGXim4%2Fio6XuIXGQsI8kTrIJC7%2Bj0WWz21f7W4MeUlVXG3lDVdo65DmtLzLSaKnJTNccSwv8NkxehqU3zr5xlXZ5K3ThZDaJEyUQG%2BSX74bjFVWAJgC5JG5OVVOtHKSYoqnzJsb31KuUHy3sivVb7s925hCzf%2FnzzosaJA90c65i44AaTSRziEKV3rcIIvXWgyASX6XGeObxllLknDbemwa4sW13C2%2BkECUMGW6Bem9jPJXcUOc8BRwox6eI8BW9x1czEhJLPHSlf4MEE8B76vywi%2BUr%2BB6VE56iqIGBxdMu4glslE%2FwbAvzGcekF77C0j9QwVkpVeXZMxVJdKBqNQsA46jOD1RdzJwlmGNr4Eq6QVSXqtbwrhv11eKbJO%2FluBA46fYh3iMthSyjG2PDSHw0lSc8W4OtXrYIc0NI3b%2FbnXHnx8RbSYhlcueqdItLxHgB%2FhfKD05vYlkwOkH7VgTLWszzwbl%2FqJTUQVyi8FJjMTnESMKfIotQGOqUBGtZgiOzBbygNw7oRtoe1Q5AAid9YxoZ86FIdi9nTHFvGDP8QB6VoOdToGvCdR9KgTwQPFfbgLR2uGayIcrR3FOTeoT07MDaRP6l8aSmwPUy%2B%2ByvfYRYnrEKhiTjUtYfkL0Itq5PheO2u3frW9PLU3dUsWZrM7oYOFYDrO9U0b%2F%2FCguyAPx14Oxq6VLM%2BU%2B6S9K3Lx95HmIfAjrsg1pEYIJnMHIEh&X-Amz-Signature=fd995db9cff25234735d48072004ebf2440f03c0e2a5fe785e43864cf19ec0b2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now consider what would happen if a user who has never applied this discount code before tried to apply it twice at almost exactly the same time:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ce41f6a9-5e2d-4e47-9abc-0a26de9798f4/image2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XJEJRYGI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204756Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCSArA35Yp6iFc8c8Dl818GA7NgeF9Cv472gYtAxNjsXAIgceJx6vSl2mugXTw5MKaMMMonhwN18G2FMFXZCGpNOOYqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDLN5PKCsK0Pyp9%2FbHCrcA%2FCKYIyyo%2FXmijsGoW3uIJdSFQp%2BOOjcbnG0BUAyVmd47BDV0luF1UCpmEuppBr2HKOX6lCnii4mqGulsJ2dk28nACGw84D9%2BtH0UiCAtXzFHuTbJLBU7juJkfrPPydGXbuJ7JZi89SbGXim4%2Fio6XuIXGQsI8kTrIJC7%2Bj0WWz21f7W4MeUlVXG3lDVdo65DmtLzLSaKnJTNccSwv8NkxehqU3zr5xlXZ5K3ThZDaJEyUQG%2BSX74bjFVWAJgC5JG5OVVOtHKSYoqnzJsb31KuUHy3sivVb7s925hCzf%2FnzzosaJA90c65i44AaTSRziEKV3rcIIvXWgyASX6XGeObxllLknDbemwa4sW13C2%2BkECUMGW6Bem9jPJXcUOc8BRwox6eI8BW9x1czEhJLPHSlf4MEE8B76vywi%2BUr%2BB6VE56iqIGBxdMu4glslE%2FwbAvzGcekF77C0j9QwVkpVeXZMxVJdKBqNQsA46jOD1RdzJwlmGNr4Eq6QVSXqtbwrhv11eKbJO%2FluBA46fYh3iMthSyjG2PDSHw0lSc8W4OtXrYIc0NI3b%2FbnXHnx8RbSYhlcueqdItLxHgB%2FhfKD05vYlkwOkH7VgTLWszzwbl%2FqJTUQVyi8FJjMTnESMKfIotQGOqUBGtZgiOzBbygNw7oRtoe1Q5AAid9YxoZ86FIdi9nTHFvGDP8QB6VoOdToGvCdR9KgTwQPFfbgLR2uGayIcrR3FOTeoT07MDaRP6l8aSmwPUy%2B%2ByvfYRYnrEKhiTjUtYfkL0Itq5PheO2u3frW9PLU3dUsWZrM7oYOFYDrO9U0b%2F%2FCguyAPx14Oxq6VLM%2BU%2B6S9K3Lx95HmIfAjrsg1pEYIJnMHIEh&X-Amz-Signature=03f17385f7e66337bf4e2f16e5216b3b5d133f06a7cdbace306e2826f84dba78&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

## [Limit overrun race conditions        ](./Limit_overrun_race_conditions.md)

## [Bypassing rate limits via race conditions](./Bypassing_rate_limits_via_race_conditions.md)

## [Multi-endpoint race conditions](./Multi-endpoint_race_conditions.md)

## [Single-endpoint race conditions](./Single-endpoint_race_conditions.md)

## [Exploiting time-sensitive vulnerabilities](./Exploiting_time-sensitive_vulnerabilities.md)

## [Partial construction race conditions](./Partial_construction_race_conditions.md)

