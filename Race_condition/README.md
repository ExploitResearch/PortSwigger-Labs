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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/b24449ade7fc_001.jpg)

*Figure 1. Process 1 performs a bit flip, changing the memory value from 0 to 1. Process 2 then performs a bit flip and changes the memory value from 1 to 0.*

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/b24449ade7fc_002.jpg)

*Figure 2. When Process 2 is unaware that Process 1 is performing a simultaneous bit flip, the bit has an ending value of 1 when its value should be 0.*

Suppose two processes need to perform a bit flip at a specific memory location. Under normal circumstances the operation should work as shown in Figure 1.

If a race condition occurred causing these two processes to overlap, the sequence of operations could potentially look more like what's shown in Figure 2.

Race conditions occasionally occur in [logic gates](https://www.techtarget.com/whatis/definition/logic-gate-AND-OR-XOR-NOT-NAND-NOR-and-XNOR) when inputs come into conflict. Because the gate output state takes a finite, nonzero amount of time to react to any change in input states, sensitive circuits or devices following the gate may be fooled by the state of the output and not operate properly.

{% hint style="info" %}
**Read-modify-write.** This kind of race condition happens when two processes read a value in a program and write back a new value. It often causes a software bug. Like the example above, the expectation is that the two processes will happen sequentially -- the first process produces its value and then the second process reads that value and returns a different one.
{% endhint %}

For example, if checks against a checking account are processed sequentially, the system will make sure there are enough funds in the account to process check A first and then look again to see if there are enough funds to process check B after processing check A. However, if the two checks are processed at the same time, the system may read the same account balance value for both processes and give an incorrect account balance value, causing the account to be overdrawn.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/b24449ade7fc_003.png)

*See how a race condition could develop if a bank receives two checks -- one for $1,000 and the other for $1,500 -- at about the same time, both drawn against a checking account with only $2,000 in it.*

{% hint style="info" %}
**Check-then-act.** This race condition happens when two processes check a value on which they will take each take an external action. The processes both check the value, but only one process can take the value with it. The later-occurring process will read the value as null. This results in a potentially out-of-date or unavailable observation being used to determine what the program will do next. For example, if a map application runs two processes simultaneously that require the same location data, one will take the value first so the other can't use it. The later process reads the data as null.
{% endhint %}

## Limit overrun race conditions

The most well-known type of race condition enables you to exceed some kind of limit imposed by the business logic of the application.

For example, consider an online store that lets you enter a promotional code during checkout to get a one-time discount on your order. To apply this discount, the application may perform the following high-level steps:

  1. Check that you haven't already used this code.
  1. Apply the discount to the order total.
  1. Update the record in the database to reflect the fact that you've now used this code.

If you later attempt to reuse this code, the initial checks performed at the start of the process should prevent you from doing this:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/b24449ade7fc_004.png)

Now consider what would happen if a user who has never applied this discount code before tried to apply it twice at almost exactly the same time:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/b24449ade7fc_005.png)

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

## Labs

- [Bypassing rate limits via race conditions](./Bypassing_rate_limits_via_race_conditions.md)
- [Exploiting time-sensitive vulnerabilities](./Exploiting_time-sensitive_vulnerabilities.md)
- [Limit overrun race conditions](./Limit_overrun_race_conditions.md)
- [Multi-endpoint race conditions](./Multi-endpoint_race_conditions.md)
- [Partial construction race conditions](./Partial_construction_race_conditions.md)
- [Single-endpoint race conditions](./Single-endpoint_race_conditions.md)
