# Information disclosure in error messages

### Goal - 

Obtain and submit the version number of this framework.

### Analysis/Exploitation -

Here, we can view the details of each products. **Let’s click on the **`View details`** button**

![](./images/1af706c709e6_001.png)

It Send the `GET` request to `/product`with parameter `productId=1` 

![](./images/1af706c709e6_002.png)

**What happens when I modify it?**

Use a productId that does not exist:

![](./images/1af706c709e6_003.png)

It gives an error “Not Found” and handle it properly and do not reveal anything interesting.

Change the value of the `productId` parameter to a non-integer data type, such as a string:

![](./images/1af706c709e6_004.png)

- Web application uses vulnerable version of : `Apache Struts 2 2.3.31`

**In **`searchsploit`**(An offline version of Exploit-DB), we can see that it’s vulnerable to Remote Code Execution(RCE)!**

![](./images/1af706c709e6_005.png)
