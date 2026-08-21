# URL-based access control can be circumvented

### Target Goal - 

Access the admin panel and delete the user `carlos`.

### Analysis/Exploitation -

there are navbar contents consisting of Home, Admin Panel, and My Account.When trying to access the Admin Panel, the web display the text “access denied”.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/013c9931-0643-4abd-99be-256cc8f9232a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZNBDAH26%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221920Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCID3EB8UeyphfRKDTzoPADiWgljFIGyiN8zrBjDgGPxG3AiEAnL5Hu3nARtTcHeaFbA6MjR0lAP8v5ZCEnz5C29de%2B7oqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDMkKBkBY8QlEvvTfdyrcA0sVRhg0JSLSv7IHBL5GQk2qGD4BNCOKwmNDr0w%2FH23UjLXNu60Lziku%2BSYpbtUYpLL3LnDMmeJqPu3NR%2Fhog2ha21rATMBDG0oHtW87wMQ7ey1ReXaZBwl%2BerFCriu7KYaoWA6iUQ0EZYy0SjAY4H25wi2MR3YGZ9YWPo3rgePX6balbrsidSiONgHLkeyF58zoVzmQlzMLAEQn0drGu5l4TJOKgWUFJp18MaRmZgFrHzSC0XBgEOyaa2lyFgcxyhdvbH4GIAK4U0zshFAKfDet9Ug6DKQrjM5WwyjwceapMj5J9B5wA5jQcNucQSQK%2BtxA27o%2FacI9Q19QPPbgv4LCiixTaEvNTygWHySel9RI%2BdebrJcrblJFs5%2Ftk9mYtWPZF5tkDMz5ekFtCshBl4U2UeKArGMjp51G2DmBmgxwFJ9cji6zf%2Bttn%2FSn895og4ZfYL9llWdIfKR7IT25Bi3QJn%2BzitchX8vaNGIvEzD6WZ9wNce2AnjdER5GcnEH0kkEs58%2FdWSoCAAhdC5M1GRq%2Bca8jP7YnCEa5Sz%2FmYynzV06pvKo1DDYcpOExCRhmmMNmkHTqKhkFg%2BxFHBbUTT5WKZvlEqHFyVcHzU4GLtBnEXmXlHYYCnw%2BCGMMN6Go9QGOqUB%2FfszaWJO6e%2FK0dFGP1lWZ5KoeKwHhQ1T4l%2Fqe7JQY9wxl5dEfA3l%2FcUyZ5QI%2B75z%2FTZQx3KIz0OZ9L5I8T4e7KkFFBNSgHVqOHGEQrqhFW5E9Cjm3oG%2BreaWBJdPCmSx167Km1M3RnXD%2BxG4MrvKbfYw0eqFi9c2IuNhj4BMJLC%2F5n5zKGQTsm7fE%2B7IOGVdNM%2FJwg1bpLScbutjUZCbONoJMOi2&X-Amz-Signature=09ec27ee11d2e18d223748ad5ab65b74f76c7a56a45317298862b613b1027540&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Let’s try to intercept when we want to access the admin panel using the burp suite. Here’s how it looks.

![](https://miro.medium.com/v2/resize:fit:700/0*glU9EajspkDB_z7h)

Based on the intercept results, the HTTP request method “Get” points to the /admin directory.

Let’s try to use non-standard HTTP headers that can replace the URL in the original request such as X-Original-URL to bypass admin access.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5140ce8e-fc5e-40a1-a9f3-a240ae459e82/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZNBDAH26%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221920Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCID3EB8UeyphfRKDTzoPADiWgljFIGyiN8zrBjDgGPxG3AiEAnL5Hu3nARtTcHeaFbA6MjR0lAP8v5ZCEnz5C29de%2B7oqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDMkKBkBY8QlEvvTfdyrcA0sVRhg0JSLSv7IHBL5GQk2qGD4BNCOKwmNDr0w%2FH23UjLXNu60Lziku%2BSYpbtUYpLL3LnDMmeJqPu3NR%2Fhog2ha21rATMBDG0oHtW87wMQ7ey1ReXaZBwl%2BerFCriu7KYaoWA6iUQ0EZYy0SjAY4H25wi2MR3YGZ9YWPo3rgePX6balbrsidSiONgHLkeyF58zoVzmQlzMLAEQn0drGu5l4TJOKgWUFJp18MaRmZgFrHzSC0XBgEOyaa2lyFgcxyhdvbH4GIAK4U0zshFAKfDet9Ug6DKQrjM5WwyjwceapMj5J9B5wA5jQcNucQSQK%2BtxA27o%2FacI9Q19QPPbgv4LCiixTaEvNTygWHySel9RI%2BdebrJcrblJFs5%2Ftk9mYtWPZF5tkDMz5ekFtCshBl4U2UeKArGMjp51G2DmBmgxwFJ9cji6zf%2Bttn%2FSn895og4ZfYL9llWdIfKR7IT25Bi3QJn%2BzitchX8vaNGIvEzD6WZ9wNce2AnjdER5GcnEH0kkEs58%2FdWSoCAAhdC5M1GRq%2Bca8jP7YnCEa5Sz%2FmYynzV06pvKo1DDYcpOExCRhmmMNmkHTqKhkFg%2BxFHBbUTT5WKZvlEqHFyVcHzU4GLtBnEXmXlHYYCnw%2BCGMMN6Go9QGOqUB%2FfszaWJO6e%2FK0dFGP1lWZ5KoeKwHhQ1T4l%2Fqe7JQY9wxl5dEfA3l%2FcUyZ5QI%2B75z%2FTZQx3KIz0OZ9L5I8T4e7KkFFBNSgHVqOHGEQrqhFW5E9Cjm3oG%2BreaWBJdPCmSx167Km1M3RnXD%2BxG4MrvKbfYw0eqFi9c2IuNhj4BMJLC%2F5n5zKGQTsm7fE%2B7IOGVdNM%2FJwg1bpLScbutjUZCbONoJMOi2&X-Amz-Signature=be00347bcf69434a04dc4a5100bbe3bfd94dfce212c7a5944639ca4d4d53d6ec&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It still doesn’t work :(

According to the lab description, “the front-end system has been configured to block external access to that path”. Let’s try to remove “admin” in the HTTP request method “get” so that it only leaves “/”.

![](https://miro.medium.com/v2/resize:fit:700/0*pZzFpMi66PxnJ6Pf)

The response displays 200 OK, which means the admin access was successfully bypassed. Next, find out how to delete the user Carlos to complete this lab.

Search “delete” or scroll down a bit in the response. We will find the path “/admin/delete” with the query string “?username=carlos” which leads to the user data deletion function with the parameter “username” which is “Carlos”.

![](https://miro.medium.com/v2/resize:fit:700/0*ELlUNarI4w2Iu1lT)

Let’s try adding it to the X-Original-Url and run it.

![](https://miro.medium.com/v2/resize:fit:700/0*a0wr6IUXoq5ZqpFz)

The response will show “HTTP/2 400 Bad Request” with the message “Missing parameter ‘username’”. This indicates that the server did not read the query string “?username=carlos” in the X-Original-Url. So for the query string, we can try moving it to Get /?username=carlos.

![](https://miro.medium.com/v2/resize:fit:700/0*Antpbuz2TaMnSKBB)

The response displays 302 Found with the directory location /admin, which means the URL function has successfully deleted the user with the username Carlos.

If we check back to the /admin directory, the Carlos user no longer exists.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3e4c3a57-ab8d-412d-8798-24a5085cba67/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZNBDAH26%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221920Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCID3EB8UeyphfRKDTzoPADiWgljFIGyiN8zrBjDgGPxG3AiEAnL5Hu3nARtTcHeaFbA6MjR0lAP8v5ZCEnz5C29de%2B7oqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDMkKBkBY8QlEvvTfdyrcA0sVRhg0JSLSv7IHBL5GQk2qGD4BNCOKwmNDr0w%2FH23UjLXNu60Lziku%2BSYpbtUYpLL3LnDMmeJqPu3NR%2Fhog2ha21rATMBDG0oHtW87wMQ7ey1ReXaZBwl%2BerFCriu7KYaoWA6iUQ0EZYy0SjAY4H25wi2MR3YGZ9YWPo3rgePX6balbrsidSiONgHLkeyF58zoVzmQlzMLAEQn0drGu5l4TJOKgWUFJp18MaRmZgFrHzSC0XBgEOyaa2lyFgcxyhdvbH4GIAK4U0zshFAKfDet9Ug6DKQrjM5WwyjwceapMj5J9B5wA5jQcNucQSQK%2BtxA27o%2FacI9Q19QPPbgv4LCiixTaEvNTygWHySel9RI%2BdebrJcrblJFs5%2Ftk9mYtWPZF5tkDMz5ekFtCshBl4U2UeKArGMjp51G2DmBmgxwFJ9cji6zf%2Bttn%2FSn895og4ZfYL9llWdIfKR7IT25Bi3QJn%2BzitchX8vaNGIvEzD6WZ9wNce2AnjdER5GcnEH0kkEs58%2FdWSoCAAhdC5M1GRq%2Bca8jP7YnCEa5Sz%2FmYynzV06pvKo1DDYcpOExCRhmmMNmkHTqKhkFg%2BxFHBbUTT5WKZvlEqHFyVcHzU4GLtBnEXmXlHYYCnw%2BCGMMN6Go9QGOqUB%2FfszaWJO6e%2FK0dFGP1lWZ5KoeKwHhQ1T4l%2Fqe7JQY9wxl5dEfA3l%2FcUyZ5QI%2B75z%2FTZQx3KIz0OZ9L5I8T4e7KkFFBNSgHVqOHGEQrqhFW5E9Cjm3oG%2BreaWBJdPCmSx167Km1M3RnXD%2BxG4MrvKbfYw0eqFi9c2IuNhj4BMJLC%2F5n5zKGQTsm7fE%2B7IOGVdNM%2FJwg1bpLScbutjUZCbONoJMOi2&X-Amz-Signature=dfbf67b5a94c03aa939f7dd6a9d7d7bd4e5858cbd18c820f56964a0023a72580&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
