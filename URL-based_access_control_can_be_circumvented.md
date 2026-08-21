# URL-based access control can be circumvented

### Target Goal - 

Access the admin panel and delete the user `carlos`.

### Analysis/Exploitation -

there are navbar contents consisting of Home, Admin Panel, and My Account.When trying to access the Admin Panel, the web display the text “access denied”.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/013c9931-0643-4abd-99be-256cc8f9232a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466V5XH43X3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204648Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGBNZU3SEQ0%2FNRNo5nFhk59%2FOSWn9kkGpVjEpFzH4AIxAiAVbTYFHhBA%2BgY%2FeoctKVHLgPf5YUuvWE6IbTpFA4GevCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMPkG7YAPCsPSNfvqUKtwDXoB3AyiUtekHkdi5ic7PI%2BkSENBoqIL5kVXssYpTlO%2FSWHxw9qefIaF%2F87kigqLAJWdR5dHojdMDV%2BGqyxrd5z%2BCoQgiegW9huwVuis5Tu8imLkjroGf1%2BbYLbUpBlIHWTRa7SoZTSNuAlOltu8rDEr7Is5WLpAMDwu87nq%2B3NA2NhaHstLks6IiNf0T23phPlSkNJao%2F2iJqjIVXWhiQTXSqWfEm1jYIZG9RNrFjP%2Ft0rcF8R8LCLQNEKcltnCsvZueVFzijmPuNcYBBJjutzPvdg8qCjAXQUkLV5qzv%2FPJ5P2DrhufLwRjty5LcymaxXWAtm7ihut9b0uXVzrnjc3vVWww7OcYt%2FbG0tw0P3aJxDIPc%2B3BcmQA8k%2ByaOw01G%2FbQPyJ87q9W3QN1fAMovyoWJn5djhS8MouZXFN8o%2BhHB%2FVna4FlKucWwCaJncPyK7%2BWFZpO39Xx25shJ2oLxihbWr9pKJkqOQWAO%2F7Oo2VQKHb6cIhVF7U9bF8HVyzIYSUXXm6lhrSQ%2BQsUqWZqpuCrvJcFBdDdyEY6ninUFqqqIKCSE2ZFu7x7CgNPdO2jc63Ndlq2ctbD0jQ3FtcsMNsHDHUEX7NuZt8M5dEwbVz9aNkd%2BmEIEQFATIwpsai1AY6pgGS13OeKbY%2Fvb53BW%2B8%2FKjPeeWf5FN5C8xyJxkr%2FDBNnKeS%2F%2B7Z7nf2SFWcAPHb%2B0FcYGm5M4n8gSc24O82m4mjuaj%2FCL65%2BFhPCLEle9Ab13LL6GoZYel2OMIVWBwi1%2F8GgFgsWydFxs7YTDjB7skQyFajhw3Gp6%2F69CovSegRD%2FfVHjE5WxPq%2BJbyHmgbgf9F24uFXZQ1rweWTmxjiobc9tUyxhGf&X-Amz-Signature=b9fcd3cbfcabe2d8b0b364c644a02d92b50f79d5318f8b57ef9827ef661662f2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Let’s try to intercept when we want to access the admin panel using the burp suite. Here’s how it looks.

![](https://miro.medium.com/v2/resize:fit:700/0*glU9EajspkDB_z7h)

Based on the intercept results, the HTTP request method “Get” points to the /admin directory.

Let’s try to use non-standard HTTP headers that can replace the URL in the original request such as X-Original-URL to bypass admin access.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5140ce8e-fc5e-40a1-a9f3-a240ae459e82/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466V5XH43X3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204648Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGBNZU3SEQ0%2FNRNo5nFhk59%2FOSWn9kkGpVjEpFzH4AIxAiAVbTYFHhBA%2BgY%2FeoctKVHLgPf5YUuvWE6IbTpFA4GevCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMPkG7YAPCsPSNfvqUKtwDXoB3AyiUtekHkdi5ic7PI%2BkSENBoqIL5kVXssYpTlO%2FSWHxw9qefIaF%2F87kigqLAJWdR5dHojdMDV%2BGqyxrd5z%2BCoQgiegW9huwVuis5Tu8imLkjroGf1%2BbYLbUpBlIHWTRa7SoZTSNuAlOltu8rDEr7Is5WLpAMDwu87nq%2B3NA2NhaHstLks6IiNf0T23phPlSkNJao%2F2iJqjIVXWhiQTXSqWfEm1jYIZG9RNrFjP%2Ft0rcF8R8LCLQNEKcltnCsvZueVFzijmPuNcYBBJjutzPvdg8qCjAXQUkLV5qzv%2FPJ5P2DrhufLwRjty5LcymaxXWAtm7ihut9b0uXVzrnjc3vVWww7OcYt%2FbG0tw0P3aJxDIPc%2B3BcmQA8k%2ByaOw01G%2FbQPyJ87q9W3QN1fAMovyoWJn5djhS8MouZXFN8o%2BhHB%2FVna4FlKucWwCaJncPyK7%2BWFZpO39Xx25shJ2oLxihbWr9pKJkqOQWAO%2F7Oo2VQKHb6cIhVF7U9bF8HVyzIYSUXXm6lhrSQ%2BQsUqWZqpuCrvJcFBdDdyEY6ninUFqqqIKCSE2ZFu7x7CgNPdO2jc63Ndlq2ctbD0jQ3FtcsMNsHDHUEX7NuZt8M5dEwbVz9aNkd%2BmEIEQFATIwpsai1AY6pgGS13OeKbY%2Fvb53BW%2B8%2FKjPeeWf5FN5C8xyJxkr%2FDBNnKeS%2F%2B7Z7nf2SFWcAPHb%2B0FcYGm5M4n8gSc24O82m4mjuaj%2FCL65%2BFhPCLEle9Ab13LL6GoZYel2OMIVWBwi1%2F8GgFgsWydFxs7YTDjB7skQyFajhw3Gp6%2F69CovSegRD%2FfVHjE5WxPq%2BJbyHmgbgf9F24uFXZQ1rweWTmxjiobc9tUyxhGf&X-Amz-Signature=24299b1562e14d2f5402063cd52a654869f32c824ff1ab6811da19d57fa188eb&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3e4c3a57-ab8d-412d-8798-24a5085cba67/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466V5XH43X3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204648Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGBNZU3SEQ0%2FNRNo5nFhk59%2FOSWn9kkGpVjEpFzH4AIxAiAVbTYFHhBA%2BgY%2FeoctKVHLgPf5YUuvWE6IbTpFA4GevCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMPkG7YAPCsPSNfvqUKtwDXoB3AyiUtekHkdi5ic7PI%2BkSENBoqIL5kVXssYpTlO%2FSWHxw9qefIaF%2F87kigqLAJWdR5dHojdMDV%2BGqyxrd5z%2BCoQgiegW9huwVuis5Tu8imLkjroGf1%2BbYLbUpBlIHWTRa7SoZTSNuAlOltu8rDEr7Is5WLpAMDwu87nq%2B3NA2NhaHstLks6IiNf0T23phPlSkNJao%2F2iJqjIVXWhiQTXSqWfEm1jYIZG9RNrFjP%2Ft0rcF8R8LCLQNEKcltnCsvZueVFzijmPuNcYBBJjutzPvdg8qCjAXQUkLV5qzv%2FPJ5P2DrhufLwRjty5LcymaxXWAtm7ihut9b0uXVzrnjc3vVWww7OcYt%2FbG0tw0P3aJxDIPc%2B3BcmQA8k%2ByaOw01G%2FbQPyJ87q9W3QN1fAMovyoWJn5djhS8MouZXFN8o%2BhHB%2FVna4FlKucWwCaJncPyK7%2BWFZpO39Xx25shJ2oLxihbWr9pKJkqOQWAO%2F7Oo2VQKHb6cIhVF7U9bF8HVyzIYSUXXm6lhrSQ%2BQsUqWZqpuCrvJcFBdDdyEY6ninUFqqqIKCSE2ZFu7x7CgNPdO2jc63Ndlq2ctbD0jQ3FtcsMNsHDHUEX7NuZt8M5dEwbVz9aNkd%2BmEIEQFATIwpsai1AY6pgGS13OeKbY%2Fvb53BW%2B8%2FKjPeeWf5FN5C8xyJxkr%2FDBNnKeS%2F%2B7Z7nf2SFWcAPHb%2B0FcYGm5M4n8gSc24O82m4mjuaj%2FCL65%2BFhPCLEle9Ab13LL6GoZYel2OMIVWBwi1%2F8GgFgsWydFxs7YTDjB7skQyFajhw3Gp6%2F69CovSegRD%2FfVHjE5WxPq%2BJbyHmgbgf9F24uFXZQ1rweWTmxjiobc9tUyxhGf&X-Amz-Signature=87d5ed9b2614e7028fc920853897eadc3237aae83d85b9f19a98386015f23ad7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
