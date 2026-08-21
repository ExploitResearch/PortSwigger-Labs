# OS command injection, simple case

### Goal - 

Exploit command injection to execute whoami command.

### Analysis/Exploitation 

As usual, the first step is to browse around a bit. Upon viewing view details of an product we get detail information about that product and we can see upon visiting a specific product a parameter named **productId **is being set. Well this is where we can try to preform command injection and i did but no luck because it fetches information by using an API which restrict all special characters. But as there is another functionality which allows us check for availability of stocks.

Let’s click the `Check stock` button, and intercept the request via Burp Suite

When we clicked that button, it’ll send a POST request to `/product/stock`, with parameter `productId=1` and `storeId=1`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/57677f51-8e40-4a70-bab1-35d5591b4927/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XOTQOTJG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222002Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDjfHQQD0nc0Uc%2BfrA1WGXVcpnRqWGUXIuQ5XQ4n6MrhAIgHOGlzIQiAQ64y1MCMMyey5IHNpdj71LjUFjkGQWH2d4qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNkpwn6W7saNy156fSrcAyHKiB012UJYMNxAq3ScnwQhJmPUL2XIxZorMzCS7aNaPj1KYj4lphJ9Pib%2FhJaX0sTOYoMhoKz5tIRqI4KWwlYQ14TmpO32pbkRmH94GhO5ITPlE86%2F6OheK6ksZho0slXyxr9KoUEPQ%2B7Yl76qlDRy7XKjcI08svRc7XRf4IENuRJUcdTG0Fiqd0R0tAT5SPtLUNYMEBK7QVx4SvOYansduTvqXvg%2FkgbdxrOQHh8iW8IQnOom7qVTO%2BMueq7w4ulFUZCjQt1DJB%2BXJz0PWKp9TGdUdyw57Iz6J8ieOgsC8T02MlWioDFtWJAbHBTUsRF8LXotlEl5R6UOw0e8m2Ln6eBYZUplt4flX12cx%2B%2FAolq06uwCtPGz9y4Z8xe6NI64qaD%2Fl3GIVdYQu4JKUhQPbQgxvSwEnKMo7RrYmZbvUb4Xpy5PBNznL0aj55AWodEwvOY02Dpkb4tK3SDii5KUcwFve0h0KnGxz1YouRz5Tgbn57HXh9TwXiPs9HXMn2dRdWB3MtS4VMx4qg2kpYg3SvmT5XDTkoz8WfZg0NwG3O9nuK2W7l4l%2BWQRDKQ9TTr%2BT05GOI0kbuZ9n3LqMwYm%2BnrQ8AafNQRaGXhwHr2KlDAVf7HOdabHcMd5MNmFo9QGOqUBU8OXQzICiH9TLSl%2FaLvN2Iuj7H2qzW06iTlFxd%2Fge633dcEt3JbIW5YpTo8fszxmk59pxe6MxSPnl9hXDWv4Evvo%2B7Lc4rZedt7LfY2ObNSBAvXd3bk8Ruk24wQE1KPpwcfngnHSX0tjjNr5SLSyS4KPZrZTCNJHvgFNgD2fnWhtEVyoar1nuILPT0ifM9NU6iHtyn4EyJapAPb5oYhK%2Bv3KLajx&X-Amz-Signature=3679790f296b0429615aaa9ba36f3d8e531443228e8fe5ebaedea010e1c3b7de&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As we have two parameters, I try to inject both with different commands. This way, I can find out which parameter is injectable and in which order they are executed.

> 💡 The script call might look something like this (likely not the exact syntax, but the general idea is the same):

```bash
echo system("someScript.sh $_REQUEST['productID'] $_REQUEST['storeId']")
```

In this case, the parameters are used as arguments for the script and the output is directly echoed back into the HTML.

There are multiple ways to execute multiple commands in one line in a shell, separating the individual commands with for example `&`, `&&`, `|`, `||`, `;`. All behave slightly differently. On Unix systems, my favorite is `;` as it completely separates the commands without side effects based on return conditions or execution order. In some conditions `&` is better as it backgrounds the command before my injection and runs my code without waiting for the other command to finish. Still, my favourite remains `;`.

<span style="color: #E03E1B">**NOTE :**</span>** when using **`&`**, it must be URLencoded**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/abae6bdd-003c-43b0-a3dc-7da788ecab25/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XOTQOTJG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222002Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDjfHQQD0nc0Uc%2BfrA1WGXVcpnRqWGUXIuQ5XQ4n6MrhAIgHOGlzIQiAQ64y1MCMMyey5IHNpdj71LjUFjkGQWH2d4qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNkpwn6W7saNy156fSrcAyHKiB012UJYMNxAq3ScnwQhJmPUL2XIxZorMzCS7aNaPj1KYj4lphJ9Pib%2FhJaX0sTOYoMhoKz5tIRqI4KWwlYQ14TmpO32pbkRmH94GhO5ITPlE86%2F6OheK6ksZho0slXyxr9KoUEPQ%2B7Yl76qlDRy7XKjcI08svRc7XRf4IENuRJUcdTG0Fiqd0R0tAT5SPtLUNYMEBK7QVx4SvOYansduTvqXvg%2FkgbdxrOQHh8iW8IQnOom7qVTO%2BMueq7w4ulFUZCjQt1DJB%2BXJz0PWKp9TGdUdyw57Iz6J8ieOgsC8T02MlWioDFtWJAbHBTUsRF8LXotlEl5R6UOw0e8m2Ln6eBYZUplt4flX12cx%2B%2FAolq06uwCtPGz9y4Z8xe6NI64qaD%2Fl3GIVdYQu4JKUhQPbQgxvSwEnKMo7RrYmZbvUb4Xpy5PBNznL0aj55AWodEwvOY02Dpkb4tK3SDii5KUcwFve0h0KnGxz1YouRz5Tgbn57HXh9TwXiPs9HXMn2dRdWB3MtS4VMx4qg2kpYg3SvmT5XDTkoz8WfZg0NwG3O9nuK2W7l4l%2BWQRDKQ9TTr%2BT05GOI0kbuZ9n3LqMwYm%2BnrQ8AafNQRaGXhwHr2KlDAVf7HOdabHcMd5MNmFo9QGOqUBU8OXQzICiH9TLSl%2FaLvN2Iuj7H2qzW06iTlFxd%2Fge633dcEt3JbIW5YpTo8fszxmk59pxe6MxSPnl9hXDWv4Evvo%2B7Lc4rZedt7LfY2ObNSBAvXd3bk8Ruk24wQE1KPpwcfngnHSX0tjjNr5SLSyS4KPZrZTCNJHvgFNgD2fnWhtEVyoar1nuILPT0ifM9NU6iHtyn4EyJapAPb5oYhK%2Bv3KLajx&X-Amz-Signature=36e4428d89a97a496eaecc0e0cd1a4dedf8d63cc0c2728535c55a674a4046888&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From the response, it can be seen that both parameters are injectable, and they are executed in the order productId first, storeId second.

**Let’s execute **`whoami`** command**

comment out the remainder of the line after the `whoami` to avoid the error message of the second parameter:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/922ea403-d4eb-47da-81af-f792b32ac69e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XOTQOTJG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222002Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDjfHQQD0nc0Uc%2BfrA1WGXVcpnRqWGUXIuQ5XQ4n6MrhAIgHOGlzIQiAQ64y1MCMMyey5IHNpdj71LjUFjkGQWH2d4qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNkpwn6W7saNy156fSrcAyHKiB012UJYMNxAq3ScnwQhJmPUL2XIxZorMzCS7aNaPj1KYj4lphJ9Pib%2FhJaX0sTOYoMhoKz5tIRqI4KWwlYQ14TmpO32pbkRmH94GhO5ITPlE86%2F6OheK6ksZho0slXyxr9KoUEPQ%2B7Yl76qlDRy7XKjcI08svRc7XRf4IENuRJUcdTG0Fiqd0R0tAT5SPtLUNYMEBK7QVx4SvOYansduTvqXvg%2FkgbdxrOQHh8iW8IQnOom7qVTO%2BMueq7w4ulFUZCjQt1DJB%2BXJz0PWKp9TGdUdyw57Iz6J8ieOgsC8T02MlWioDFtWJAbHBTUsRF8LXotlEl5R6UOw0e8m2Ln6eBYZUplt4flX12cx%2B%2FAolq06uwCtPGz9y4Z8xe6NI64qaD%2Fl3GIVdYQu4JKUhQPbQgxvSwEnKMo7RrYmZbvUb4Xpy5PBNznL0aj55AWodEwvOY02Dpkb4tK3SDii5KUcwFve0h0KnGxz1YouRz5Tgbn57HXh9TwXiPs9HXMn2dRdWB3MtS4VMx4qg2kpYg3SvmT5XDTkoz8WfZg0NwG3O9nuK2W7l4l%2BWQRDKQ9TTr%2BT05GOI0kbuZ9n3LqMwYm%2BnrQ8AafNQRaGXhwHr2KlDAVf7HOdabHcMd5MNmFo9QGOqUBU8OXQzICiH9TLSl%2FaLvN2Iuj7H2qzW06iTlFxd%2Fge633dcEt3JbIW5YpTo8fszxmk59pxe6MxSPnl9hXDWv4Evvo%2B7Lc4rZedt7LfY2ObNSBAvXd3bk8Ruk24wQE1KPpwcfngnHSX0tjjNr5SLSyS4KPZrZTCNJHvgFNgD2fnWhtEVyoar1nuILPT0ifM9NU6iHtyn4EyJapAPb5oYhK%2Bv3KLajx&X-Amz-Signature=00bd16140a0be73781f30a511967cac73ba94f937f189df348e859b7ebbc0f1e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
