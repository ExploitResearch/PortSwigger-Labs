# User ID controlled by request parameter with data leakage in redirect

### Target Goal - 

Obtain the API key for the user `carlos` and submit it as the solution

### Analysis/Exploitation -

**Login as user **`wiener`**:**

- Send the request to Burp Repeater.
- Change the "id" parameter to `carlos`.
- Observe that although the response is now
redirecting you to the home page, it has a body containing the API key
belonging to `carlos`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/4e833dd2-8913-48f3-932d-aefe23920fe4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SNN6ILQQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221917Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJrDP3RwUxG3xxxkmlrE4VA0Hq7sPUnDpuZXLEp5EuMAiEAj%2Br9qVhZFvsa3OY%2FM1jp%2BCuk1p9EUmKtp6dwJALQvb4qiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDC96X2B4ytyCLE7lYSrcA8D80VnQcrIledJcoTnW%2FQVMjTN9gD445NE9qnXOjn%2FaVJHurciJttpiGMwwjXZGZlKWcg6fl6TjbVl0MpyIKODaI5Mxr0Alkk5EvcvOGdEO1jv7%2BnBpzJNrUjsTFYFRcggdMbVzQ3NWSC5IhB9QOFs1igAWfYSyxYUr%2FZGXpt3MBHo8VFTyIpS5J%2BY22mX6Qgmzo5E99qmk%2FcDQQvhjDIMKfPhD4ioHk2%2FxOVc5%2Bm64%2BURxXIR%2B6bq6ud92sB6%2FBjY7JGmYVgi1NVPGE17Uuu6YTgRZsj1FaaJS88cMDJwGgf0fEmesLKgvhYT5gQzO675cCy0y2exMpP6qvUovg5gMqe4CfhwLck1uVL%2Ffq1C12cNd1rblKFF0yfVSzuRDQYFOjgQuptilTRpTnBMDC0YidcYnLAOM7%2BujCAmBk%2F3qvlhyzWRnRr3tcaXdLdDx0gPc95%2BlSV1RYixotKlHKc3dwGSjOO9tcE9h5TickDw4OMo5XFdDEAdVq2TwWMiz0rfgKIzErKqC7U8pVSRliAmzfCZ9G2Pp6a37ihAPFxEdGBytpwZvICicVplGGhUNzt50uy4Jld2kpOA6mIViKyv5%2BxVIglHGLg99vhjGM54uu4Juvfi%2FBcPavPs5MNWGo9QGOqUB%2BTnwIqmbJy6m1BfF4ECvZP4f0XNzlClkuLbXj9bA6iGSIIg91xZTN%2B6ja6O%2FVruWLOoY%2Ft%2Fqiq8f53jyD0nY0vMPXs%2FqcriwDZwf%2B5Hv6927LCNZHVP5E0VtUNqTtWFXHFTxUQ8wrb60Dlc9FOwG%2FqeiUT3QUmgzel%2BXuBRemNXqxClkSX6Dsi9zP3Xd8n0VfP6vGF7yPSs601wUGUpvBNbCIEzn&X-Amz-Signature=03983ba6cdbd0a064794c32cf956d747a868455fca1f9b1bfd2db205979366be&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Submit the API key.
