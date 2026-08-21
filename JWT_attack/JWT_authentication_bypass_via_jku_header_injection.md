# JWT authentication bypass via jku header injection

## Goal - 

Forge a JWT that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

## Analysis/Exploitation -

**Login as user **`wiener`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1aaa703c-3df7-434a-b6f9-396a8e9cf1be/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XW62C6QK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCBfs76KQTXMi2Fe4AQ5Da2Orp5KVmVLDT5ISGyxQd22AIgKYma91teREj4NrSA3dUxOpQvIAyEU5b%2FEjrgReR2FRgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHgGWKVupf41pDeGdyrcA9btxp%2F7FOAQJEe0kup86Qc%2B29d2r%2F5IQA%2FQRXMkP1j5qn8PRCM5NhIphDSi65cBBmr3aMfbD3uXLcPT695ZdCUEHqEfXw14e5x7H%2BdGUMcv12XZqG03wmIT7Tj0HjerorjEzjqN%2FC9%2Biw40liN%2Beu1gD%2BvR46Qk8nTzFpujsP8DSJ%2Fr%2BbBCb3ay3H3yV81OGk4C2rE0dpNDUem4cTQrGFUyp9nLYduWb0%2BpcxgvmrD8frVXORcvzw98MoYXB68lcoaUeple%2FduochMtqcYeqGGty2f7j7b4hkgeKtfKGnFh4tD43gP5N4HjJKHiPCZMxOl8SNIDpBTjSCvoJc3USgN50bRErvuF%2BimpY1HpISoIEbZcSW4eqfoILECpEUwzCihLl6yIQZtKwmrNLfhxRTt3o5N%2FTQ%2BBIW31XQ9OaR2XdxpQotcrduOiUGwDYYo1Vs2iDE1%2FNaszidTr9w6buzc7Orv6TL3o6Cu%2BoP9nSxKLiXjHcPwlS4guMOgSJ3%2BSSg7F0%2FBPR52R7jsVFaKllPUxSGVq%2FWfC%2FUZfAEsdW6u24z7HXlbMpzc%2BQvNgAcD6AP8L2dVTRByjuWG2EV3E0TMZRCI%2BKmnPQ9bWjXPBxL5IMAi0y5gdusVypgi5MOeDo9QGOqUBl%2Ff1oxTrv4%2ButtWKjaIBjhceD7B8uxI4%2BFXIRnzSTTSk59ZInTtAg%2BWYCweAQLeRVG89N9atxLvemqzEa%2BpNqNVaXzTlsTjkdVAfkOHXcOpGkbipcuhui8AKs%2BGiner4zP%2BbN8f%2FoB8Cg2PM8ZcOL4IWLc9q5ODJWrUlt7ZXtQuHGJt9oYtbrKHdP6bY8LDXd6lKBS5LdsB%2BM7oCDj%2Fb3LyAHwyf&X-Amz-Signature=4d0f99ebeb38df9012f58643df578d45faeca220398a6a2fb1eec477802a3eba&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the header’s `alg`, it tells that **it’s using RS256(RSA + SHA-256) algorithm.**

**In the lab’s background, it said:**

> The server supports the jku(JWK Set URL) parameter in the JWT header. However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key.

### Upload a malicious JWK Set of **new generated RSA key pair:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9b6e3d3c-9638-4f47-9d99-213faa330981/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XW62C6QK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCBfs76KQTXMi2Fe4AQ5Da2Orp5KVmVLDT5ISGyxQd22AIgKYma91teREj4NrSA3dUxOpQvIAyEU5b%2FEjrgReR2FRgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHgGWKVupf41pDeGdyrcA9btxp%2F7FOAQJEe0kup86Qc%2B29d2r%2F5IQA%2FQRXMkP1j5qn8PRCM5NhIphDSi65cBBmr3aMfbD3uXLcPT695ZdCUEHqEfXw14e5x7H%2BdGUMcv12XZqG03wmIT7Tj0HjerorjEzjqN%2FC9%2Biw40liN%2Beu1gD%2BvR46Qk8nTzFpujsP8DSJ%2Fr%2BbBCb3ay3H3yV81OGk4C2rE0dpNDUem4cTQrGFUyp9nLYduWb0%2BpcxgvmrD8frVXORcvzw98MoYXB68lcoaUeple%2FduochMtqcYeqGGty2f7j7b4hkgeKtfKGnFh4tD43gP5N4HjJKHiPCZMxOl8SNIDpBTjSCvoJc3USgN50bRErvuF%2BimpY1HpISoIEbZcSW4eqfoILECpEUwzCihLl6yIQZtKwmrNLfhxRTt3o5N%2FTQ%2BBIW31XQ9OaR2XdxpQotcrduOiUGwDYYo1Vs2iDE1%2FNaszidTr9w6buzc7Orv6TL3o6Cu%2BoP9nSxKLiXjHcPwlS4guMOgSJ3%2BSSg7F0%2FBPR52R7jsVFaKllPUxSGVq%2FWfC%2FUZfAEsdW6u24z7HXlbMpzc%2BQvNgAcD6AP8L2dVTRByjuWG2EV3E0TMZRCI%2BKmnPQ9bWjXPBxL5IMAi0y5gdusVypgi5MOeDo9QGOqUBl%2Ff1oxTrv4%2ButtWKjaIBjhceD7B8uxI4%2BFXIRnzSTTSk59ZInTtAg%2BWYCweAQLeRVG89N9atxLvemqzEa%2BpNqNVaXzTlsTjkdVAfkOHXcOpGkbipcuhui8AKs%2BGiner4zP%2BbN8f%2FoB8Cg2PM8ZcOL4IWLc9q5ODJWrUlt7ZXtQuHGJt9oYtbrKHdP6bY8LDXd6lKBS5LdsB%2BM7oCDj%2Fb3LyAHwyf&X-Amz-Signature=e3044d94c9f703de395e4e179ce6cc3f564a509ad98d3f484c63e68180c32294&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5456a1c7-f4f1-4e85-84e7-0615d6492830/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XW62C6QK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCBfs76KQTXMi2Fe4AQ5Da2Orp5KVmVLDT5ISGyxQd22AIgKYma91teREj4NrSA3dUxOpQvIAyEU5b%2FEjrgReR2FRgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHgGWKVupf41pDeGdyrcA9btxp%2F7FOAQJEe0kup86Qc%2B29d2r%2F5IQA%2FQRXMkP1j5qn8PRCM5NhIphDSi65cBBmr3aMfbD3uXLcPT695ZdCUEHqEfXw14e5x7H%2BdGUMcv12XZqG03wmIT7Tj0HjerorjEzjqN%2FC9%2Biw40liN%2Beu1gD%2BvR46Qk8nTzFpujsP8DSJ%2Fr%2BbBCb3ay3H3yV81OGk4C2rE0dpNDUem4cTQrGFUyp9nLYduWb0%2BpcxgvmrD8frVXORcvzw98MoYXB68lcoaUeple%2FduochMtqcYeqGGty2f7j7b4hkgeKtfKGnFh4tD43gP5N4HjJKHiPCZMxOl8SNIDpBTjSCvoJc3USgN50bRErvuF%2BimpY1HpISoIEbZcSW4eqfoILECpEUwzCihLl6yIQZtKwmrNLfhxRTt3o5N%2FTQ%2BBIW31XQ9OaR2XdxpQotcrduOiUGwDYYo1Vs2iDE1%2FNaszidTr9w6buzc7Orv6TL3o6Cu%2BoP9nSxKLiXjHcPwlS4guMOgSJ3%2BSSg7F0%2FBPR52R7jsVFaKllPUxSGVq%2FWfC%2FUZfAEsdW6u24z7HXlbMpzc%2BQvNgAcD6AP8L2dVTRByjuWG2EV3E0TMZRCI%2BKmnPQ9bWjXPBxL5IMAi0y5gdusVypgi5MOeDo9QGOqUBl%2Ff1oxTrv4%2ButtWKjaIBjhceD7B8uxI4%2BFXIRnzSTTSk59ZInTtAg%2BWYCweAQLeRVG89N9atxLvemqzEa%2BpNqNVaXzTlsTjkdVAfkOHXcOpGkbipcuhui8AKs%2BGiner4zP%2BbN8f%2FoB8Cg2PM8ZcOL4IWLc9q5ODJWrUlt7ZXtQuHGJt9oYtbrKHdP6bY8LDXd6lKBS5LdsB%2BM7oCDj%2Fb3LyAHwyf&X-Amz-Signature=12496adcc32759fac4cc6a5830365cb3abef89901e13d0f8ff3c931e0b542e49&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Copy the new generated Public Key as JWK and paste in Body** **section of exploit server** into the `keys` array of JWK Set as follows:                  

```perl
{
    "keys": [
    <<PASTE PUBLIC key as JWK>>
    ]
}
```

**then **`Store`** in the exploit server:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e482895f-d5af-4140-b83e-255746344cf3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XW62C6QK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCBfs76KQTXMi2Fe4AQ5Da2Orp5KVmVLDT5ISGyxQd22AIgKYma91teREj4NrSA3dUxOpQvIAyEU5b%2FEjrgReR2FRgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHgGWKVupf41pDeGdyrcA9btxp%2F7FOAQJEe0kup86Qc%2B29d2r%2F5IQA%2FQRXMkP1j5qn8PRCM5NhIphDSi65cBBmr3aMfbD3uXLcPT695ZdCUEHqEfXw14e5x7H%2BdGUMcv12XZqG03wmIT7Tj0HjerorjEzjqN%2FC9%2Biw40liN%2Beu1gD%2BvR46Qk8nTzFpujsP8DSJ%2Fr%2BbBCb3ay3H3yV81OGk4C2rE0dpNDUem4cTQrGFUyp9nLYduWb0%2BpcxgvmrD8frVXORcvzw98MoYXB68lcoaUeple%2FduochMtqcYeqGGty2f7j7b4hkgeKtfKGnFh4tD43gP5N4HjJKHiPCZMxOl8SNIDpBTjSCvoJc3USgN50bRErvuF%2BimpY1HpISoIEbZcSW4eqfoILECpEUwzCihLl6yIQZtKwmrNLfhxRTt3o5N%2FTQ%2BBIW31XQ9OaR2XdxpQotcrduOiUGwDYYo1Vs2iDE1%2FNaszidTr9w6buzc7Orv6TL3o6Cu%2BoP9nSxKLiXjHcPwlS4guMOgSJ3%2BSSg7F0%2FBPR52R7jsVFaKllPUxSGVq%2FWfC%2FUZfAEsdW6u24z7HXlbMpzc%2BQvNgAcD6AP8L2dVTRByjuWG2EV3E0TMZRCI%2BKmnPQ9bWjXPBxL5IMAi0y5gdusVypgi5MOeDo9QGOqUBl%2Ff1oxTrv4%2ButtWKjaIBjhceD7B8uxI4%2BFXIRnzSTTSk59ZInTtAg%2BWYCweAQLeRVG89N9atxLvemqzEa%2BpNqNVaXzTlsTjkdVAfkOHXcOpGkbipcuhui8AKs%2BGiner4zP%2BbN8f%2FoB8Cg2PM8ZcOL4IWLc9q5ODJWrUlt7ZXtQuHGJt9oYtbrKHdP6bY8LDXd6lKBS5LdsB%2BM7oCDj%2Fb3LyAHwyf&X-Amz-Signature=094216d1592d1c9f2040c47f67a9e2ed67c606fed87aac039d24cba114fb7f83&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Modify and sign the JWT

Send the post-login `GET /my-account?id=wiener` request to Burp Repeater, then remove id parameter    

- In the header of the JWT, replace the current value of the `kid` parameter with the `kid` of the JWK that you uploaded to the exploit server.
Add a new `jku` parameter to the header of the JWT. Set its value to the URL of your JWK Set on the exploit server.

> 💡 Remember all parameter end with comma , except last one

- In the payload, change the value of the `sub` claim to `administrator`.
- At the bottom of the tab, click **Sign**, then select the RSA key that you generated. Make sure that the **Don't modify header** option is selected, then click **OK**.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fc076ff1-8f65-4dd0-9bc7-4b2f0b767ac3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XW62C6QK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215632Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCBfs76KQTXMi2Fe4AQ5Da2Orp5KVmVLDT5ISGyxQd22AIgKYma91teREj4NrSA3dUxOpQvIAyEU5b%2FEjrgReR2FRgqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHgGWKVupf41pDeGdyrcA9btxp%2F7FOAQJEe0kup86Qc%2B29d2r%2F5IQA%2FQRXMkP1j5qn8PRCM5NhIphDSi65cBBmr3aMfbD3uXLcPT695ZdCUEHqEfXw14e5x7H%2BdGUMcv12XZqG03wmIT7Tj0HjerorjEzjqN%2FC9%2Biw40liN%2Beu1gD%2BvR46Qk8nTzFpujsP8DSJ%2Fr%2BbBCb3ay3H3yV81OGk4C2rE0dpNDUem4cTQrGFUyp9nLYduWb0%2BpcxgvmrD8frVXORcvzw98MoYXB68lcoaUeple%2FduochMtqcYeqGGty2f7j7b4hkgeKtfKGnFh4tD43gP5N4HjJKHiPCZMxOl8SNIDpBTjSCvoJc3USgN50bRErvuF%2BimpY1HpISoIEbZcSW4eqfoILECpEUwzCihLl6yIQZtKwmrNLfhxRTt3o5N%2FTQ%2BBIW31XQ9OaR2XdxpQotcrduOiUGwDYYo1Vs2iDE1%2FNaszidTr9w6buzc7Orv6TL3o6Cu%2BoP9nSxKLiXjHcPwlS4guMOgSJ3%2BSSg7F0%2FBPR52R7jsVFaKllPUxSGVq%2FWfC%2FUZfAEsdW6u24z7HXlbMpzc%2BQvNgAcD6AP8L2dVTRByjuWG2EV3E0TMZRCI%2BKmnPQ9bWjXPBxL5IMAi0y5gdusVypgi5MOeDo9QGOqUBl%2Ff1oxTrv4%2ButtWKjaIBjhceD7B8uxI4%2BFXIRnzSTTSk59ZInTtAg%2BWYCweAQLeRVG89N9atxLvemqzEa%2BpNqNVaXzTlsTjkdVAfkOHXcOpGkbipcuhui8AKs%2BGiner4zP%2BbN8f%2FoB8Cg2PM8ZcOL4IWLc9q5ODJWrUlt7ZXtQuHGJt9oYtbrKHdP6bY8LDXd6lKBS5LdsB%2BM7oCDj%2Fb3LyAHwyf&X-Amz-Signature=cc054af05c96eab7981bca8845f3a5cb25c4c6276b59c8e270ef599c91edd3cb&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Copy the JWT and update session cookie in the browser**, then refresh the page:**

go to the admin panel and delete user `carlos`
