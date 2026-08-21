# URL-based access control can be circumvented

### Target Goal - 

Access the admin panel and delete the user `carlos`.

### Analysis/Exploitation -

there are navbar contents consisting of Home, Admin Panel, and My Account.When trying to access the Admin Panel, the web display the text “access denied”.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/013c9931-0643-4abd-99be-256cc8f9232a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z63437N5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210353Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCztiJZL0s9P88e8c1CKr9GyULCh5yGJzDXpvO%2BTWSieQIhALwHixsHqRfUlShqbiUMxyir23KmYU%2FuOC6EfjXLDPfOKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxK0T1C5lm50aRmj%2Bcq3APn0ZoYwGyZQno4syCIgJ7uN7sLlgWMWMV8RYrw%2FBz13Sg4Pj7EuBU4xfakBt2QJ3%2B%2FubhvlMU75sW%2FEWMjH87Ua2TT%2BlwA6JQ0pH2jMiJBlAFd0kVfcrHvLcMDL9BiY700%2B1bt2SoHvvZOsnnoUC9T5np8A%2FGCPXSyarx2yBAh2GEIkKWQFn2bk43kQzx%2BazZ6lyUQtHMj6aCLjbHG5g6Ts36M%2F0BfZejcJkrfGQwtoemt2jAGx8NCOgM%2BZ5g7GITgKg5z5zbngBchXj9X94g71KhuqwpeoQdO3BpexN%2BFNrUqZa5eQI%2BfDOavaB2a4JWIJ6CoBY3YlFqv1eCvLNukZiJH8nelBoIb6Ji8QZJqJe6KW%2FK22AZgToedTWktTkyk%2FyJvNzlNZlNYnTPq3PBfxlbtGfyhTdCbdthpOD6iZ0hq66xTQC0mxUvTuImX6RQtP36y%2Bgl%2BOe4%2FgBplG%2FS0oZ1PxSJPkvEgtQUSmRSKlQmkiAmJcDNxJbnaiabSdYXywxLiP7Kal8K7NbRF1%2F7GjfzugDGX1jMvXJ%2FmgDxgOLuCGoyadyRbG5VgDhcnoZo%2B%2BNCdIwkt214LldMz6Vf6UxJGBVF5JZVN0dvgeGlB1UDWCDr8Ni%2BKju8qqzDTyaLUBjqkAbNQ%2FFvUfSme4zjacZijRWoFi1XSeTgQ098g5K%2FTEmwRzMz5moM363mtRtYfU0GV7hPZR8KY5uvjv8oaSY5mKMKN7JAlNxQphwTimAFl1ulfFbAbm9vLj3bkDSQjnYZnG5j%2B%2Fm3d8jXpmM3DE7r8M10FRVrfPiRJbKmqaylXtdeHwpL%2Bm55fEEQsvkXihi5%2FccDe7Lb96LlsQT9u1rslLMPcVX6e&X-Amz-Signature=b156bc5fb311f9148fe3558fd5000d3b8f4c9ec7ff4c303ea5f53882184ea19c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Let’s try to intercept when we want to access the admin panel using the burp suite. Here’s how it looks.

![](https://miro.medium.com/v2/resize:fit:700/0*glU9EajspkDB_z7h)

Based on the intercept results, the HTTP request method “Get” points to the /admin directory.

Let’s try to use non-standard HTTP headers that can replace the URL in the original request such as X-Original-URL to bypass admin access.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5140ce8e-fc5e-40a1-a9f3-a240ae459e82/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z63437N5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210353Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCztiJZL0s9P88e8c1CKr9GyULCh5yGJzDXpvO%2BTWSieQIhALwHixsHqRfUlShqbiUMxyir23KmYU%2FuOC6EfjXLDPfOKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxK0T1C5lm50aRmj%2Bcq3APn0ZoYwGyZQno4syCIgJ7uN7sLlgWMWMV8RYrw%2FBz13Sg4Pj7EuBU4xfakBt2QJ3%2B%2FubhvlMU75sW%2FEWMjH87Ua2TT%2BlwA6JQ0pH2jMiJBlAFd0kVfcrHvLcMDL9BiY700%2B1bt2SoHvvZOsnnoUC9T5np8A%2FGCPXSyarx2yBAh2GEIkKWQFn2bk43kQzx%2BazZ6lyUQtHMj6aCLjbHG5g6Ts36M%2F0BfZejcJkrfGQwtoemt2jAGx8NCOgM%2BZ5g7GITgKg5z5zbngBchXj9X94g71KhuqwpeoQdO3BpexN%2BFNrUqZa5eQI%2BfDOavaB2a4JWIJ6CoBY3YlFqv1eCvLNukZiJH8nelBoIb6Ji8QZJqJe6KW%2FK22AZgToedTWktTkyk%2FyJvNzlNZlNYnTPq3PBfxlbtGfyhTdCbdthpOD6iZ0hq66xTQC0mxUvTuImX6RQtP36y%2Bgl%2BOe4%2FgBplG%2FS0oZ1PxSJPkvEgtQUSmRSKlQmkiAmJcDNxJbnaiabSdYXywxLiP7Kal8K7NbRF1%2F7GjfzugDGX1jMvXJ%2FmgDxgOLuCGoyadyRbG5VgDhcnoZo%2B%2BNCdIwkt214LldMz6Vf6UxJGBVF5JZVN0dvgeGlB1UDWCDr8Ni%2BKju8qqzDTyaLUBjqkAbNQ%2FFvUfSme4zjacZijRWoFi1XSeTgQ098g5K%2FTEmwRzMz5moM363mtRtYfU0GV7hPZR8KY5uvjv8oaSY5mKMKN7JAlNxQphwTimAFl1ulfFbAbm9vLj3bkDSQjnYZnG5j%2B%2Fm3d8jXpmM3DE7r8M10FRVrfPiRJbKmqaylXtdeHwpL%2Bm55fEEQsvkXihi5%2FccDe7Lb96LlsQT9u1rslLMPcVX6e&X-Amz-Signature=a0a8bb9dc96bebaf0b104a7f7bfa811dffcc15278ea1ab9e39e40fc23b96c40f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3e4c3a57-ab8d-412d-8798-24a5085cba67/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Z63437N5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210353Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCztiJZL0s9P88e8c1CKr9GyULCh5yGJzDXpvO%2BTWSieQIhALwHixsHqRfUlShqbiUMxyir23KmYU%2FuOC6EfjXLDPfOKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxK0T1C5lm50aRmj%2Bcq3APn0ZoYwGyZQno4syCIgJ7uN7sLlgWMWMV8RYrw%2FBz13Sg4Pj7EuBU4xfakBt2QJ3%2B%2FubhvlMU75sW%2FEWMjH87Ua2TT%2BlwA6JQ0pH2jMiJBlAFd0kVfcrHvLcMDL9BiY700%2B1bt2SoHvvZOsnnoUC9T5np8A%2FGCPXSyarx2yBAh2GEIkKWQFn2bk43kQzx%2BazZ6lyUQtHMj6aCLjbHG5g6Ts36M%2F0BfZejcJkrfGQwtoemt2jAGx8NCOgM%2BZ5g7GITgKg5z5zbngBchXj9X94g71KhuqwpeoQdO3BpexN%2BFNrUqZa5eQI%2BfDOavaB2a4JWIJ6CoBY3YlFqv1eCvLNukZiJH8nelBoIb6Ji8QZJqJe6KW%2FK22AZgToedTWktTkyk%2FyJvNzlNZlNYnTPq3PBfxlbtGfyhTdCbdthpOD6iZ0hq66xTQC0mxUvTuImX6RQtP36y%2Bgl%2BOe4%2FgBplG%2FS0oZ1PxSJPkvEgtQUSmRSKlQmkiAmJcDNxJbnaiabSdYXywxLiP7Kal8K7NbRF1%2F7GjfzugDGX1jMvXJ%2FmgDxgOLuCGoyadyRbG5VgDhcnoZo%2B%2BNCdIwkt214LldMz6Vf6UxJGBVF5JZVN0dvgeGlB1UDWCDr8Ni%2BKju8qqzDTyaLUBjqkAbNQ%2FFvUfSme4zjacZijRWoFi1XSeTgQ098g5K%2FTEmwRzMz5moM363mtRtYfU0GV7hPZR8KY5uvjv8oaSY5mKMKN7JAlNxQphwTimAFl1ulfFbAbm9vLj3bkDSQjnYZnG5j%2B%2Fm3d8jXpmM3DE7r8M10FRVrfPiRJbKmqaylXtdeHwpL%2Bm55fEEQsvkXihi5%2FccDe7Lb96LlsQT9u1rslLMPcVX6e&X-Amz-Signature=19fea1454416ca4a4c80d227087e176e189f6e3f9fdb66356d0ac627954836c8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
