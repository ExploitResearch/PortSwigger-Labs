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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f419ccfa-6c51-4811-9269-500414a57519/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WDI35Z55%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204716Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDhYj6kPfMNBzVyclSDsq%2FDosdXb4wTytDrHmaEGf%2Fr1wIgUIyzxR7VnuwLm63%2F2nxHqB7pF1vzgCapUw2wHnr90%2F8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHQk1GFurcoGMDNuYSrcA7TbIVioNnJL%2F0uvB0n%2BRqMnLTIJPh82Zek%2BKt7jNqhB%2FmB5ZtNxXqbYquMvrQp2G0J6wCgLXjcezW6MPY%2BA0hItpjoAvhT5PjSElsE3otQt%2BIaDDwIpbNFO9zXS5H5akntLdS1ZE0mV8h7ubqQ3j%2Btqp%2BVftfkFKkYje9iW14IvZfaGCOoFp2HwBjmzvbReEW6Gz9ZTWOriHgaUl%2B4GFsjxzSq48B%2FCbYfiX%2FHUa5TGgzvmgann8AYbxZdSMLg3H4VdE07I%2FHWh40GBa4ZQxbmkLhSsxHBaXwa43k9SODL%2BTutU1dR0HEPfyRHozCnOqdLEqjJZKePKJLMH8E1bzd%2BpIIVzZv61WXdcyziUibSfZU8KE0i9HJ9dvIQxTLj6WTNwadJwmLnM3kLSoybWsU%2ByRZBK0KRkaCVpqt967tpI%2Fj2oOTKahzgVF1yGn5%2B6asBgDET1koI1e%2F0Zij8MkP6bRXfW0KOXoEQf8Wb73Y5W6cLiDctoDinvmEjTProDfilj8riuzDq6W1Bw3oBF2bq6PVE%2FheQKvm5dRqYxTShNba9dpRnc9YxyZvnbfdtwK4ru5UhF1vD9mpobRsKyue66e8pUnJZxCifnLSZKF4t%2Bq1jCxnU%2F1G96dYZHMOXGotQGOqUBymGfPqVoNIclznm69yWY3%2F9cEMMy%2B2taJW%2BSW4g3h%2B4g6hHzCsq4%2FDPJLIC19Ih1gbMVmcBaqr%2F4%2BqrNRnKgjE1QsLU%2B9UbJzBqPKblNft4FxEjKvfw1qVYn%2Bkw6doSTnhEHMRnb8Vb3PKsT862QKzOWgneFk%2Bco%2BvFKiwNcnZ3zn6o7yvrsiGVdx4%2BMWfgIdLWkvxx2dJcrD1M2MLEzm5DH7Xbd&X-Amz-Signature=77a2c37cc0d754c2faf09361115c41a35ce76f14e14ca46c4fd1ee79d0c52b9c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now, instead of triggering a time delay, we can also **redirect the command’s output to a file, and stored it to where we can access.**

In the home page, we can see there are some product images:

Typically you’ll **stored the output to a static file**, like `images`.As we can see, **they are at **`/image`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e029e26c-adab-42eb-8b75-cc03aa5cb267/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WDI35Z55%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204716Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDhYj6kPfMNBzVyclSDsq%2FDosdXb4wTytDrHmaEGf%2Fr1wIgUIyzxR7VnuwLm63%2F2nxHqB7pF1vzgCapUw2wHnr90%2F8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHQk1GFurcoGMDNuYSrcA7TbIVioNnJL%2F0uvB0n%2BRqMnLTIJPh82Zek%2BKt7jNqhB%2FmB5ZtNxXqbYquMvrQp2G0J6wCgLXjcezW6MPY%2BA0hItpjoAvhT5PjSElsE3otQt%2BIaDDwIpbNFO9zXS5H5akntLdS1ZE0mV8h7ubqQ3j%2Btqp%2BVftfkFKkYje9iW14IvZfaGCOoFp2HwBjmzvbReEW6Gz9ZTWOriHgaUl%2B4GFsjxzSq48B%2FCbYfiX%2FHUa5TGgzvmgann8AYbxZdSMLg3H4VdE07I%2FHWh40GBa4ZQxbmkLhSsxHBaXwa43k9SODL%2BTutU1dR0HEPfyRHozCnOqdLEqjJZKePKJLMH8E1bzd%2BpIIVzZv61WXdcyziUibSfZU8KE0i9HJ9dvIQxTLj6WTNwadJwmLnM3kLSoybWsU%2ByRZBK0KRkaCVpqt967tpI%2Fj2oOTKahzgVF1yGn5%2B6asBgDET1koI1e%2F0Zij8MkP6bRXfW0KOXoEQf8Wb73Y5W6cLiDctoDinvmEjTProDfilj8riuzDq6W1Bw3oBF2bq6PVE%2FheQKvm5dRqYxTShNba9dpRnc9YxyZvnbfdtwK4ru5UhF1vD9mpobRsKyue66e8pUnJZxCifnLSZKF4t%2Bq1jCxnU%2F1G96dYZHMOXGotQGOqUBymGfPqVoNIclznm69yWY3%2F9cEMMy%2B2taJW%2BSW4g3h%2B4g6hHzCsq4%2FDPJLIC19Ih1gbMVmcBaqr%2F4%2BqrNRnKgjE1QsLU%2B9UbJzBqPKblNft4FxEjKvfw1qVYn%2Bkw6doSTnhEHMRnb8Vb3PKsT862QKzOWgneFk%2Bco%2BvFKiwNcnZ3zn6o7yvrsiGVdx4%2BMWfgIdLWkvxx2dJcrD1M2MLEzm5DH7Xbd&X-Amz-Signature=a08dbf337c0f586279d66c84d4732a561b82a93d33ce600602f7f7e9a8ca1c33&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

To redirect command’s output to a file, we can put it to `/var/www/image/<filename>`.since it is mentionted in lab description that Writeable folder is at `/var/www/images/`

> **Note: **In Linux, web root is usually located in **/var/www/**.

The command to execute is `whoami > /var/www/images/whoami.txt `to write the file. Inject it into the email argument. And as in the previous lab, commenting out the remainder results in a `200 OK`, while not doing so results in `500 Internal Server Error`. Both ways work though.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/dd85ec37-3d71-4f42-94bf-b434ad755201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WDI35Z55%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204716Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDhYj6kPfMNBzVyclSDsq%2FDosdXb4wTytDrHmaEGf%2Fr1wIgUIyzxR7VnuwLm63%2F2nxHqB7pF1vzgCapUw2wHnr90%2F8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHQk1GFurcoGMDNuYSrcA7TbIVioNnJL%2F0uvB0n%2BRqMnLTIJPh82Zek%2BKt7jNqhB%2FmB5ZtNxXqbYquMvrQp2G0J6wCgLXjcezW6MPY%2BA0hItpjoAvhT5PjSElsE3otQt%2BIaDDwIpbNFO9zXS5H5akntLdS1ZE0mV8h7ubqQ3j%2Btqp%2BVftfkFKkYje9iW14IvZfaGCOoFp2HwBjmzvbReEW6Gz9ZTWOriHgaUl%2B4GFsjxzSq48B%2FCbYfiX%2FHUa5TGgzvmgann8AYbxZdSMLg3H4VdE07I%2FHWh40GBa4ZQxbmkLhSsxHBaXwa43k9SODL%2BTutU1dR0HEPfyRHozCnOqdLEqjJZKePKJLMH8E1bzd%2BpIIVzZv61WXdcyziUibSfZU8KE0i9HJ9dvIQxTLj6WTNwadJwmLnM3kLSoybWsU%2ByRZBK0KRkaCVpqt967tpI%2Fj2oOTKahzgVF1yGn5%2B6asBgDET1koI1e%2F0Zij8MkP6bRXfW0KOXoEQf8Wb73Y5W6cLiDctoDinvmEjTProDfilj8riuzDq6W1Bw3oBF2bq6PVE%2FheQKvm5dRqYxTShNba9dpRnc9YxyZvnbfdtwK4ru5UhF1vD9mpobRsKyue66e8pUnJZxCifnLSZKF4t%2Bq1jCxnU%2F1G96dYZHMOXGotQGOqUBymGfPqVoNIclznm69yWY3%2F9cEMMy%2B2taJW%2BSW4g3h%2B4g6hHzCsq4%2FDPJLIC19Ih1gbMVmcBaqr%2F4%2BqrNRnKgjE1QsLU%2B9UbJzBqPKblNft4FxEjKvfw1qVYn%2Bkw6doSTnhEHMRnb8Vb3PKsT862QKzOWgneFk%2Bco%2BvFKiwNcnZ3zn6o7yvrsiGVdx4%2BMWfgIdLWkvxx2dJcrD1M2MLEzm5DH7Xbd&X-Amz-Signature=1ef087aca41f2f0ac0410f4ad29e4592cb3b68cad9ec1d3dfda9464ccc512c79&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Access the file**

Now the file is in `/var/www/images`, but the path to it within the application is unknown and perhaps not even accessible directly. But I can utilize the way the application includes its images with a GET request to `/image?filename=`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1796e77c-5656-43a4-8c91-3fc0bde988d7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WDI35Z55%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204716Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDhYj6kPfMNBzVyclSDsq%2FDosdXb4wTytDrHmaEGf%2Fr1wIgUIyzxR7VnuwLm63%2F2nxHqB7pF1vzgCapUw2wHnr90%2F8qiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHQk1GFurcoGMDNuYSrcA7TbIVioNnJL%2F0uvB0n%2BRqMnLTIJPh82Zek%2BKt7jNqhB%2FmB5ZtNxXqbYquMvrQp2G0J6wCgLXjcezW6MPY%2BA0hItpjoAvhT5PjSElsE3otQt%2BIaDDwIpbNFO9zXS5H5akntLdS1ZE0mV8h7ubqQ3j%2Btqp%2BVftfkFKkYje9iW14IvZfaGCOoFp2HwBjmzvbReEW6Gz9ZTWOriHgaUl%2B4GFsjxzSq48B%2FCbYfiX%2FHUa5TGgzvmgann8AYbxZdSMLg3H4VdE07I%2FHWh40GBa4ZQxbmkLhSsxHBaXwa43k9SODL%2BTutU1dR0HEPfyRHozCnOqdLEqjJZKePKJLMH8E1bzd%2BpIIVzZv61WXdcyziUibSfZU8KE0i9HJ9dvIQxTLj6WTNwadJwmLnM3kLSoybWsU%2ByRZBK0KRkaCVpqt967tpI%2Fj2oOTKahzgVF1yGn5%2B6asBgDET1koI1e%2F0Zij8MkP6bRXfW0KOXoEQf8Wb73Y5W6cLiDctoDinvmEjTProDfilj8riuzDq6W1Bw3oBF2bq6PVE%2FheQKvm5dRqYxTShNba9dpRnc9YxyZvnbfdtwK4ru5UhF1vD9mpobRsKyue66e8pUnJZxCifnLSZKF4t%2Bq1jCxnU%2F1G96dYZHMOXGotQGOqUBymGfPqVoNIclznm69yWY3%2F9cEMMy%2B2taJW%2BSW4g3h%2B4g6hHzCsq4%2FDPJLIC19Ih1gbMVmcBaqr%2F4%2BqrNRnKgjE1QsLU%2B9UbJzBqPKblNft4FxEjKvfw1qVYn%2Bkw6doSTnhEHMRnb8Vb3PKsT862QKzOWgneFk%2Bco%2BvFKiwNcnZ3zn6o7yvrsiGVdx4%2BMWfgIdLWkvxx2dJcrD1M2MLEzm5DH7Xbd&X-Amz-Signature=40bfc73bb24450266a526c8960530b816655086484fff0c77d8d76c8519a2174&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 **summary
**

  1. Find & Confirm blind command injection
-email field
  1. Check location from where application serves static resources, here images 
  1. Redirect output to file at that static location
  1. Check if file was created by accessing it
