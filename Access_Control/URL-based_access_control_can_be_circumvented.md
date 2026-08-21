# URL-based access control can be circumvented

### Target Goal - 

Access the admin panel and delete the user `carlos`.

### Analysis/Exploitation -

there are navbar contents consisting of Home, Admin Panel, and My Account.When trying to access the Admin Panel, the web display the text “access denied”.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/013c9931-0643-4abd-99be-256cc8f9232a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46672SGJYTU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215520Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD2%2B0YnyGP26HzFjUX5v%2F6eMRVRro4wkdx9gBKmGkaZzAIhAJKcDmWzag94hbwzVB5D92mudIOj5EK7pbaGtMbkIMFCKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyQlXzks8A7PkHdlyYq3ANil7qy1nQDSc8Bze7lrjGBGFCTVnjMe%2BTvNt3TvBX5iYYndgSkO725oVktsr7EiBcTH3%2BlniZNRQZDfyh1LtTEuJmVFn7ZbezefX3EOuU3GJs0h0cYWXPcJFXjxZyeepEjGJLJw5Mk5K%2F9TlsUUiVztwAEgC7yjZPTcHbrsEQ%2Fh4xvF61%2F8II5Klbapa6kXJMcLmsV%2F%2BBeHcg0oNDN3NnxIqTrzSnwLm1LZxxGOzLT9fD0sQK2PLVWOBCpLC88MLA2B9WgSmQMic9rixAQos3cSMeZu2jqcEiilJNazDogciFWR0MTMEIxfmB8Lz6ROO3dP988LbBWMmmem%2BJmE6aArc%2F0b8%2BeEE6PHHQyz7gNbGofmSxsD8b%2BYViVTmaVKNlxRvW6RzX69CJu4T2Mqjwnpap0GMBxCVi7WJA6PDAUL75R6XuV8MliIpy3PheCGOBp8C1tZyrqCL46TsbnJRtgi5h%2BYacx4%2FS%2B4FX%2BplAq%2Fh6fbg8MJ0QIIHfzXKlkTxN9jqqpq0A5RDoZRMInhoQRy8IxcKLuJsTuipo54ZzIIoCnznB71spbTCAUdefs1DUkvy2ohW8ptnexfzUDrK9NmTf16oy%2BH02aRH0upBrRAuV19cd97vKWrYfjwjCph6PUBjqkAZjdxSTjbdRFme0vk6yp1AyJhKbimDZFruyB2wXxrzBNIM5M8x0z1zbQMuZml8hEVtcSek%2BtALhlqrYwmmu%2BtEiSCVPlK3MHQxLoFrtkCmUi0Iel3PPKkx4bQZZkR%2FkCUhO5I6uRcR7UXTTTPuED6OQJm3IUEbOhqK7%2F8uyCiRuqkLCYZobLAg%2BW9F09%2Fn8xdfiO9GcjNoMfqzdEHmhL%2FxxM%2F7k1&X-Amz-Signature=ea8bbebc63ba0c8399a9712f6cdb1110e1a9dfb3580f977f08b7aada00c72e84&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Let’s try to intercept when we want to access the admin panel using the burp suite. Here’s how it looks.

![](https://miro.medium.com/v2/resize:fit:700/0*glU9EajspkDB_z7h)

Based on the intercept results, the HTTP request method “Get” points to the /admin directory.

Let’s try to use non-standard HTTP headers that can replace the URL in the original request such as X-Original-URL to bypass admin access.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5140ce8e-fc5e-40a1-a9f3-a240ae459e82/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46672SGJYTU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215520Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD2%2B0YnyGP26HzFjUX5v%2F6eMRVRro4wkdx9gBKmGkaZzAIhAJKcDmWzag94hbwzVB5D92mudIOj5EK7pbaGtMbkIMFCKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyQlXzks8A7PkHdlyYq3ANil7qy1nQDSc8Bze7lrjGBGFCTVnjMe%2BTvNt3TvBX5iYYndgSkO725oVktsr7EiBcTH3%2BlniZNRQZDfyh1LtTEuJmVFn7ZbezefX3EOuU3GJs0h0cYWXPcJFXjxZyeepEjGJLJw5Mk5K%2F9TlsUUiVztwAEgC7yjZPTcHbrsEQ%2Fh4xvF61%2F8II5Klbapa6kXJMcLmsV%2F%2BBeHcg0oNDN3NnxIqTrzSnwLm1LZxxGOzLT9fD0sQK2PLVWOBCpLC88MLA2B9WgSmQMic9rixAQos3cSMeZu2jqcEiilJNazDogciFWR0MTMEIxfmB8Lz6ROO3dP988LbBWMmmem%2BJmE6aArc%2F0b8%2BeEE6PHHQyz7gNbGofmSxsD8b%2BYViVTmaVKNlxRvW6RzX69CJu4T2Mqjwnpap0GMBxCVi7WJA6PDAUL75R6XuV8MliIpy3PheCGOBp8C1tZyrqCL46TsbnJRtgi5h%2BYacx4%2FS%2B4FX%2BplAq%2Fh6fbg8MJ0QIIHfzXKlkTxN9jqqpq0A5RDoZRMInhoQRy8IxcKLuJsTuipo54ZzIIoCnznB71spbTCAUdefs1DUkvy2ohW8ptnexfzUDrK9NmTf16oy%2BH02aRH0upBrRAuV19cd97vKWrYfjwjCph6PUBjqkAZjdxSTjbdRFme0vk6yp1AyJhKbimDZFruyB2wXxrzBNIM5M8x0z1zbQMuZml8hEVtcSek%2BtALhlqrYwmmu%2BtEiSCVPlK3MHQxLoFrtkCmUi0Iel3PPKkx4bQZZkR%2FkCUhO5I6uRcR7UXTTTPuED6OQJm3IUEbOhqK7%2F8uyCiRuqkLCYZobLAg%2BW9F09%2Fn8xdfiO9GcjNoMfqzdEHmhL%2FxxM%2F7k1&X-Amz-Signature=0485cd3967ccd65895a282a830b87f83eb4a0e82276d23398364982a6c604555&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3e4c3a57-ab8d-412d-8798-24a5085cba67/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46672SGJYTU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215520Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD2%2B0YnyGP26HzFjUX5v%2F6eMRVRro4wkdx9gBKmGkaZzAIhAJKcDmWzag94hbwzVB5D92mudIOj5EK7pbaGtMbkIMFCKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgyQlXzks8A7PkHdlyYq3ANil7qy1nQDSc8Bze7lrjGBGFCTVnjMe%2BTvNt3TvBX5iYYndgSkO725oVktsr7EiBcTH3%2BlniZNRQZDfyh1LtTEuJmVFn7ZbezefX3EOuU3GJs0h0cYWXPcJFXjxZyeepEjGJLJw5Mk5K%2F9TlsUUiVztwAEgC7yjZPTcHbrsEQ%2Fh4xvF61%2F8II5Klbapa6kXJMcLmsV%2F%2BBeHcg0oNDN3NnxIqTrzSnwLm1LZxxGOzLT9fD0sQK2PLVWOBCpLC88MLA2B9WgSmQMic9rixAQos3cSMeZu2jqcEiilJNazDogciFWR0MTMEIxfmB8Lz6ROO3dP988LbBWMmmem%2BJmE6aArc%2F0b8%2BeEE6PHHQyz7gNbGofmSxsD8b%2BYViVTmaVKNlxRvW6RzX69CJu4T2Mqjwnpap0GMBxCVi7WJA6PDAUL75R6XuV8MliIpy3PheCGOBp8C1tZyrqCL46TsbnJRtgi5h%2BYacx4%2FS%2B4FX%2BplAq%2Fh6fbg8MJ0QIIHfzXKlkTxN9jqqpq0A5RDoZRMInhoQRy8IxcKLuJsTuipo54ZzIIoCnznB71spbTCAUdefs1DUkvy2ohW8ptnexfzUDrK9NmTf16oy%2BH02aRH0upBrRAuV19cd97vKWrYfjwjCph6PUBjqkAZjdxSTjbdRFme0vk6yp1AyJhKbimDZFruyB2wXxrzBNIM5M8x0z1zbQMuZml8hEVtcSek%2BtALhlqrYwmmu%2BtEiSCVPlK3MHQxLoFrtkCmUi0Iel3PPKkx4bQZZkR%2FkCUhO5I6uRcR7UXTTTPuED6OQJm3IUEbOhqK7%2F8uyCiRuqkLCYZobLAg%2BW9F09%2Fn8xdfiO9GcjNoMfqzdEHmhL%2FxxM%2F7k1&X-Amz-Signature=708218e08a2200228fbc2de3fcb050fd3205875e943ded9ecd751ea06159a35e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
