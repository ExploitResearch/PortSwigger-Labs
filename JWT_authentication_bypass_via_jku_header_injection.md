# JWT authentication bypass via jku header injection

## Goal - 

Forge a JWT that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

## Analysis/Exploitation -

**Login as user **`wiener`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1aaa703c-3df7-434a-b6f9-396a8e9cf1be/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662TOHYB22%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204741Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBFJW57qJYr68xK2aNU7QFayYVhgoiwlPbTOn%2BwpA%2BsfAiB7GPNGblh0U1fwW5gHOO71JloWiBfZtXsuNEeclVqFCiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5bkFmozwYgwGJhY5KtwD%2FtRFHHH3IgnT1zDEXR%2BMpS3AlXESqvnZ61yPYG5eO0Tzxgxb7yEOwl4xefzmJ%2FN0%2Fv8xati%2BUrIIyih3x1QdpKDjS8pJXOPftQwWWjkkVklH4z8GoqTNVqutmd0xrj6Qn9fwPE6yNNaDDfg57FCgmoV%2FrrLtSOw8gjHetRsRcn5hJWGRQ3QRAvFgZjj9C7B5%2BLfKiaXN3FSjHPa3P397O%2B5Vu8xZN8KqkmO5mOKfWCaa6z4iHz7e1h%2Fl2MSvvEQ4JCQG7qRUOeXqm4pCuRCmmC1VtCcZYmZUoj0brtJ8qoWExwEXNyhnPZ2uIQ8xiRNIP0Tl7QtqTpSbdco0ZvmTKqYfzXANM8V0EmNXu8m4ApL6wkVmDK9iQAP9e0va%2BFDRlnrvZDX2Ce%2FZBZaLAIgxcXie1TX19WNpnuovgS%2BOZvjbNMcwdfxaV9Te%2BBKAIpbgQx5%2B4RZaMP9ZQ3KrxeuiyM7jQtFwPqGVgBOqtN8ux15k5JvRmkQeQSokliFxzlHainY%2BsBLMQcLc8WlbLyHfb3tec0H4Wg6aIec%2FtO9RylhuM0qUb8xit%2B2usfz5TMrqG1DylFrASWIGotGkOT5Ix5ho9NHHCG4Q%2B70hIf7XoYGOt7kY3L8%2FW%2FZqvkgwzMai1AY6pgGUhdkwK5QvJexZXym73xl6JIaNXvRjnzZE4GHoZLUcDGHKGB6vUnBxwapA1LGwr2%2Bb%2FoN6c7ivklXg0bdkzT%2BlrXBEGtgtXgDyLcRvTWnCFQKrGpo7agehXATzSn5WBjTOrUu8wBmMVOICNdE0C7pbg5NjMZRNu84DamiSvec0sS4%2BFsu5ymmtmGO6ZUvwbDK23lY1XX4saKoEFdQ60zEseM3UdAu%2B&X-Amz-Signature=e75fc104db5278828f13b8d92c5e080628d7548f285b60ec49104c6bc51230d9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the header’s `alg`, it tells that **it’s using RS256(RSA + SHA-256) algorithm.**

**In the lab’s background, it said:**

> The server supports the jku(JWK Set URL) parameter in the JWT header. However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key.

### Upload a malicious JWK Set of **new generated RSA key pair:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9b6e3d3c-9638-4f47-9d99-213faa330981/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662TOHYB22%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204741Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBFJW57qJYr68xK2aNU7QFayYVhgoiwlPbTOn%2BwpA%2BsfAiB7GPNGblh0U1fwW5gHOO71JloWiBfZtXsuNEeclVqFCiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5bkFmozwYgwGJhY5KtwD%2FtRFHHH3IgnT1zDEXR%2BMpS3AlXESqvnZ61yPYG5eO0Tzxgxb7yEOwl4xefzmJ%2FN0%2Fv8xati%2BUrIIyih3x1QdpKDjS8pJXOPftQwWWjkkVklH4z8GoqTNVqutmd0xrj6Qn9fwPE6yNNaDDfg57FCgmoV%2FrrLtSOw8gjHetRsRcn5hJWGRQ3QRAvFgZjj9C7B5%2BLfKiaXN3FSjHPa3P397O%2B5Vu8xZN8KqkmO5mOKfWCaa6z4iHz7e1h%2Fl2MSvvEQ4JCQG7qRUOeXqm4pCuRCmmC1VtCcZYmZUoj0brtJ8qoWExwEXNyhnPZ2uIQ8xiRNIP0Tl7QtqTpSbdco0ZvmTKqYfzXANM8V0EmNXu8m4ApL6wkVmDK9iQAP9e0va%2BFDRlnrvZDX2Ce%2FZBZaLAIgxcXie1TX19WNpnuovgS%2BOZvjbNMcwdfxaV9Te%2BBKAIpbgQx5%2B4RZaMP9ZQ3KrxeuiyM7jQtFwPqGVgBOqtN8ux15k5JvRmkQeQSokliFxzlHainY%2BsBLMQcLc8WlbLyHfb3tec0H4Wg6aIec%2FtO9RylhuM0qUb8xit%2B2usfz5TMrqG1DylFrASWIGotGkOT5Ix5ho9NHHCG4Q%2B70hIf7XoYGOt7kY3L8%2FW%2FZqvkgwzMai1AY6pgGUhdkwK5QvJexZXym73xl6JIaNXvRjnzZE4GHoZLUcDGHKGB6vUnBxwapA1LGwr2%2Bb%2FoN6c7ivklXg0bdkzT%2BlrXBEGtgtXgDyLcRvTWnCFQKrGpo7agehXATzSn5WBjTOrUu8wBmMVOICNdE0C7pbg5NjMZRNu84DamiSvec0sS4%2BFsu5ymmtmGO6ZUvwbDK23lY1XX4saKoEFdQ60zEseM3UdAu%2B&X-Amz-Signature=ed7a0ab8a6b14eb6d053256c494ef6e161c0ac54bb6089af4f738036015efb4a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5456a1c7-f4f1-4e85-84e7-0615d6492830/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662TOHYB22%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204741Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBFJW57qJYr68xK2aNU7QFayYVhgoiwlPbTOn%2BwpA%2BsfAiB7GPNGblh0U1fwW5gHOO71JloWiBfZtXsuNEeclVqFCiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5bkFmozwYgwGJhY5KtwD%2FtRFHHH3IgnT1zDEXR%2BMpS3AlXESqvnZ61yPYG5eO0Tzxgxb7yEOwl4xefzmJ%2FN0%2Fv8xati%2BUrIIyih3x1QdpKDjS8pJXOPftQwWWjkkVklH4z8GoqTNVqutmd0xrj6Qn9fwPE6yNNaDDfg57FCgmoV%2FrrLtSOw8gjHetRsRcn5hJWGRQ3QRAvFgZjj9C7B5%2BLfKiaXN3FSjHPa3P397O%2B5Vu8xZN8KqkmO5mOKfWCaa6z4iHz7e1h%2Fl2MSvvEQ4JCQG7qRUOeXqm4pCuRCmmC1VtCcZYmZUoj0brtJ8qoWExwEXNyhnPZ2uIQ8xiRNIP0Tl7QtqTpSbdco0ZvmTKqYfzXANM8V0EmNXu8m4ApL6wkVmDK9iQAP9e0va%2BFDRlnrvZDX2Ce%2FZBZaLAIgxcXie1TX19WNpnuovgS%2BOZvjbNMcwdfxaV9Te%2BBKAIpbgQx5%2B4RZaMP9ZQ3KrxeuiyM7jQtFwPqGVgBOqtN8ux15k5JvRmkQeQSokliFxzlHainY%2BsBLMQcLc8WlbLyHfb3tec0H4Wg6aIec%2FtO9RylhuM0qUb8xit%2B2usfz5TMrqG1DylFrASWIGotGkOT5Ix5ho9NHHCG4Q%2B70hIf7XoYGOt7kY3L8%2FW%2FZqvkgwzMai1AY6pgGUhdkwK5QvJexZXym73xl6JIaNXvRjnzZE4GHoZLUcDGHKGB6vUnBxwapA1LGwr2%2Bb%2FoN6c7ivklXg0bdkzT%2BlrXBEGtgtXgDyLcRvTWnCFQKrGpo7agehXATzSn5WBjTOrUu8wBmMVOICNdE0C7pbg5NjMZRNu84DamiSvec0sS4%2BFsu5ymmtmGO6ZUvwbDK23lY1XX4saKoEFdQ60zEseM3UdAu%2B&X-Amz-Signature=93c10805b88778a619362dfd3c1444d2a83dc929e57d57526cc4e83ede04f74f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Copy the new generated Public Key as JWK and paste in Body** **section of exploit server** into the `keys` array of JWK Set as follows:                  

```perl
{
    "keys": [
    <<PASTE PUBLIC key as JWK>>
    ]
}
```

**then **`Store`** in the exploit server:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e482895f-d5af-4140-b83e-255746344cf3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662TOHYB22%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204741Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBFJW57qJYr68xK2aNU7QFayYVhgoiwlPbTOn%2BwpA%2BsfAiB7GPNGblh0U1fwW5gHOO71JloWiBfZtXsuNEeclVqFCiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5bkFmozwYgwGJhY5KtwD%2FtRFHHH3IgnT1zDEXR%2BMpS3AlXESqvnZ61yPYG5eO0Tzxgxb7yEOwl4xefzmJ%2FN0%2Fv8xati%2BUrIIyih3x1QdpKDjS8pJXOPftQwWWjkkVklH4z8GoqTNVqutmd0xrj6Qn9fwPE6yNNaDDfg57FCgmoV%2FrrLtSOw8gjHetRsRcn5hJWGRQ3QRAvFgZjj9C7B5%2BLfKiaXN3FSjHPa3P397O%2B5Vu8xZN8KqkmO5mOKfWCaa6z4iHz7e1h%2Fl2MSvvEQ4JCQG7qRUOeXqm4pCuRCmmC1VtCcZYmZUoj0brtJ8qoWExwEXNyhnPZ2uIQ8xiRNIP0Tl7QtqTpSbdco0ZvmTKqYfzXANM8V0EmNXu8m4ApL6wkVmDK9iQAP9e0va%2BFDRlnrvZDX2Ce%2FZBZaLAIgxcXie1TX19WNpnuovgS%2BOZvjbNMcwdfxaV9Te%2BBKAIpbgQx5%2B4RZaMP9ZQ3KrxeuiyM7jQtFwPqGVgBOqtN8ux15k5JvRmkQeQSokliFxzlHainY%2BsBLMQcLc8WlbLyHfb3tec0H4Wg6aIec%2FtO9RylhuM0qUb8xit%2B2usfz5TMrqG1DylFrASWIGotGkOT5Ix5ho9NHHCG4Q%2B70hIf7XoYGOt7kY3L8%2FW%2FZqvkgwzMai1AY6pgGUhdkwK5QvJexZXym73xl6JIaNXvRjnzZE4GHoZLUcDGHKGB6vUnBxwapA1LGwr2%2Bb%2FoN6c7ivklXg0bdkzT%2BlrXBEGtgtXgDyLcRvTWnCFQKrGpo7agehXATzSn5WBjTOrUu8wBmMVOICNdE0C7pbg5NjMZRNu84DamiSvec0sS4%2BFsu5ymmtmGO6ZUvwbDK23lY1XX4saKoEFdQ60zEseM3UdAu%2B&X-Amz-Signature=3710f854dca7ad1838d05dc1e0dc5efe18bb609ce741a3fe6c20930e88aa65f5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Modify and sign the JWT

Send the post-login `GET /my-account?id=wiener` request to Burp Repeater, then remove id parameter    

- In the header of the JWT, replace the current value of the `kid` parameter with the `kid` of the JWK that you uploaded to the exploit server.
Add a new `jku` parameter to the header of the JWT. Set its value to the URL of your JWK Set on the exploit server.

> 💡 Remember all parameter end with comma , except last one

- In the payload, change the value of the `sub` claim to `administrator`.
- At the bottom of the tab, click **Sign**, then select the RSA key that you generated. Make sure that the **Don't modify header** option is selected, then click **OK**.
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fc076ff1-8f65-4dd0-9bc7-4b2f0b767ac3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662TOHYB22%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204741Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBFJW57qJYr68xK2aNU7QFayYVhgoiwlPbTOn%2BwpA%2BsfAiB7GPNGblh0U1fwW5gHOO71JloWiBfZtXsuNEeclVqFCiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5bkFmozwYgwGJhY5KtwD%2FtRFHHH3IgnT1zDEXR%2BMpS3AlXESqvnZ61yPYG5eO0Tzxgxb7yEOwl4xefzmJ%2FN0%2Fv8xati%2BUrIIyih3x1QdpKDjS8pJXOPftQwWWjkkVklH4z8GoqTNVqutmd0xrj6Qn9fwPE6yNNaDDfg57FCgmoV%2FrrLtSOw8gjHetRsRcn5hJWGRQ3QRAvFgZjj9C7B5%2BLfKiaXN3FSjHPa3P397O%2B5Vu8xZN8KqkmO5mOKfWCaa6z4iHz7e1h%2Fl2MSvvEQ4JCQG7qRUOeXqm4pCuRCmmC1VtCcZYmZUoj0brtJ8qoWExwEXNyhnPZ2uIQ8xiRNIP0Tl7QtqTpSbdco0ZvmTKqYfzXANM8V0EmNXu8m4ApL6wkVmDK9iQAP9e0va%2BFDRlnrvZDX2Ce%2FZBZaLAIgxcXie1TX19WNpnuovgS%2BOZvjbNMcwdfxaV9Te%2BBKAIpbgQx5%2B4RZaMP9ZQ3KrxeuiyM7jQtFwPqGVgBOqtN8ux15k5JvRmkQeQSokliFxzlHainY%2BsBLMQcLc8WlbLyHfb3tec0H4Wg6aIec%2FtO9RylhuM0qUb8xit%2B2usfz5TMrqG1DylFrASWIGotGkOT5Ix5ho9NHHCG4Q%2B70hIf7XoYGOt7kY3L8%2FW%2FZqvkgwzMai1AY6pgGUhdkwK5QvJexZXym73xl6JIaNXvRjnzZE4GHoZLUcDGHKGB6vUnBxwapA1LGwr2%2Bb%2FoN6c7ivklXg0bdkzT%2BlrXBEGtgtXgDyLcRvTWnCFQKrGpo7agehXATzSn5WBjTOrUu8wBmMVOICNdE0C7pbg5NjMZRNu84DamiSvec0sS4%2BFsu5ymmtmGO6ZUvwbDK23lY1XX4saKoEFdQ60zEseM3UdAu%2B&X-Amz-Signature=3d324ec6dd2056b4caf78f8dd1eb6043440170b3eb27a2800b2341185971489f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Copy the JWT and update session cookie in the browser**, then refresh the page:**

go to the admin panel and delete user `carlos`

