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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f419ccfa-6c51-4811-9269-500414a57519/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WCISNGXT%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222004Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGJzDe2STentsdryoO96QFbaTvDPNgW55MNsZWeia2BxAiAZsaZzrDJPMcVFcgmpfHZ%2F9t0a%2Fs1I5VtObbFvEzFkJiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMDWnZ5jvOTYERUuQQKtwDyutcHw%2BUGGmBbduI7vfDrfu9HEGVDXmFU8yNvq0a4hRoVM1aT8wzWCCkLKzIIlYWJdDg0WZpT4KdBNYG%2FzkNitc1q%2B3s5au535XivcBJK4TJG%2FjRhdhAQ928%2B2l0aI%2FiIvWgmmB3VGKUFVTZiuQ6MCAuo5gxYu9gh5Gw6I7u43FggSBhqAzYL7X018q94cHQ9gdi2Bvxpx92PB5UO%2F%2FPZThvnHhCj6foguIxqauopr2VhLnVB6j7gpXAVpop%2F5KZrF6qribUsYyuIq1k2RKHEzJKzV4wEdGvkOBHmBRRMqoV6RkNRRN1JltgwgTHPUveThrGdJ%2Ba6e%2FQj1O5fBzb1p6Etdv3nqBLibRgt8onY%2BYMgv7%2Fd41FhPmaNubsqdMA7yz%2B2OMk7QckVOiAXzE9kmgwG1ouiYvoOhNqayXZyV0gvnpHBGYVlXq1YI9%2FgmmTa0Ju2pfx5FvG%2B%2BI7AbV66Ze2O5l929r07amU0DV4vaLTYwg29HPSGgWzrVUxGbrFXXxuVehiVwKTM9W5pxau%2FI0zeitir6KBMoxUNweAytHfXh0RwO%2Fn0anXzu1oS%2BPjRJZp1jWGPwlfT%2B4VAkLLvRbUMVYvHG3zbA%2F5GJVB0ex2W7F4qNmSLNVbqnww0ISj1AY6pgFiRYJ1YAMTAXGrUo7dg92Rf60HRDzgkqkB%2FNyzLkZAcSpXJ4Yh3Ar2PZA8Bo4bBLgTU1maby8FAtqLsKtgrdAzNb6Rjdp5VBIzAS1AOO46eX2meJs1ieDqhhaZJcCScMf3YxJTGTl79CUFxY9sfCx8b3RiZIMG7M3RQBH3Xzxf6cFaFG2cadaU1EPdsddZtRsJKiZgXgYgY%2B1Tspeg1tzCsI2bHR3x&X-Amz-Signature=dbdd0e62551f803a742f674d81b43745d72a458021fb997ae663899d1e8b313c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now, instead of triggering a time delay, we can also **redirect the command’s output to a file, and stored it to where we can access.**

In the home page, we can see there are some product images:

Typically you’ll **stored the output to a static file**, like `images`.As we can see, **they are at **`/image`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e029e26c-adab-42eb-8b75-cc03aa5cb267/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WCISNGXT%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222004Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGJzDe2STentsdryoO96QFbaTvDPNgW55MNsZWeia2BxAiAZsaZzrDJPMcVFcgmpfHZ%2F9t0a%2Fs1I5VtObbFvEzFkJiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMDWnZ5jvOTYERUuQQKtwDyutcHw%2BUGGmBbduI7vfDrfu9HEGVDXmFU8yNvq0a4hRoVM1aT8wzWCCkLKzIIlYWJdDg0WZpT4KdBNYG%2FzkNitc1q%2B3s5au535XivcBJK4TJG%2FjRhdhAQ928%2B2l0aI%2FiIvWgmmB3VGKUFVTZiuQ6MCAuo5gxYu9gh5Gw6I7u43FggSBhqAzYL7X018q94cHQ9gdi2Bvxpx92PB5UO%2F%2FPZThvnHhCj6foguIxqauopr2VhLnVB6j7gpXAVpop%2F5KZrF6qribUsYyuIq1k2RKHEzJKzV4wEdGvkOBHmBRRMqoV6RkNRRN1JltgwgTHPUveThrGdJ%2Ba6e%2FQj1O5fBzb1p6Etdv3nqBLibRgt8onY%2BYMgv7%2Fd41FhPmaNubsqdMA7yz%2B2OMk7QckVOiAXzE9kmgwG1ouiYvoOhNqayXZyV0gvnpHBGYVlXq1YI9%2FgmmTa0Ju2pfx5FvG%2B%2BI7AbV66Ze2O5l929r07amU0DV4vaLTYwg29HPSGgWzrVUxGbrFXXxuVehiVwKTM9W5pxau%2FI0zeitir6KBMoxUNweAytHfXh0RwO%2Fn0anXzu1oS%2BPjRJZp1jWGPwlfT%2B4VAkLLvRbUMVYvHG3zbA%2F5GJVB0ex2W7F4qNmSLNVbqnww0ISj1AY6pgFiRYJ1YAMTAXGrUo7dg92Rf60HRDzgkqkB%2FNyzLkZAcSpXJ4Yh3Ar2PZA8Bo4bBLgTU1maby8FAtqLsKtgrdAzNb6Rjdp5VBIzAS1AOO46eX2meJs1ieDqhhaZJcCScMf3YxJTGTl79CUFxY9sfCx8b3RiZIMG7M3RQBH3Xzxf6cFaFG2cadaU1EPdsddZtRsJKiZgXgYgY%2B1Tspeg1tzCsI2bHR3x&X-Amz-Signature=1de8b3dfe20e2f772d79ed2d1ec246bb7e489152dd24c6937cd51db38dc3ecb6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

To redirect command’s output to a file, we can put it to `/var/www/image/<filename>`.since it is mentionted in lab description that Writeable folder is at `/var/www/images/`

{% hint style="info" %}
**Note: **In Linux, web root is usually located in <span style="color: #E03E1B">**/var/www/**</span>.
{% endhint %}

The command to execute is `whoami > /var/www/images/whoami.txt `to write the file. Inject it into the email argument. And as in the previous lab, commenting out the remainder results in a `200 OK`, while not doing so results in `500 Internal Server Error`. Both ways work though.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/dd85ec37-3d71-4f42-94bf-b434ad755201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WCISNGXT%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222004Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGJzDe2STentsdryoO96QFbaTvDPNgW55MNsZWeia2BxAiAZsaZzrDJPMcVFcgmpfHZ%2F9t0a%2Fs1I5VtObbFvEzFkJiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMDWnZ5jvOTYERUuQQKtwDyutcHw%2BUGGmBbduI7vfDrfu9HEGVDXmFU8yNvq0a4hRoVM1aT8wzWCCkLKzIIlYWJdDg0WZpT4KdBNYG%2FzkNitc1q%2B3s5au535XivcBJK4TJG%2FjRhdhAQ928%2B2l0aI%2FiIvWgmmB3VGKUFVTZiuQ6MCAuo5gxYu9gh5Gw6I7u43FggSBhqAzYL7X018q94cHQ9gdi2Bvxpx92PB5UO%2F%2FPZThvnHhCj6foguIxqauopr2VhLnVB6j7gpXAVpop%2F5KZrF6qribUsYyuIq1k2RKHEzJKzV4wEdGvkOBHmBRRMqoV6RkNRRN1JltgwgTHPUveThrGdJ%2Ba6e%2FQj1O5fBzb1p6Etdv3nqBLibRgt8onY%2BYMgv7%2Fd41FhPmaNubsqdMA7yz%2B2OMk7QckVOiAXzE9kmgwG1ouiYvoOhNqayXZyV0gvnpHBGYVlXq1YI9%2FgmmTa0Ju2pfx5FvG%2B%2BI7AbV66Ze2O5l929r07amU0DV4vaLTYwg29HPSGgWzrVUxGbrFXXxuVehiVwKTM9W5pxau%2FI0zeitir6KBMoxUNweAytHfXh0RwO%2Fn0anXzu1oS%2BPjRJZp1jWGPwlfT%2B4VAkLLvRbUMVYvHG3zbA%2F5GJVB0ex2W7F4qNmSLNVbqnww0ISj1AY6pgFiRYJ1YAMTAXGrUo7dg92Rf60HRDzgkqkB%2FNyzLkZAcSpXJ4Yh3Ar2PZA8Bo4bBLgTU1maby8FAtqLsKtgrdAzNb6Rjdp5VBIzAS1AOO46eX2meJs1ieDqhhaZJcCScMf3YxJTGTl79CUFxY9sfCx8b3RiZIMG7M3RQBH3Xzxf6cFaFG2cadaU1EPdsddZtRsJKiZgXgYgY%2B1Tspeg1tzCsI2bHR3x&X-Amz-Signature=514aed93763a3674ebb031f5993b1299dc81534dc0c206d0b9b622afafa034b1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Access the file**

Now the file is in `/var/www/images`, but the path to it within the application is unknown and perhaps not even accessible directly. But I can utilize the way the application includes its images with a GET request to `/image?filename=`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1796e77c-5656-43a4-8c91-3fc0bde988d7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WCISNGXT%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222004Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGJzDe2STentsdryoO96QFbaTvDPNgW55MNsZWeia2BxAiAZsaZzrDJPMcVFcgmpfHZ%2F9t0a%2Fs1I5VtObbFvEzFkJiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMDWnZ5jvOTYERUuQQKtwDyutcHw%2BUGGmBbduI7vfDrfu9HEGVDXmFU8yNvq0a4hRoVM1aT8wzWCCkLKzIIlYWJdDg0WZpT4KdBNYG%2FzkNitc1q%2B3s5au535XivcBJK4TJG%2FjRhdhAQ928%2B2l0aI%2FiIvWgmmB3VGKUFVTZiuQ6MCAuo5gxYu9gh5Gw6I7u43FggSBhqAzYL7X018q94cHQ9gdi2Bvxpx92PB5UO%2F%2FPZThvnHhCj6foguIxqauopr2VhLnVB6j7gpXAVpop%2F5KZrF6qribUsYyuIq1k2RKHEzJKzV4wEdGvkOBHmBRRMqoV6RkNRRN1JltgwgTHPUveThrGdJ%2Ba6e%2FQj1O5fBzb1p6Etdv3nqBLibRgt8onY%2BYMgv7%2Fd41FhPmaNubsqdMA7yz%2B2OMk7QckVOiAXzE9kmgwG1ouiYvoOhNqayXZyV0gvnpHBGYVlXq1YI9%2FgmmTa0Ju2pfx5FvG%2B%2BI7AbV66Ze2O5l929r07amU0DV4vaLTYwg29HPSGgWzrVUxGbrFXXxuVehiVwKTM9W5pxau%2FI0zeitir6KBMoxUNweAytHfXh0RwO%2Fn0anXzu1oS%2BPjRJZp1jWGPwlfT%2B4VAkLLvRbUMVYvHG3zbA%2F5GJVB0ex2W7F4qNmSLNVbqnww0ISj1AY6pgFiRYJ1YAMTAXGrUo7dg92Rf60HRDzgkqkB%2FNyzLkZAcSpXJ4Yh3Ar2PZA8Bo4bBLgTU1maby8FAtqLsKtgrdAzNb6Rjdp5VBIzAS1AOO46eX2meJs1ieDqhhaZJcCScMf3YxJTGTl79CUFxY9sfCx8b3RiZIMG7M3RQBH3Xzxf6cFaFG2cadaU1EPdsddZtRsJKiZgXgYgY%2B1Tspeg1tzCsI2bHR3x&X-Amz-Signature=68868eefd79f6efc3a67da5ac1b718bf2b21a02294582292041be678af0dbc45&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 **summary

**

  1. Find & Confirm blind command injection
-email field
  1. Check location from where application serves static resources, here images 
  1. Redirect output to file at that static location
  1. Check if file was created by accessing it
