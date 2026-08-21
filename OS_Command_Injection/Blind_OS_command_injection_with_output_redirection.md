# Blind OS command injection with output redirection

### Goal - 

Exploit the blind command injection and redirect the output from the whoami command to the /var/www/images

### Analysis/Exploitation 

> 💡 You can redirect the output from the injected command into a file within the web root that you can access then retrieve using the browser. 
For example, if the application serves static resources from the filesystem location `/var/www/static`, then you can submit the following input:

```bash
& whoami > /var/www/static/whoami.txt &
```

The `>` character sends the output from the `whoami` command to the specified file. You can then use the browser to fetch `https://vulnerable-website.com/whoami.txt` to retrieve the file, and view the output from the injected command.

In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f419ccfa-6c51-4811-9269-500414a57519/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46673E3XUEY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210429Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDJq34ieVRrbpFGW9EWjxzmgoXTNNw8gRTbrpOe7ew%2B%2BgIhAJutwf%2BpEzKTGRrA%2FTKl4WRq%2Fn7GmjVzOF9sVcY4rjkXKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzhPooKz4QC7bCyD5cq3ANc1VXPpaIalEzClH%2FCXI2BT6Bdy3470RlG5%2BRxzNONY4eQPQCppWb3SlWIKIMsJH7aXgFAFNrWALaDwkf2lHDPQTEQZUgUTk1kvyShqMP5LMVHC7GsEZFzVmmcKUM53ahhozJ6mUDMFMNZ3K8w%2F%2Bzx1%2BPfjZ5HPxIjuVCsEzZtSHRVjrdRBvJ3tJEOIu%2BtkKFsWP4JvFRtpmBUw0QDhIkfV9pP%2BgpF%2BJ9X%2Bvvg%2F49J80PlgKAKxHlLbYDT%2BCwh7RrG38GtcPEvhVkvgkOGqLVlYJz4iOc%2BQgwvKSssWP77yV6BmGUq0ZFzI1AxrItHGY%2B81TOMghHf5aeD7w6OrOtV4Cc81m%2Bz4C2mBzwTluqmlSZ%2FCQznMUeumjlNGDCogPQVqjcyUujE4mxFS4PbCpVp9Gfrifl4SLHeIdFJmTWYcItvduH6HNXqMdkJUOyUlYVQp0OssX2MFrEeczMjw8mb2N9jJUY2BWC4B8VQ4yUVkeSc6YXI0e6%2B1oT1gixMS3gQc7M01AfrvyZabMrMAbwYC%2BUVFfzGRFexms3VPcvnzgQHcSa2WooRmGc08pA7MTWWIbyjw1ystzDyvdPoLiuHTqV0M9ivNXwFWB9Q%2BdeAgNebsxWbGfluYe7%2B0TD5yKLUBjqkAXKm8KtkiQXbrOqDgKse1UZ1Z0qIMowU1wNSK5dB6AdQPpxYuGTLsERWxo7JsbHLdq6URJxybLjBFFA%2F7rD63z%2BTLHMm4lzpY2QFcPoALaFjAxAaFQMyhavZUJ31iQv35WLrN9waOJAh2M9px3jph6n9m8r%2FawHhQnKQ1Re3fQulSeGgJLcu14D69KlPxK4EEQiDVlWRZhLj2ZZg5rX8uy4U91Ws&X-Amz-Signature=7a71a6c5ef2617eb1815e0195b590f8e0c03bb576a505b14a20f47efb294a7ba&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now, instead of triggering a time delay, we can also **redirect the command’s output to a file, and stored it to where we can access.**

In the home page, we can see there are some product images:

Typically you’ll **stored the output to a static file**, like `images`.As we can see, **they are at **`/image`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e029e26c-adab-42eb-8b75-cc03aa5cb267/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46673E3XUEY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210429Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDJq34ieVRrbpFGW9EWjxzmgoXTNNw8gRTbrpOe7ew%2B%2BgIhAJutwf%2BpEzKTGRrA%2FTKl4WRq%2Fn7GmjVzOF9sVcY4rjkXKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzhPooKz4QC7bCyD5cq3ANc1VXPpaIalEzClH%2FCXI2BT6Bdy3470RlG5%2BRxzNONY4eQPQCppWb3SlWIKIMsJH7aXgFAFNrWALaDwkf2lHDPQTEQZUgUTk1kvyShqMP5LMVHC7GsEZFzVmmcKUM53ahhozJ6mUDMFMNZ3K8w%2F%2Bzx1%2BPfjZ5HPxIjuVCsEzZtSHRVjrdRBvJ3tJEOIu%2BtkKFsWP4JvFRtpmBUw0QDhIkfV9pP%2BgpF%2BJ9X%2Bvvg%2F49J80PlgKAKxHlLbYDT%2BCwh7RrG38GtcPEvhVkvgkOGqLVlYJz4iOc%2BQgwvKSssWP77yV6BmGUq0ZFzI1AxrItHGY%2B81TOMghHf5aeD7w6OrOtV4Cc81m%2Bz4C2mBzwTluqmlSZ%2FCQznMUeumjlNGDCogPQVqjcyUujE4mxFS4PbCpVp9Gfrifl4SLHeIdFJmTWYcItvduH6HNXqMdkJUOyUlYVQp0OssX2MFrEeczMjw8mb2N9jJUY2BWC4B8VQ4yUVkeSc6YXI0e6%2B1oT1gixMS3gQc7M01AfrvyZabMrMAbwYC%2BUVFfzGRFexms3VPcvnzgQHcSa2WooRmGc08pA7MTWWIbyjw1ystzDyvdPoLiuHTqV0M9ivNXwFWB9Q%2BdeAgNebsxWbGfluYe7%2B0TD5yKLUBjqkAXKm8KtkiQXbrOqDgKse1UZ1Z0qIMowU1wNSK5dB6AdQPpxYuGTLsERWxo7JsbHLdq6URJxybLjBFFA%2F7rD63z%2BTLHMm4lzpY2QFcPoALaFjAxAaFQMyhavZUJ31iQv35WLrN9waOJAh2M9px3jph6n9m8r%2FawHhQnKQ1Re3fQulSeGgJLcu14D69KlPxK4EEQiDVlWRZhLj2ZZg5rX8uy4U91Ws&X-Amz-Signature=a31a111d074d75cc483a24c38d67b2b660ab5ef866879f5c29b8a6ede39239fd&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

To redirect command’s output to a file, we can put it to `/var/www/image/<filename>`.since it is mentionted in lab description that Writeable folder is at `/var/www/images/`

> **Note: **In Linux, web root is usually located in **/var/www/**.

The command to execute is `whoami > /var/www/images/whoami.txt `to write the file. Inject it into the email argument. And as in the previous lab, commenting out the remainder results in a `200 OK`, while not doing so results in `500 Internal Server Error`. Both ways work though.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/dd85ec37-3d71-4f42-94bf-b434ad755201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46673E3XUEY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210429Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDJq34ieVRrbpFGW9EWjxzmgoXTNNw8gRTbrpOe7ew%2B%2BgIhAJutwf%2BpEzKTGRrA%2FTKl4WRq%2Fn7GmjVzOF9sVcY4rjkXKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzhPooKz4QC7bCyD5cq3ANc1VXPpaIalEzClH%2FCXI2BT6Bdy3470RlG5%2BRxzNONY4eQPQCppWb3SlWIKIMsJH7aXgFAFNrWALaDwkf2lHDPQTEQZUgUTk1kvyShqMP5LMVHC7GsEZFzVmmcKUM53ahhozJ6mUDMFMNZ3K8w%2F%2Bzx1%2BPfjZ5HPxIjuVCsEzZtSHRVjrdRBvJ3tJEOIu%2BtkKFsWP4JvFRtpmBUw0QDhIkfV9pP%2BgpF%2BJ9X%2Bvvg%2F49J80PlgKAKxHlLbYDT%2BCwh7RrG38GtcPEvhVkvgkOGqLVlYJz4iOc%2BQgwvKSssWP77yV6BmGUq0ZFzI1AxrItHGY%2B81TOMghHf5aeD7w6OrOtV4Cc81m%2Bz4C2mBzwTluqmlSZ%2FCQznMUeumjlNGDCogPQVqjcyUujE4mxFS4PbCpVp9Gfrifl4SLHeIdFJmTWYcItvduH6HNXqMdkJUOyUlYVQp0OssX2MFrEeczMjw8mb2N9jJUY2BWC4B8VQ4yUVkeSc6YXI0e6%2B1oT1gixMS3gQc7M01AfrvyZabMrMAbwYC%2BUVFfzGRFexms3VPcvnzgQHcSa2WooRmGc08pA7MTWWIbyjw1ystzDyvdPoLiuHTqV0M9ivNXwFWB9Q%2BdeAgNebsxWbGfluYe7%2B0TD5yKLUBjqkAXKm8KtkiQXbrOqDgKse1UZ1Z0qIMowU1wNSK5dB6AdQPpxYuGTLsERWxo7JsbHLdq6URJxybLjBFFA%2F7rD63z%2BTLHMm4lzpY2QFcPoALaFjAxAaFQMyhavZUJ31iQv35WLrN9waOJAh2M9px3jph6n9m8r%2FawHhQnKQ1Re3fQulSeGgJLcu14D69KlPxK4EEQiDVlWRZhLj2ZZg5rX8uy4U91Ws&X-Amz-Signature=982db22c76e383dae9bdd719a53be1e498018ef39b1e41156297cf45ca79143f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Access the file**

Now the file is in `/var/www/images`, but the path to it within the application is unknown and perhaps not even accessible directly. But I can utilize the way the application includes its images with a GET request to `/image?filename=`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1796e77c-5656-43a4-8c91-3fc0bde988d7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46673E3XUEY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210429Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDJq34ieVRrbpFGW9EWjxzmgoXTNNw8gRTbrpOe7ew%2B%2BgIhAJutwf%2BpEzKTGRrA%2FTKl4WRq%2Fn7GmjVzOF9sVcY4rjkXKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzhPooKz4QC7bCyD5cq3ANc1VXPpaIalEzClH%2FCXI2BT6Bdy3470RlG5%2BRxzNONY4eQPQCppWb3SlWIKIMsJH7aXgFAFNrWALaDwkf2lHDPQTEQZUgUTk1kvyShqMP5LMVHC7GsEZFzVmmcKUM53ahhozJ6mUDMFMNZ3K8w%2F%2Bzx1%2BPfjZ5HPxIjuVCsEzZtSHRVjrdRBvJ3tJEOIu%2BtkKFsWP4JvFRtpmBUw0QDhIkfV9pP%2BgpF%2BJ9X%2Bvvg%2F49J80PlgKAKxHlLbYDT%2BCwh7RrG38GtcPEvhVkvgkOGqLVlYJz4iOc%2BQgwvKSssWP77yV6BmGUq0ZFzI1AxrItHGY%2B81TOMghHf5aeD7w6OrOtV4Cc81m%2Bz4C2mBzwTluqmlSZ%2FCQznMUeumjlNGDCogPQVqjcyUujE4mxFS4PbCpVp9Gfrifl4SLHeIdFJmTWYcItvduH6HNXqMdkJUOyUlYVQp0OssX2MFrEeczMjw8mb2N9jJUY2BWC4B8VQ4yUVkeSc6YXI0e6%2B1oT1gixMS3gQc7M01AfrvyZabMrMAbwYC%2BUVFfzGRFexms3VPcvnzgQHcSa2WooRmGc08pA7MTWWIbyjw1ystzDyvdPoLiuHTqV0M9ivNXwFWB9Q%2BdeAgNebsxWbGfluYe7%2B0TD5yKLUBjqkAXKm8KtkiQXbrOqDgKse1UZ1Z0qIMowU1wNSK5dB6AdQPpxYuGTLsERWxo7JsbHLdq6URJxybLjBFFA%2F7rD63z%2BTLHMm4lzpY2QFcPoALaFjAxAaFQMyhavZUJ31iQv35WLrN9waOJAh2M9px3jph6n9m8r%2FawHhQnKQ1Re3fQulSeGgJLcu14D69KlPxK4EEQiDVlWRZhLj2ZZg5rX8uy4U91Ws&X-Amz-Signature=87523a05fb5baae26da6fc55cef38aea0acd4ffd47e5941224427ca64d349655&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 **summary
**

  1. Find & Confirm blind command injection
-email field
  1. Check location from where application serves static resources, here images 
  1. Redirect output to file at that static location
  1. Check if file was created by accessing it
