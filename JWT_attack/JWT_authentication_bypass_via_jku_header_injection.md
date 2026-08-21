# JWT authentication bypass via jku header injection

## Goal - 

Forge a JWT that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

## Analysis/Exploitation -

**Login as user **`wiener`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1aaa703c-3df7-434a-b6f9-396a8e9cf1be/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHOITL6L%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210507Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDtdOUqpQSjX%2FQCygjWSj9Qj%2BVgGxzxXKKMZkNm%2B5LSuAiEA3ImZnYJ3L%2FqQlFzhBH1r1rGtQNXzegBv0ExgoL1bFskqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEtTtsGrCqBVvuBIdSrcA%2ByEHQ07SdXIFp9cX5W7cm5rBWlf%2B%2BC8ENtKnJpGbXk2saAXuEb95MsX%2FIjk5TKt%2BNxH%2BEUzRHkH9p9Psx0r6CZx5gct6BIa6TspP8dOpgT229JBu8NnvI5qGfZ1trD1818PvjbeWlwvsHNMEZmhGoHx5cn12l3Ppdfodgm%2F%2BlhVZEjGeEXFm4w7523YKdeH3ZCUuh5IefyFzPfpa9Xg7d5FHoNCTMo7xzNrGVQRZ9RpuqJXPDQFU%2F0X9wRkJRdvVkpEeCwxuLFvwoYqGUsbCNb%2FLv5YvoLSCb6pDK59nbfFwph0GV%2FzaE7hdP6VfeGJLLq4tAVZ8gd%2B4iDKL4v9ep0c70nCYz3pRKdOtTuufB4QfUcDzngw%2FIX5omh0ADEYi32rWAzaaFszoh%2BMMvXjRBjx1zqzMq7FiaBAmA%2FMCaxlpPBxYtRp5ItRfnD5UvIwf%2FqUVRUn3mzIx5lvYGjLw472E9T5j4GhmNcZhba3X%2BoBwQ844wUqmXJV34hBC4K3Jg2x%2FJWBnXCIXxTEwXhJDnBLIFkfiNptLbVb3pSyNfcOBnWh5NUskuDtQCuwrcvJy8uaULDCqXDwM3%2FxI3tKFmn2ihzaLHpYHnBxoIAIIdXBHgbnu%2BtpjlaolPPSMJrGotQGOqUBb0c%2F6UBA%2B%2FAKiqhXJvn%2F6GnrkBBc%2BD6mij1%2FovrMB%2FrSMW1KMaU%2F9hTUlIBIbQjFBXAi7H2L1SWs979h3XSlWtHIXT7ef5ofLCKScrryQneMlXQzKx1qnt3dUkq5vmvG%2B050w%2BwagARU2ncwRH22wBGzW3rHKMrgNgPkd%2Forv%2BAhDHm6ZMPN4R1o%2BaYoDZdhNmBT0HAfqH618P02YaSUFETaTwtG&X-Amz-Signature=16a22fecefed029b4914fe07bfcffddcde912c8d2b9b05a6cf1fb63dd57088f9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the header’s `alg`, it tells that **it’s using RS256(RSA + SHA-256) algorithm.**

**In the lab’s background, it said:**

> The server supports the jku(JWK Set URL) parameter in the JWT header. However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key.

### Upload a malicious JWK Set of **new generated RSA key pair:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9b6e3d3c-9638-4f47-9d99-213faa330981/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHOITL6L%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210507Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDtdOUqpQSjX%2FQCygjWSj9Qj%2BVgGxzxXKKMZkNm%2B5LSuAiEA3ImZnYJ3L%2FqQlFzhBH1r1rGtQNXzegBv0ExgoL1bFskqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEtTtsGrCqBVvuBIdSrcA%2ByEHQ07SdXIFp9cX5W7cm5rBWlf%2B%2BC8ENtKnJpGbXk2saAXuEb95MsX%2FIjk5TKt%2BNxH%2BEUzRHkH9p9Psx0r6CZx5gct6BIa6TspP8dOpgT229JBu8NnvI5qGfZ1trD1818PvjbeWlwvsHNMEZmhGoHx5cn12l3Ppdfodgm%2F%2BlhVZEjGeEXFm4w7523YKdeH3ZCUuh5IefyFzPfpa9Xg7d5FHoNCTMo7xzNrGVQRZ9RpuqJXPDQFU%2F0X9wRkJRdvVkpEeCwxuLFvwoYqGUsbCNb%2FLv5YvoLSCb6pDK59nbfFwph0GV%2FzaE7hdP6VfeGJLLq4tAVZ8gd%2B4iDKL4v9ep0c70nCYz3pRKdOtTuufB4QfUcDzngw%2FIX5omh0ADEYi32rWAzaaFszoh%2BMMvXjRBjx1zqzMq7FiaBAmA%2FMCaxlpPBxYtRp5ItRfnD5UvIwf%2FqUVRUn3mzIx5lvYGjLw472E9T5j4GhmNcZhba3X%2BoBwQ844wUqmXJV34hBC4K3Jg2x%2FJWBnXCIXxTEwXhJDnBLIFkfiNptLbVb3pSyNfcOBnWh5NUskuDtQCuwrcvJy8uaULDCqXDwM3%2FxI3tKFmn2ihzaLHpYHnBxoIAIIdXBHgbnu%2BtpjlaolPPSMJrGotQGOqUBb0c%2F6UBA%2B%2FAKiqhXJvn%2F6GnrkBBc%2BD6mij1%2FovrMB%2FrSMW1KMaU%2F9hTUlIBIbQjFBXAi7H2L1SWs979h3XSlWtHIXT7ef5ofLCKScrryQneMlXQzKx1qnt3dUkq5vmvG%2B050w%2BwagARU2ncwRH22wBGzW3rHKMrgNgPkd%2Forv%2BAhDHm6ZMPN4R1o%2BaYoDZdhNmBT0HAfqH618P02YaSUFETaTwtG&X-Amz-Signature=854d687ff86a5e68a6acdfe8e41a2a25d7841c3d72f0d98c70fba91b5760674c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5456a1c7-f4f1-4e85-84e7-0615d6492830/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHOITL6L%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210507Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDtdOUqpQSjX%2FQCygjWSj9Qj%2BVgGxzxXKKMZkNm%2B5LSuAiEA3ImZnYJ3L%2FqQlFzhBH1r1rGtQNXzegBv0ExgoL1bFskqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEtTtsGrCqBVvuBIdSrcA%2ByEHQ07SdXIFp9cX5W7cm5rBWlf%2B%2BC8ENtKnJpGbXk2saAXuEb95MsX%2FIjk5TKt%2BNxH%2BEUzRHkH9p9Psx0r6CZx5gct6BIa6TspP8dOpgT229JBu8NnvI5qGfZ1trD1818PvjbeWlwvsHNMEZmhGoHx5cn12l3Ppdfodgm%2F%2BlhVZEjGeEXFm4w7523YKdeH3ZCUuh5IefyFzPfpa9Xg7d5FHoNCTMo7xzNrGVQRZ9RpuqJXPDQFU%2F0X9wRkJRdvVkpEeCwxuLFvwoYqGUsbCNb%2FLv5YvoLSCb6pDK59nbfFwph0GV%2FzaE7hdP6VfeGJLLq4tAVZ8gd%2B4iDKL4v9ep0c70nCYz3pRKdOtTuufB4QfUcDzngw%2FIX5omh0ADEYi32rWAzaaFszoh%2BMMvXjRBjx1zqzMq7FiaBAmA%2FMCaxlpPBxYtRp5ItRfnD5UvIwf%2FqUVRUn3mzIx5lvYGjLw472E9T5j4GhmNcZhba3X%2BoBwQ844wUqmXJV34hBC4K3Jg2x%2FJWBnXCIXxTEwXhJDnBLIFkfiNptLbVb3pSyNfcOBnWh5NUskuDtQCuwrcvJy8uaULDCqXDwM3%2FxI3tKFmn2ihzaLHpYHnBxoIAIIdXBHgbnu%2BtpjlaolPPSMJrGotQGOqUBb0c%2F6UBA%2B%2FAKiqhXJvn%2F6GnrkBBc%2BD6mij1%2FovrMB%2FrSMW1KMaU%2F9hTUlIBIbQjFBXAi7H2L1SWs979h3XSlWtHIXT7ef5ofLCKScrryQneMlXQzKx1qnt3dUkq5vmvG%2B050w%2BwagARU2ncwRH22wBGzW3rHKMrgNgPkd%2Forv%2BAhDHm6ZMPN4R1o%2BaYoDZdhNmBT0HAfqH618P02YaSUFETaTwtG&X-Amz-Signature=fb47a6826b83c5fc643c66108e790b5412e3327395a0ef0a833d29aa02f60843&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Copy the new generated Public Key as JWK and paste in Body** **section of exploit server** into the `keys` array of JWK Set as follows:                  

```perl
{
    "keys": [
    <<PASTE PUBLIC key as JWK>>
    ]
}
```

**then **`Store`** in the exploit server:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e482895f-d5af-4140-b83e-255746344cf3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHOITL6L%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210507Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDtdOUqpQSjX%2FQCygjWSj9Qj%2BVgGxzxXKKMZkNm%2B5LSuAiEA3ImZnYJ3L%2FqQlFzhBH1r1rGtQNXzegBv0ExgoL1bFskqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEtTtsGrCqBVvuBIdSrcA%2ByEHQ07SdXIFp9cX5W7cm5rBWlf%2B%2BC8ENtKnJpGbXk2saAXuEb95MsX%2FIjk5TKt%2BNxH%2BEUzRHkH9p9Psx0r6CZx5gct6BIa6TspP8dOpgT229JBu8NnvI5qGfZ1trD1818PvjbeWlwvsHNMEZmhGoHx5cn12l3Ppdfodgm%2F%2BlhVZEjGeEXFm4w7523YKdeH3ZCUuh5IefyFzPfpa9Xg7d5FHoNCTMo7xzNrGVQRZ9RpuqJXPDQFU%2F0X9wRkJRdvVkpEeCwxuLFvwoYqGUsbCNb%2FLv5YvoLSCb6pDK59nbfFwph0GV%2FzaE7hdP6VfeGJLLq4tAVZ8gd%2B4iDKL4v9ep0c70nCYz3pRKdOtTuufB4QfUcDzngw%2FIX5omh0ADEYi32rWAzaaFszoh%2BMMvXjRBjx1zqzMq7FiaBAmA%2FMCaxlpPBxYtRp5ItRfnD5UvIwf%2FqUVRUn3mzIx5lvYGjLw472E9T5j4GhmNcZhba3X%2BoBwQ844wUqmXJV34hBC4K3Jg2x%2FJWBnXCIXxTEwXhJDnBLIFkfiNptLbVb3pSyNfcOBnWh5NUskuDtQCuwrcvJy8uaULDCqXDwM3%2FxI3tKFmn2ihzaLHpYHnBxoIAIIdXBHgbnu%2BtpjlaolPPSMJrGotQGOqUBb0c%2F6UBA%2B%2FAKiqhXJvn%2F6GnrkBBc%2BD6mij1%2FovrMB%2FrSMW1KMaU%2F9hTUlIBIbQjFBXAi7H2L1SWs979h3XSlWtHIXT7ef5ofLCKScrryQneMlXQzKx1qnt3dUkq5vmvG%2B050w%2BwagARU2ncwRH22wBGzW3rHKMrgNgPkd%2Forv%2BAhDHm6ZMPN4R1o%2BaYoDZdhNmBT0HAfqH618P02YaSUFETaTwtG&X-Amz-Signature=6c6d0d67a890d01dbeb0f461db67fe46d7ef7abb246e4bb4c556982d6852f50c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Modify and sign the JWT

Send the post-login `GET /my-account?id=wiener` request to Burp Repeater, then remove id parameter    

- In the header of the JWT, replace the current value of the `kid` parameter with the `kid` of the JWK that you uploaded to the exploit server.
Add a new `jku` parameter to the header of the JWT. Set its value to the URL of your JWK Set on the exploit server.

> 💡 Remember all parameter end with comma , except last one

- In the payload, change the value of the `sub` claim to `administrator`.
- At the bottom of the tab, click **Sign**, then select the RSA key that you generated. Make sure that the **Don't modify header** option is selected, then click **OK**.
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fc076ff1-8f65-4dd0-9bc7-4b2f0b767ac3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHOITL6L%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210507Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIDtdOUqpQSjX%2FQCygjWSj9Qj%2BVgGxzxXKKMZkNm%2B5LSuAiEA3ImZnYJ3L%2FqQlFzhBH1r1rGtQNXzegBv0ExgoL1bFskqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDEtTtsGrCqBVvuBIdSrcA%2ByEHQ07SdXIFp9cX5W7cm5rBWlf%2B%2BC8ENtKnJpGbXk2saAXuEb95MsX%2FIjk5TKt%2BNxH%2BEUzRHkH9p9Psx0r6CZx5gct6BIa6TspP8dOpgT229JBu8NnvI5qGfZ1trD1818PvjbeWlwvsHNMEZmhGoHx5cn12l3Ppdfodgm%2F%2BlhVZEjGeEXFm4w7523YKdeH3ZCUuh5IefyFzPfpa9Xg7d5FHoNCTMo7xzNrGVQRZ9RpuqJXPDQFU%2F0X9wRkJRdvVkpEeCwxuLFvwoYqGUsbCNb%2FLv5YvoLSCb6pDK59nbfFwph0GV%2FzaE7hdP6VfeGJLLq4tAVZ8gd%2B4iDKL4v9ep0c70nCYz3pRKdOtTuufB4QfUcDzngw%2FIX5omh0ADEYi32rWAzaaFszoh%2BMMvXjRBjx1zqzMq7FiaBAmA%2FMCaxlpPBxYtRp5ItRfnD5UvIwf%2FqUVRUn3mzIx5lvYGjLw472E9T5j4GhmNcZhba3X%2BoBwQ844wUqmXJV34hBC4K3Jg2x%2FJWBnXCIXxTEwXhJDnBLIFkfiNptLbVb3pSyNfcOBnWh5NUskuDtQCuwrcvJy8uaULDCqXDwM3%2FxI3tKFmn2ihzaLHpYHnBxoIAIIdXBHgbnu%2BtpjlaolPPSMJrGotQGOqUBb0c%2F6UBA%2B%2FAKiqhXJvn%2F6GnrkBBc%2BD6mij1%2FovrMB%2FrSMW1KMaU%2F9hTUlIBIbQjFBXAi7H2L1SWs979h3XSlWtHIXT7ef5ofLCKScrryQneMlXQzKx1qnt3dUkq5vmvG%2B050w%2BwagARU2ncwRH22wBGzW3rHKMrgNgPkd%2Forv%2BAhDHm6ZMPN4R1o%2BaYoDZdhNmBT0HAfqH618P02YaSUFETaTwtG&X-Amz-Signature=07e41192eb750724224cc6c532932a9d3d968c60b15ce527314425ad69f9fef5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Copy the JWT and update session cookie in the browser**, then refresh the page:**

go to the admin panel and delete user `carlos`

