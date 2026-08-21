# OS command injection, simple case

### Goal - 

Exploit command injection to execute whoami command.

### Analysis/Exploitation 

As usual, the first step is to browse around a bit. Upon viewing view details of an product we get detail information about that product and we can see upon visiting a specific product a parameter named **productId **is being set. Well this is where we can try to preform command injection and i did but no luck because it fetches information by using an API which restrict all special characters. But as there is another functionality which allows us check for availability of stocks.

Let’s click the `Check stock` button, and intercept the request via Burp Suite

When we clicked that button, it’ll send a POST request to `/product/stock`, with parameter `productId=1` and `storeId=1`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/57677f51-8e40-4a70-bab1-35d5591b4927/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QLSQIKON%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215555Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC2vbVHWek%2BoEzFg%2B1LLOFdRBnJkUR2hNs2nOgEJM5tHQIgYosA2MxvdNCDRO1D%2B5jAVeQwt9VhU0%2BTPRFaSXMKtJgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNkRK1PqLp%2Bv%2FAf1bCrcA2DD6upVkfzu0YMJjNUyN8c%2Ba9PcP8SXlmdgIh20IcbrIXxJiY7WiQeeVOf9jEC0Lxe208hTtNvkHhygo%2FOLynV1of0m9LAITdzfEy2jWLM9y5BwXxA5uT1YnGV%2FqunHEwsQR0LZ3sawWyQZalvKftZhNZAWkfDDjc0thAJgfuOhk9fCea9izX30UkfDvpv8EakbTIoJlJLprghOLBC4iTA0kjXLnNwscz95U8hotJvFvat3vkkURpoq2W8QJ9XwoyRSC6iNM%2FDz9KqX0u9YFqh%2Fpn0l8kZPiezpNmmB7I%2B0JFqomG4I7lFQ6msJyOPx1UB3oE2yVClujWhPidwDAcAODsJHztVrpLDt2OuUFXHOPj0FSZys0pLc5yKSz8C%2BDvTqGcI%2FOivcCIutkR8Lt96V6Lk6ZUj99CXmek6ivO%2BFBRQVQICQs4G8CkVLl4N%2FnC%2BZ4NoOfk2GobK%2BNULNs8hM0%2BCbyB1DHzOiMntmqbiJOdIiAHCa6csos9MbSwYK%2B1vNAg%2BtRVREGUqRSZ5fsr6lYJTckHDLI3pp%2FH9OWU9MhXTEOEDdM93cljxMrqhxAm6fKqi7Co8kRjmbhg%2FTNJSbhUOakr01QlFM1O9nNep%2Fyjy8ij%2FjPqASskMhMKWEo9QGOqUB%2BL8BrLkS1KlpjLIeMC8A2GIJif96MzrvFMFkjOdO7eEES6cdCT7X9ZvmiepC2Mip3xUWlTcrJ%2F8Zuu7P6uyahcXAKQ8ruAYnsvOsIWBwW80RyM20fNfjL4%2F2e%2Fm86FpR1Qdf9vtZBxjgQBSf69e89Fu%2FnP0MKScidpe7Ds4MtluUBzXvvkku8KsYgm%2Fwooyl0zk1S%2F%2BglMfM0YS5Y04Q1r9wSYxd&X-Amz-Signature=883e3ea8052e858affd6708db8d1d30331c6398ad31452534d5e51b7bed91e34&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As we have two parameters, I try to inject both with different commands. This way, I can find out which parameter is injectable and in which order they are executed.

> 💡 The script call might look something like this (likely not the exact syntax, but the general idea is the same):

```bash
echo system("someScript.sh $_REQUEST['productID'] $_REQUEST['storeId']")
```

In this case, the parameters are used as arguments for the script and the output is directly echoed back into the HTML.

There are multiple ways to execute multiple commands in one line in a shell, separating the individual commands with for example `&`, `&&`, `|`, `||`, `;`. All behave slightly differently. On Unix systems, my favorite is `;` as it completely separates the commands without side effects based on return conditions or execution order. In some conditions `&` is better as it backgrounds the command before my injection and runs my code without waiting for the other command to finish. Still, my favourite remains `;`.

**NOTE :**** when using **`&`**, it must be URLencoded**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/abae6bdd-003c-43b0-a3dc-7da788ecab25/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QLSQIKON%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215555Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC2vbVHWek%2BoEzFg%2B1LLOFdRBnJkUR2hNs2nOgEJM5tHQIgYosA2MxvdNCDRO1D%2B5jAVeQwt9VhU0%2BTPRFaSXMKtJgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNkRK1PqLp%2Bv%2FAf1bCrcA2DD6upVkfzu0YMJjNUyN8c%2Ba9PcP8SXlmdgIh20IcbrIXxJiY7WiQeeVOf9jEC0Lxe208hTtNvkHhygo%2FOLynV1of0m9LAITdzfEy2jWLM9y5BwXxA5uT1YnGV%2FqunHEwsQR0LZ3sawWyQZalvKftZhNZAWkfDDjc0thAJgfuOhk9fCea9izX30UkfDvpv8EakbTIoJlJLprghOLBC4iTA0kjXLnNwscz95U8hotJvFvat3vkkURpoq2W8QJ9XwoyRSC6iNM%2FDz9KqX0u9YFqh%2Fpn0l8kZPiezpNmmB7I%2B0JFqomG4I7lFQ6msJyOPx1UB3oE2yVClujWhPidwDAcAODsJHztVrpLDt2OuUFXHOPj0FSZys0pLc5yKSz8C%2BDvTqGcI%2FOivcCIutkR8Lt96V6Lk6ZUj99CXmek6ivO%2BFBRQVQICQs4G8CkVLl4N%2FnC%2BZ4NoOfk2GobK%2BNULNs8hM0%2BCbyB1DHzOiMntmqbiJOdIiAHCa6csos9MbSwYK%2B1vNAg%2BtRVREGUqRSZ5fsr6lYJTckHDLI3pp%2FH9OWU9MhXTEOEDdM93cljxMrqhxAm6fKqi7Co8kRjmbhg%2FTNJSbhUOakr01QlFM1O9nNep%2Fyjy8ij%2FjPqASskMhMKWEo9QGOqUB%2BL8BrLkS1KlpjLIeMC8A2GIJif96MzrvFMFkjOdO7eEES6cdCT7X9ZvmiepC2Mip3xUWlTcrJ%2F8Zuu7P6uyahcXAKQ8ruAYnsvOsIWBwW80RyM20fNfjL4%2F2e%2Fm86FpR1Qdf9vtZBxjgQBSf69e89Fu%2FnP0MKScidpe7Ds4MtluUBzXvvkku8KsYgm%2Fwooyl0zk1S%2F%2BglMfM0YS5Y04Q1r9wSYxd&X-Amz-Signature=849afbeb5b7556c9bc95c4dcce5dec2d404e91454c66c099bcedb6bbd4849c12&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From the response, it can be seen that both parameters are injectable, and they are executed in the order productId first, storeId second.

**Let’s execute **`whoami`** command**

comment out the remainder of the line after the `whoami` to avoid the error message of the second parameter:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/922ea403-d4eb-47da-81af-f792b32ac69e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QLSQIKON%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215555Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC2vbVHWek%2BoEzFg%2B1LLOFdRBnJkUR2hNs2nOgEJM5tHQIgYosA2MxvdNCDRO1D%2B5jAVeQwt9VhU0%2BTPRFaSXMKtJgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNkRK1PqLp%2Bv%2FAf1bCrcA2DD6upVkfzu0YMJjNUyN8c%2Ba9PcP8SXlmdgIh20IcbrIXxJiY7WiQeeVOf9jEC0Lxe208hTtNvkHhygo%2FOLynV1of0m9LAITdzfEy2jWLM9y5BwXxA5uT1YnGV%2FqunHEwsQR0LZ3sawWyQZalvKftZhNZAWkfDDjc0thAJgfuOhk9fCea9izX30UkfDvpv8EakbTIoJlJLprghOLBC4iTA0kjXLnNwscz95U8hotJvFvat3vkkURpoq2W8QJ9XwoyRSC6iNM%2FDz9KqX0u9YFqh%2Fpn0l8kZPiezpNmmB7I%2B0JFqomG4I7lFQ6msJyOPx1UB3oE2yVClujWhPidwDAcAODsJHztVrpLDt2OuUFXHOPj0FSZys0pLc5yKSz8C%2BDvTqGcI%2FOivcCIutkR8Lt96V6Lk6ZUj99CXmek6ivO%2BFBRQVQICQs4G8CkVLl4N%2FnC%2BZ4NoOfk2GobK%2BNULNs8hM0%2BCbyB1DHzOiMntmqbiJOdIiAHCa6csos9MbSwYK%2B1vNAg%2BtRVREGUqRSZ5fsr6lYJTckHDLI3pp%2FH9OWU9MhXTEOEDdM93cljxMrqhxAm6fKqi7Co8kRjmbhg%2FTNJSbhUOakr01QlFM1O9nNep%2Fyjy8ij%2FjPqASskMhMKWEo9QGOqUB%2BL8BrLkS1KlpjLIeMC8A2GIJif96MzrvFMFkjOdO7eEES6cdCT7X9ZvmiepC2Mip3xUWlTcrJ%2F8Zuu7P6uyahcXAKQ8ruAYnsvOsIWBwW80RyM20fNfjL4%2F2e%2Fm86FpR1Qdf9vtZBxjgQBSf69e89Fu%2FnP0MKScidpe7Ds4MtluUBzXvvkku8KsYgm%2Fwooyl0zk1S%2F%2BglMfM0YS5Y04Q1r9wSYxd&X-Amz-Signature=11a5898ab37908c8557eeca25f00836447e36bfcd3a254660c5c11f693e6711d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
