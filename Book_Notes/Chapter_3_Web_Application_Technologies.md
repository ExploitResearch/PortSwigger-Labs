# Chapter 3 Web Application Technologies

# HTTP Hypertext Transfer Protocol

- **Connectionless protocol**
  - **Client sends an HTTP request to a Web server**
  - **Gets an HTTP response**
  - **No session formed, nothing remembered--no "state"**
## HTTP Requests

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/eb91b3ab-c66e-4c39-a64e-80f747aebcef/image2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=c6f0997ed65f8b7074c9ec2777450260a6433457de950c821e75d5183881790d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Verb: GET (also called "method")**
- **URL: /css?family=Roboto:400,700**
  - **Portion after ? is the *****query string***** containing Parameters**
- **Version: HTTP/1.1**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/eb91b3ab-c66e-4c39-a64e-80f747aebcef/image2.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=c6f0997ed65f8b7074c9ec2777450260a6433457de950c821e75d5183881790d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Referer: URL the request originated from**
- **User-Agent: browser being used**
- **Host: Hostname of the server**
  - **Essential when multiple hosts run on the same IP**
  - **Required in HTTP/1.1**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ab52d9f2-c47b-4f0b-8218-fa40af8a11e0/image3.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=40e1054ee41a031e401841f2c5a1a9b0ac34a54fbb2a3e77f799d3c783a86478&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Cookie: additional parameters the server has issued to the client**
## HTTP Response

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e89cf121-b1e9-4ac3-86bc-fee1613533c9/image4.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=9ada2be09e155423117a7fe610291f1d561d696e8ae9619a85453338aa551390&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **First line**
  - **HTTP version**
  - **Status code (200 in this case)**
  - **Textual "reason phrase" describing the response**
    - **Ignored by browser**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6b2eaa2c-29fd-4f94-a178-1ad3fbcc26d1/image5.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=67a45ab73c0177516f12aee6f95ff63758511e992a985f881b0fb107f19c3d3a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Server: banner of server software**
  - **Not always accurate**
- **Set-Cookie used to set cookie values**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/79cb5f82-ca96-44f0-b958-dd3c2e27527d/image6.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=29e553836abf5f983f98ed5ecda6857c76b03488e5a023826cf2d887a611512b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Pragma: tells browser not to store response in its cache**
- **Expires: set to a date in the past to ensure that the content is freshly loaded**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e89cf121-b1e9-4ac3-86bc-fee1613533c9/image4.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=9ada2be09e155423117a7fe610291f1d561d696e8ae9619a85453338aa551390&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Message Body after header contains data of type specified in Content-Type header**
## HTTP Methods: 

1. **GET**
  - **GET retrieves resources**
    - **Can send parameters in the URL query string**
    - **Users can bookmark the whole URL**
    - **Whole URL may appear in server logs and in Referer headers**
    - **Also on the browser's screen**
  - **Don't put sensitive information in the query string**
1. **POST**
  - **POST performs actions**
  - **Request parameters can be in URL query string and in the body of the message**
    - **Parameters in body aren't saved in bookmarks or most server logs**
    - **A better place for sensitive data**
  - **POST requests perform actions, like buying something**
  - **Clicking the browser's Back button displays a box like this**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b4a3b17c-20e5-4d77-90be-11be5e6e3719/image7.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667FUC4VAZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210158Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIFS%2BX5l4Gycgeyys1sTboRNdPlbMNskscRZP9VSoT2NsAiEAyLFpG%2FPrAvu%2F5WXD%2FYNWqiYz%2B2wIQg%2FyuH5dqnXPB0kqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDCjOo7wSiu1sHVq%2F%2FSrcA1bCUA9iFSlSszmHSKmXJi7HHGDOyn5v8ltB7r%2BIH%2BJzDH8EuPCUBIPfM%2Bz%2BtFA5XHWND%2FF0hmdh0gYu7n2202B4JBqEmnIvhfgiNgIHpKrQ1%2BEYrgSwqdmhl0bZoUI63byQrshZBBBzjRiALx1okfPGb1XZYHvKXGO0xKFj7s51LdBjV1h%2FwVIk%2FzweEbdJ4QUTx4MtrK1loNBd5pJD3%2FbgmgvLdnS3CEXf7QRx1AUzcvdRZgx4RwCqOuDR%2FnBNTJu1fEwLgkJYderqaSoNe%2FaiO0Dg3GTrcqLFP5R5KjZAYjj1fKimLyJS4C3M2%2FL7alX3zS3GmxIyF%2FE9XIL743so4F1oAAlSzp1GfqFI4QaR66K8Unaa%2BCnEoR3peuIO9nzIX9mmWxuBbcmRQZEu9AGD8ZLPxqf2C6ct33h5u1eEw2QYqNzHghCGStDaYs8AeQCMk0zOeQm5HKauia1CHUXkDSGcoTzUhcUy82aYiN04MhE1v1H4wUl%2BEriipRi134Q7Z%2BVP9BASXFwxZQWgljKQXs10j%2BkMeUbNlp1hGRv8y%2FlnkTmihQ7eqweiYQ6ua93jtwwWlnKwHak8WPoFFRHx0pf0ZlcK8LCh%2B9o0Exmryg3tVZLxTX4WjzYiMObGotQGOqUBAXvsBQaJFVXpJC5o4Ljxqin8KEDScayJe9n51czBoEzAtoNVkFyYWVL5aOrNGD7KVIsBGHzotGJlWDFgzmsUqgBEYCBRa4Ll79ufOGsJLZDS3A3MjaAsrYiDC0o%2FiLQ9HBC06Wy%2FhcwDVd8xlqM7d3BB204SfprnleKr1oF3oW2CdLxcxg%2B2m3hlHc0JuNhanRCuaFZcdanr9AihHoR1utOk1aYV&X-Amz-Signature=df85de1a9de9cc2844cd2edd41483460ebb48e591049359edcbe94405eb3236e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

1. **Other HTTP Methods**
  - **HEAD returns only the header, not the body**
    - **Can be used to check if a resource is available before Geting it**
  - **OPTIONS shows allowed methods**
  - **PUT uploads to server (usually disabled)**
## URL (Uniform Resource Locator)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1b7e9970-7b89-4d5f-8bfb-97b319b883ce/image8.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=dc621e31b8e004d74ea97cf07b5c45475c1dce29e0b1141edc669e09daf6d8bf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **If protocol is absent, it defaults to HTTP**
- **If port is absent, it uses the default port for the protocol**
  - **80 for HTTP, 443 for HTTPS, etc.**
## REST (Representational State Transfer)

- **RESTful URLs put parameters in the URL, not the query string**
- http: [//wahh-app.com/search?make=ford&model=pinto](https://wahh-app.com/search?make=ford&model=pinto) **becomes 
**http: [//wahh-app.com/search/ford/pinto](https://wahh-app.com/search/ford/pinto)
## HTTP Headers

### General Headers

- connection tells the other end of the communication whether it should close the TCP connection after the HTTP transmission has completed or keep it open for further messages.
- content-Encoding specifies what kind of encoding is being used for the content contained in the message body, such as gzip, which is used by some applications to compress responses for faster transmission.
- content-Length specifies the length of the message body, in bytes ( except in the case of responses to HEAD requests, when it indicates the length of the body in the response to the corresponding GET request).
- content-Type specifies the type of content contained in the message body, such as text/html for HTML documents.
- Transfer-Encoding specifies any encoding that was performed on the message body to facilitate its transfer over HTTP. It is normally used to specify chunked encoding when this is employed.
### **Request Headers**

- Accept tells the server what kinds of content the client is willing to accept, such as image types, office document formats, and so on.
- Accept-Encoding tells the server what kinds of content encoding the client is willing to accept.
- Authorization submits credentials to the server for one of the built-in *HTTP* authentication types.
- cookie submits cookies to the server that the server previously issued.
- Host specifies the hostname that appeared in the full URL being requested.
- If-Modified-Since specifies when the browser last received the requested resource. If the resource has not changed since that time, the server may instruct the client to use its cached copy, using a response with status code 304.
- If-None-Match specifies an *entity tag,* which is an identifier denoting the contents of the message body. The browser submits the entity tag that the server issued with the requested resource when it was last received. The server can use the entity tag to determine whether the browser may use its cached copy of the resource.
- origin is used in cross-domain Ajax requests to indicate the domain from which the request originated (see Chapter 13).
- Referer specifies the URL from which the current request originated.
- user-Agent provides information about the browser or other client software that generated the request.
### **Response Headers**

- Access-Control-Allow-Origin indicates whether the resource can be retrieved via cross-domain Ajax.
- cache-Control passes caching directives to the browser (for example, no-cache).
- ETag specifies an entity tag. Clients can submit this identifier in future requests for the same resource in the If-None-Match header to notify the server which version of the resource the browser currently holds in its cache.
- Expires tells the browser for how long the contents of the message body are valid. The browser may use the cached copy of this resource until this time.
- Location is used in redirection responses (those that have a status code starting with 3) to specify the target of the redirect.
- Pragma passes caching directives to the browser (for example, no-cache).
- server provides information about the web server software being used.
- set-cookie issues cookies to the browser that it will submit back to the server in subsequent requests.
- WWW-Authenticate is used in responses that have a 401 status code to provide details on the type(s) of authentication that the server supports.
- X-Frame-Options indicates whether and how the current response may be loaded within a browser frame (see Chapter 13).
## Cookies

- **Cookies are resubmitted in each request to the same domain**
  - **Unlike other request parameters, such as the query string**
A server issues a cookie using the Set-Cookie response header, as you have seen:

```javascript
Set-Cookie: tracking=tI8rk7joMx44S2Uu85nSWc
```

The user's browser then automatically adds the following header to subsequent requests back to the same server:

```javascript
Cookie: tracking=tI8rk7joMx44S2Uu85nSWc
```

### Set-Cookie Header

- **path - URL path for which the cookie is valid**
- **secure - transmit cookie only via HTTPS**
- **HttpOnly - Cookie cannot be directly accessed via client-side JavaScript**
Optional attributes

  - **expires - date when the cookie stops being valid**
    - **If absent, cookie is used only in the current browser session**
  - **domain - specified domain for which cookie is valid**
    - **Must be the same or a parent of the domain from which the cookie is received**
    - **"Same-Origin Policy"**
## Status Codes Groups

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5688e6c6-70d2-427b-b4b1-74b17472b5e0/image14.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UACFOVF6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210155Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCj8Mlv9ELNtUCRSJZUau7EMfZcrzj0ukWaG0lXeEfEZAIgd85%2BmQZkBoOG6n4SAsgrxVS%2BH8%2F%2Bi5LsuoPwUlAiCrIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP7Eba5K92TNuc4rNSrcA487LLaZ38Nvi7wVDdH%2BDOiDr0mPmOqNAW8yKWtekV2rg9JqET%2FOqkcaPTaJbu8uiRO8aWjJeki0npm%2FOM0LKV1T9YClz8GK0bcsTHuzOK1PPaZJO2dEwYFWSDuPxH23uZMkdj79lgxvuzIX46SOQZL%2BWM1OKGke7Zxj%2FUOycB2TTzVR2%2BUhYiSdUis6Xaa11uYm%2FHnCMh%2Fu4T0zMQEhOV0OscyfRYEdgX7B6k6Jxi34vp%2FWw7avufZXzV87EcAFXK02qrM0%2BuueJ9aIjjsLO%2BShjL%2B8EqwCFOP7KCZxusi4YhCTBXAsM3ELNvd9So7kc947tivyb%2Be52KpCIc0EuoJjtuzmQIt0qs4kU2qVJh%2B8AB5XZiLZxQiiClkNkGtJ03OeP3SXYUbbVmLc2S4RTNhxnuZ8IjZabsMncguT2aoqtwl5Sbsm%2Fv%2BvOR%2B0zes4AwwjbUEQGLi04nTEm991RyMF0xBRth74AGOSYFiBEP2bBrduhqPTvyyuk4zcO8es4nUApsfsnblNqQWLyUGRe9XwDEFUgQemRNE2KZpnuUB15YJKv4JuBYgjYDsT09h4InOkcr9yfIwItI%2BOhPteIIl0geWMjs2%2FQPFePKh%2B5dNa%2F%2FuJ6nz9S8k%2B2BvzMKTGotQGOqUB4HMXJx0uUflSRl3IoRx0WsWfIdeEuTuULGbTekQIyjXUTuh83k7n4AP2LtHQbOiK17wGWEHptt4mEmYtZpPAiWU0hWeobFwFCOBFqDGuVdOO2aSxrK5HDFMmobzuBzI5PQ%2FKOh2VDlC7uAIzut2iO%2B08Yc2OPRYBLsGLcF8Z%2BmvhdRPu%2FL76zrIqQptd%2BajmHXlX%2B1VL2lHIbBbTut5Ca7TNoqr4&X-Amz-Signature=501439401da5ba17fb3d5624bacfcce61f156ddd2acd8241f4fce04a6d003e4e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Important Status Codes

- **200 OK - request succeeded, response body contains result**
- **301 Moved Permanently - redirects the browser, client should use new URL in the future**
- **302 Found - redirects browser temporarily. Client should revert to original URL in subsequent requests**
- **304 Not Modified - browser should use cached copy of resource**
- **400 Bad Request - invalid HTTP request**
- **401 Unauthorized - Server requires HTTP authentication.**
  - **WWW-Authenticate header specifies the type(s) of authentication supported**
- **403 Forbidden - no one is allowed to access resource, regardless of authentication**
- **404 Not Found - requested resource does not exist**
- **500 Internal Server Error - unhanded exception in an app, such as a PHP error**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d7d16957-c053-4e73-b1cd-9a096be62c1b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663SZKZZMS%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210202Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCoAo3JazPsuPOS7ELhEd5JXcu7KAqjKhmpRUW1cbZN1QIgHsUukzaZAlbA%2FQEby4uVOKugokAt5DSsmcCK00jFO6QqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDNidfxwIiLwjavKizCrcAxjopnBZp%2Fm8UOSOjwnvpGivMUTudMH8wAFPzNXc1QGzEq2hzvu6csYGLT6ZJUyMkQjOojAFVQfKdMIce1mRWEqAsGKO%2FsuIAq4en3%2F6qUdlaudfkaeolZAMZkpLTJ0h2UfQRNwzFFLsedCFlH%2BoZG4ncFBYYIU4a4tUkW05pBYYlFjbk6A4IJA3Jn6TitzvtbXMusilUP7f6A3d35e2owPz2Iglv5YfNCIg1Ic9rah3TArtnnwxZ4YfPoW5xNr7Jhfx2DEKSJBgh%2F865RIwErNOeMWULqt7m%2BNetC5idVaNHdd9jr%2FV7xpxht%2BcV3bozd2hGrONqQuID%2Fd5olSNtgVMAtG9Ryd8BKyCt5cq8FfNR0%2BEQMZwUi%2FAEtpeTxYoCFSdPoJDIBmmNKJw5ESsbQLmo44IrfLWjnXBVAHQxf0NSm5qRoYXcGCtwFdZRYu34QIZ%2FuRKpj4LDFU9rAls2jsW4Ej5vXiAW8wcMY4i3vGibrOirzwdsViQOhrAstXdONT22ECo9SFEhknkZd0tW%2BlNVS0VHgtdBEklqQqm6vBc8KTowXeGil%2BAD03d5FEIurdVKdYwsKrCa9mBqFUo4wlk%2BX3S4Ppl8IaVJAs04ROLNtBjlaMZn8qz8%2FlqMIjJotQGOqUBbQje7WX1ki97FA2Hh41SG%2BIBqx5bG3K77FW0Xv2EIFZ6OGM%2F6yegoN6A70PgRa5NIsWbfz0R1kx6iv3xOfUEWDru5fjTq6rEOHh4JWbUVphOdwifTdY7bS%2FSUCBzxCUXPIzQWNus9r40NdY7yKDFe76k8ccbTaYR75tNmsDgkRRRAACHKCfDi0jUKUqJaXL9wQE8DE1VaGNODucgAoclI5NOAWGL&X-Amz-Signature=9eaa901b214ec5a5a89d6e82f20dda562a3da4091b36c536dcf2787dcbeccf8f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2ff60443-f464-450e-b840-ffb4d201d32e/image16.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664XHC66WX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210202Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC%2BF1Ri7EzCKXIQXCZIZFo6yXlOvKrCzZB2PIZLfnfbRwIgPg6h1EkOoroOzl%2F9wbHZ4E2VEN0w1rDsIlcmPlFxh7oqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFQ%2FeTtghbGBlpeKlyrcA9RLBi6FFkc40%2FuWH5jhzoaviTxhYEnp%2F%2BlBE3N5zJunuw%2B3XsnozmF%2BiDwYXdFvpLLSQN4%2FqeAQA5olpnmwsy2FtppEB6FM%2BNRpL6d3eEuAyjv%2BrjjAiPfKu5%2FTL2Sa%2FAQrqeQLbVzIhqJTaBLhy8ZRjCBksvZgyUri0NcMmsBOneutfX%2FPfJYdoAg8Sh%2Ft%2FF5rH9zI3cOE%2BBGeiHdHbomnS9q1E%2Bw1XkdAdnqeKXvEUMSH3R%2Bw22LySJcEAyJfRzWd1zCCMfbKlYH22hjaCCgbwNxZvpyGz5pFI41gb71fB2v6n7z1oDbuhqef81Vk3DlXs9OYM2T5gAbgS9aq5BYBa2GMXn1YArLFM3X5jHu5WZPTclw5bRmD0awVW52VQGMwfI%2BhLypyDU5NR%2F1ZHsiEeRXWW3rx%2FlIdjVWDiZz437OOt0r2tBO%2FEpa2fA%2FOKHJzLeju3Q9oqNvEhudRmZeBzrpF2EK34KNtlYw%2FbVXAB%2FoNG%2Ffuki%2B26X4ECPkq0A7%2FaBySpmKmb8bKVjkyvf24l%2BCUtJiZ1gm1ixua81hSGhtBweBAPLdepY1sxBQ3VMGceP4gphi6OqzXYwSffawglJkl1IXGzO%2FKzXnvtNcFc3QVhuCt8SjozsSaML3GotQGOqUBiWdLvbHGkQCrwiSjAewxh%2FCupXi%2FMvNwgUW%2BvhW%2Fhr%2FBitnkWgYLnnBte3gTRDAAP6d6G3kRyq4ATdbO1mbt6JYOiDUhJBDtanjz4pvtckH%2BWFTgDTDJ10nrHnhyGP6XdNy9AMvh9Z0P8mkGF6B78WmYDkcSejRTxScy%2B%2FtnjlQdjTIuX3O6U1xQwC7GFsAhw1bthHLVGzJGqTrMaqaPQbe4YSOl&X-Amz-Signature=875e00def134facecef45b5a60ef4799ef6e99dc82c270589dc90a222a0e1d8d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fc284b6a-7782-4e59-a0a7-204729e55c22/image17.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466R2OFK7RM%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210203Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDv8Yg8WNRJ%2Fdo1p310Vu5nQG2hnpiVQaN6nVErcVVJnQIgJMvPBSSjWtSMhbosxkC4Wyc2OTAUAqad8RnPXTWI2AYqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIBq3%2FW5oM2bW4B2wCrcAzJprD%2B7odhHvYAKoUiw4Jb0gbd%2FbYobrOyXLvbF8lgmuxUP65G97%2BBlhiF7QpUncuOryfDvpQaUEhLvp%2F1f0fpMkrNbDb8UlvSvjB9Aecd1beM3SQnP2a2%2BS4JpIujhC0o%2Blwvoguu1Tq8bftb%2FN9fFvXJyQqWFtCS%2BvG4LzXPQdmbOWH8qfx17t6S4M%2BeCOrUp9W%2ByL1Akrx99vfb%2BXXstk6ii1L50KTOvO%2FfkvFxNqE37HYGTgC3fp4kCUuQMeSJTZRSH6UwNY1SXB7n7sajYDWeyegOOFGRpLT8C8sjwa7sGp%2BCtoDwjkyom7ONXNIIKA6iF1boYcOgwx%2Fmza05wkvvBjQxKaEFDSzsCpnBA6DSWzfMaMDNK%2FvwPff05knpXrvNj6g2RMhMOm3Z2D2eVBZXuulHZfsqVT4y%2F1jB8PwDB40FqxtHA3hyK%2FermgyERnAV%2F%2Be%2FSlTS1gXnbpRPY%2BtA3ay4VO%2F6naDCm%2BJ90284z7lP8LWXROZwJ2tCfoQO6fCQ5FOmiShSQCan6TJeDqc51e032UoPa8aR4zCKsOXShW9OJldz6oJinpUsbJkAXqQ1kiTqoLJ6juiQhDSAzmvP%2ByiqpTrepj8t5oQhXpUfh4VYGHxpOGm9KMMTGotQGOqUBSDzcnvqkytMBkF4pgAr5%2BIB7SjCe459Dur%2B9vmM9FMTBM0fGzBUkyuf7uES044%2BSBD2jD0e%2FzEjj2v7LxUJsqJdxdFkz0tI9%2BKcIkFKXpjvFNSljay6OrCeM2prjtM1O9tKq0mlwt2vlZ8Aok2UrpwFDjKN8zCIJ8DeoIdyv1Vyq4UL8FpeN%2F97G8G6j1gp6PR1Yd5y%2BoYGrssPan%2FuXj%2Fr6YqAg&X-Amz-Signature=8e7439ce25b3c74ab57b14c8cd5fdf29be600213e195bcce4d535b677272fa34&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3ecc2cee-896d-4013-89cd-6c18309d5a09/image18.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663BAVVFGU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210203Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCRjlNaNQOdqB5%2FSgeTwwUJGeNVGHZKih%2FpINH6eikBzQIhAMuLQHgulzjq%2FVZNThR3X4hpKO9Inz5cCYJ3zIbUHNjrKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igyk0MLP7%2FfS%2FzPo48Qq3AOIccUuH7%2Bw2VQgKrPPAdU%2Bm%2BqGVZYoLUzaVpvb2H2R77IezZRmg6wGq4aIiKnKMU8XGMko%2Br6tBsUeFWp%2Bsv4qkToDlryMD7gSUKxRiFxxvrkm28b%2FlsKgl0ksV0NpSnEVxEJMq4USD9m1Az53LS3DW4wBTYf4LwxWMdikzb0X0qitALEL%2FzHIONgHzXKUI1TB%2FggkhvZqQB8fv4ehI2%2F9XohGpKklKT6KdfTY42nBNtZGZgcovlyE04W%2F0556Uv9BDvnS6zS8V0JhEnb6DOVav%2FwjcUTmyWQeJt9oZvtn0QVIdV8MwhKpii%2FSz471xPSUq%2F0pJ%2BtwezUgxuWxqOSPrnY58KQ3AOcS%2FcpKCct1hmNHfton5loKwc5odH3v%2FGB%2FXYDADq%2BU5KwRKjTzcU%2BKEnit4RxuAYrLvOjJPhNbYKijNc%2Fyu9W0JVAh%2BPuH8y0JZra1tANZNc2f6qsNMabA3GFbCmfBAxMGnt6%2Brta7hWeQKFUQVIL8%2B49VQOaMpLv%2Br3lIQYjHy5g2INJsICe%2F8aO0U6gctGrVZviUVBBovs%2BeupARkBHAOkdZWuaduOp6d7BXHkWpZ3c%2B3AgpuqXPnsV%2F0NDpTY5JVPUzf3dMOfowjXfxwMGWYM1tfTCIxqLUBjqkAXAUrAO%2FPcduwPYE3nTHx9gm9q5onla5kMVFlQ3pAvnvlY25%2BPNykEiZGiIsLTYZ%2BfsbyL%2FLj6G%2BornKI3uk5BvP9UJz%2Bxy%2BI4BcgQ%2B3nNbhGtDUs8BwaJJ290b3EGRiTpm3TFKOtdjwsfWyY1krcJZJ70redMDhnWz2FGIOsstZXhtL2liLnOMZPpeUqeB1lBfvlJZz449HwCzSRX9ilsnC197K&X-Amz-Signature=d0c3d6bf20b31869c22aa34c10e99809ac66d0260ed8932a929fd5fe6e67280f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## HTTPS

- **HTTP over SSL (Secure Sockets Layer)**
  - **Actually now TLS (Transport Layer Security)**
  - **All versions of SSL are deprecated**
  - **Protects data with encryption**
  - **Protects data in motion, but not at rest or in use**
## HTTP Proxies

- **Browser sends requests to proxy server**
- **Proxy fetches resource and sends it to browser**
- **Proxies may provide caching, authentication, and access control**
### HTTPS and Man-in-the-Middle (MITM) Attacks

- **HTTPS connections use public-key cryptography and end-to-end encryption**
  - **Only the endpoints can decrypt traffic**
- **Companies wishing to restrict HTTPS traffic have two choices**
  - **Perform complete MITM with fake certificates, or real root certificates from trusted CA's**
  - **Allow encrypted traffic to trusted domains without being able to inspect it**
### HTTPS and Proxies

- **Browser sends an HTTP request to the proxy using the CONNECT method and destination hostname and port number**
- **If proxy allows the request, it returns 200 status and keeps the TCP connection open**
- **Thereafter acts as a pure TCP-level relay to the destination web server**
## HTTP Authentication

- **Basic: sends username and password in Base64-encoding**
- **NTLM: Uses Windows NTLM protocol (MD4 hashing)**
- **Digest: Challenge-response using MD5 hashing**
- **These are generally used in intranets, not on the Internet**
- **All are very weak cryptographically, and should be protected with HTTPS**
# Web Functionality

## Server-Side Functionality

- **Static content - HTML pages and images that are the same for all users**
- **Dynamic content - response created in the fly, can be customized for each user**
  - **Created by scripts on the server**
  - **Customized based on parameters in the request**
When a user’s browser requests a dynamic resource, normally it does not simply ask for a copy of that resource. In general, it also submits various parameters along with its request. It is these parameters that enable the server side application to generate content that is tailored to the individual user.

**HTTP requests can be used to send parameters to the application in three main ways:**

1. **HTTP Parameters****
**May be sent in these ways:
  1. In the URL query string
  1. In the file path of REST-style URLs
  1. In HTTP cookies
  1. In the body of requests using the post method
1. **Other Inputs**
- **Server-side application may use any part of the HTTP request as an input**
  - Such as User-Agent
  - Often used to display smartphone-friendly versions of pages
1. **Web Application Technologies**
  1. Scripting languages such as PHP, VBScript, and Perl
  1. Web application platforms such as [ASP.NET](http://asp.net/) and Java
  1. Web servers such as Apache, IIS, and Netscape Enterprise
  1. Databases such as MS-SQL, Oracle, and MySQL
  1. Other back-end components such as filesystems, SOAP-based web services, and directory services
### **The Java Platform**

- **Standard for large-scale enterprise applications**
- **Lends itself to multitiered and load-balanced architectures**
- **Well-suited to modular development and code reuse**
- **Runs on Windows, Linux, and Solaris**
### **Java Platform Terms**

- **Enterprise Java Bean (EJB)**
  - Heavyweight software component to encapsulate business logic, such as transactional integrity
- **Plain Old Java Object (POJO)**
  - User-defined, lightweight object, distinct from a special object such as an EJB
- **Java Servlet**
  - Object on an application server that receives HTTP requests from client and returns HTTP responses
- **Java web container**
  - Platform or engine that provides a runtime environment for Java-based web applications
  - Ex: Apache Tomcat, BEA WebLogic, JBoss
### **Common Components**

- **Third-party or open-source components that are often used alongside custom-built code**
  1. Authentication — JAAS, ACEGI
  1. Presentation layer — SiteMesh, Tapestry
  1. Database object relational mapping — Hibernate
  1. Logging — Log4J
### ASP.NET

- **Microsoft's web application framework**
  - **Competitor to Java platform**
- **Uses .NET Framework, which provides a virtual machine (the Common Language Runtime) and a set of powerful APIs (Application Program Interfaces)**
- **Applications can be written in any .NET language, such as C# or VB.NET**
### **Visual Studio**

- **Powerful development environment for ASP.NET applications**
- **Easy for developers to make a web application, even with limited programming skills**
- **ASP.NET helps protect against some common vulnerabilities, such as cross-site scripting, without requiring any effort from the developer**
### PHP

- Originally "Personal Home Page", now "PHP Hypertext Processor"
- Often used on LAMP servers
  - Linux, Apache, MySQL, and PHP
- Free and easy to use, but many security problems
- Both in PHP itself and in custom code using it
**Common PHP Applications**

- Bulletin boards — PHPBB, PHP-Nuke
- Administrative front ends — PHPMyAdmin
- Web mail — SquirrelMail, IlohaMail
- Photo galleries — Gallery
- Shopping carts — osCommerce, ECW-Shop
- Wikis — MediaWiki, WakkaWikki
### Ruby on Rails

- **Allows rapid development of applications**
- **Can autogenerate much of the code if developer follows the Rails coding style and naming conventions**
- **Has vulnerabilities like PHP**
### SQL (Structured Query Language)

- **Used to access data in relational databases, such as Oracle, MS-SQL, and MySQL**
- **Data stored in tables, each containing rows and columns**
- **SQL queries are used to read, add, update, or delete data**
- **SQL injection vulnerabilities are very severe**
### XML (eXtensible Markup Language)

- **A specification to encode data in machine- readable form**
- **Markup uses tags**
```javascript
<pet>ginger</pet>
<pets><dog>spot</dog><cat>paws</cat></pets>
```

Tags may include attributes, which are name/value pairs:

```javascript
<data version="2.1"><pets>...</pets></data>
```

### Web Services and SOAP (Simple Object Access Protocol)

- **SOAP uses HTTP and XML to exchange data**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/a5a11991-0a3b-4bba-9983-9e171807b5a4/image24.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RNVO3GLB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210211Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBWjg0bvJlOYndS2%2F6Qm8j1XiHOe8Fy8bBPKoxjDlKDaAiAn1cKw%2Fs5NTsOGNl8FpPhOVY59v52Wz8tOnNk%2BTY9EWyqIBAit%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMnz%2B5U76uiqaRKNp6KtwDjrm%2B0vr0maVc23EQJP%2FLqr259jQW758pL%2BzLg%2F6LUvGlEaOY%2FpM58KkXPzNQlIq0z2OUZ%2F5oRF7VyqQugc1ltYR2TEIOBEkRYkV9jbwgt1S56oyPYDMQhvEOk86Zc0atJ00oLK1YCWhsPEfD9j6k54GUSo7%2BPFko928aqvQrYJH2Q20noQW2oferV7oNSxAyTbpi4FAdA3wiW3RD1vA7VTe6L6d5yzNFZmUPq%2Fxg20SlRLptXcHbhJV63BOijYXvceiTx3AS03c3MgoSqse5s1N6gvJhhkMDHNUZxzVhjQUndSkYbradYX2xPHRlTkeHrjf1QMYBpH2qEI0H%2Fbm5JA2Ff1Y5SQ6Jkz6GrZHjjjvngRSN2JXvpCeTRzkrYcU86zpU6ZnqEpGiS6lNLE3GkfbygLMJmzxSP3GgcZDvA6j2CG3jUUTt%2F3PAIG0HKfoSBz4dME8u%2FP37Gat%2F7T6dyh1GnEmoeU8oEi%2FUwtW4WipGcy43UTig7oUCU7ptOhnNZlwGnmKjE4%2BAm%2BbHENZn3uiIVf2EFGnBvf8Y4i7W%2F%2Bk4%2FK%2BBtZx8T8zDLYtNSgwNKzkN%2BSjIO6xzvvehIXKdIW8F5Dk0A4bWdFrjb%2BLnS0uUqfJ2Re1vQ8P2Nlowz82i1AY6pgFzmll8nHzL7cbTsSGNT02tiptAFVnozVkIvGI2lhG4Y%2BXe1oaX7qUq8R03MQA9G%2F9I8FdFyqzluNGfrUiWFIRaVxyxLZVQp0k7hpGm5PCUEpuAMOyg5UWUc9AhABujQx%2BmQx9eTiiraDDscXLeY8TEMLh%2FccThGRHybs%2FIhv5tbwSd7m2EbkoX3vuVwRHI%2ByxV0pho0Av3otWHizcl9AozMRsGah9C&X-Amz-Signature=b636eb9a514a560959dcd86744687d5b3f8b61fb1520c3523d3722d7c4528d85&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **If user-supplied data is incorporated into SOAP requests, it can have code injection vulnerabilities**
- **Server usually publishes available services and parameters using Web Services Description Language (WSDL)**
- **soapUI and other tools can generate requests based on WSDL file**
## Client-Side Functionality (in browser)

### HTML Hypertext Markup Language

- **HTML used for formatting "markup"**
- **XHTML is based on XML and is stricter than old versions of HTML**
### Hyperlinks

- **Clickable text that go to URLs**
- **Clicking this link:**
```javascript
<a href="129S/129S_S22.shtml" target="_blank"> CNIT 129S: Securing Web Applications</a>
```

- **Makes this request**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1271266b-93a7-4f25-a844-1ce81c2f716a/image27.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=4d04f7909269855c35d64c96ae5990762ea91f9373ed6e8192bba8560a75853c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### HTML Forms

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/42f4d52c-382e-4819-9c56-592bbb228549/image28.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=2c4e5e587f970454513f44fadb75a03e884b9cdeedb15b896b49fcff82149022&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/42cdd1cd-a206-4f5e-bfce-b47dbe0451a5/image29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=f2de595262990177c985caee3384252949e947723c0076ace93862ae81538ba1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**HTTP Request**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/af79dc02-5507-430e-8463-0ff9df88190e/image30.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=87468ec732e4e2d8dafe0622ab4958671a86652a90f931b975cff10b2720c571&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### multipart/form-data

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/98918a79-8c13-4919-a799-5c04953eddee/image31.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=27a5405736242818a5b7248b6f9a786435a3e639b56d06076e39f955dedb0ad4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d4050ea6-30a5-470d-a646-5c9c1c1be859/image32.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=fa83f826e5f3bf8be1bc60b973b8c7c27b7be8817a8bd099d3db85962068bd8a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **Browser generates random boundary text**
**HTTP Request**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b044719c-7963-4128-b5e6-71d4b6b8fb95/image33.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=1348abf58a67ddb61f1f760be471e4941c932c394e861eded7fcd6e0d1e1a63b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### CSS Cascading Style Sheets

- **Specifies format of document elements**
- **Separates content from presentation**
- **Has vulnerabilities, and can be used for attacks**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/704b6c84-6847-48a1-b8ec-0bd6348d0f0b/image34.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664ATEEXD4%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210211Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCxboDAbiDTHbk2mA8js1ltImPrTQNHMXv4WP3GOrnVYQIgRgVbuN5FrZES9L0u7rCbd5%2BpGG0IDYvu9AmHgQSdC%2BMqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDE%2BGSzW0LWwA0POuVCrcA9ebj4XN2Oi%2FDKsIs5xeVpWs6GR%2BRQAtiZop%2Fj6G7S63kUHd150aW%2BtO2WnJHFoEFGmbnlpLWsvB%2F8N0hjLXrYMMbUHgAaDJoif5%2FJyDoFtBTeRXG8RF2uvWsaaqwGnvGgudtNWOR4A5PFWmDoMgBrYqIlj6RKXXThIlWm6YCedoBLGjaYkGkjGrm66i8%2FrCrJUaIB5EWFuUsBoBcshxPWeb08hWA1JdTvKYUokhdMsoJxF8THwB7zu0dB5b3xZGCm7Tebaq4CpXKasdK%2B0UWXG5h8mbuDfAdL6ib8ynzxQ12IdqJRFR5tTxBu7zXHzJuWkcYEMvk7TYR1PJdUI3pDbOEqjmuKe14T%2BirOqIhmRJxJ8Sbvnvz2Si8Ck5p0Gh1iVPweAdR77ZWHg2DcOz8A%2F97K7T%2FVIXP%2FVERfC0TYuzyvfjYzMh%2BdjdSmvEV5MZ9t84QGgW5LuYSSKr2l9RvOqucIEUdB1GwFBdEQK8K7P0CQ2kaUZ805ZXaexH4q4voHP3wbOae0TV7rUNLmjx5mWu75kSATER8yh%2BbvVphwXihH59OMEWOc0xCh0T4lbeEABAINcbhkNRdnXtfKOwf2zAedMYk7KzWADeQxToTTLMMFuI5MIPHZkwd611MP7FotQGOqUB52LWMponIlJ4qfUPmJs8RXiTM4xjIOHF9LpOs3pBpa%2B8QcGk7GWBDrzfEcL1CTBCSk5Z%2FDXIfNLvQ61uNxkErmFnXo6j7Zly4X5GZUXWZLLkgiwI7qAOEyxVN2UKElGzox2PaYIoSXJAim5ZDpnsfds1jP%2FaQ2jlbz77ifUnPhs%2BuHSgpgHxOCbnR6rObOuMlDwChlj9YeiOrhLostIinYIgk7GE&X-Amz-Signature=16b1fbd301a187640f3f6669ca138b54f2fc94f093b5b172b853b0a34431907f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Javascript

- **Scripts that run in the client's browser**
- **Used to validate user-entered data before submitting it to the server**
- **Dynamically modify UI in response to user action, such as in drop-down menus**
- **Using Document Object Model (DOM) to control the browser's behavior**
### VBScript

- **Microsoft's alternative to JavaScript**
  - **Only supported in Internet Explorer (now obsolete)**
- **Edge does not support VBScript**
### Document Object Model DOM

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/75866999-a500-4527-a326-6e245327762f/image35.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPQHQY7U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210205Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC8KkgCrF9WSfC7VkJPrHPU580s6S5VLid7R52N8G61PwIhAJVVPrPUf9ymWMrEo9ig9ZzlsP0DydBIvbendbnmkOy5KogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzwqE%2BKukiojSRe%2BMYq3ANle1STBvKcHMWnVJZcuR44URhlwzZSw1Qd6vR%2FTAQxPHdvLSveT2reUjfN75QwUpXa5Eg06OSCZOuKcZWXMpKe3KokNBvS6y2TgttctGTaWPWMdz1BkBI82quQ6%2FIiKN9WftdDqDxeAByFCYtT7pWLVKbvyKsT6AWDYphp2eY%2FpcwrqXKo0845PA8TLv6jFoTTjgBujZdKrdJvXD3EuYIzSlXVa5mJRL4alYEbGHX1qrT6vTN7eyrjOrkfc2iU8GA5a%2B3Nm39aEKZ5ac6xnGAbATNaMESDjBsWES4lGFC8ij8Zb5ENDOwcV6hwm%2F3I%2BAx1K4io6fgXlZThqoXfR%2FjaaKzcfaY4yktIETCC3izzcSWFyKDeVH%2FdIDukmgJcCyti7icwKbLidfVa5tGIWMZHCocYOVBLuGp9Fl16gGHWjWcF7Zp5sX8awXq4NfcOLt1tZ77lLUIq6eLpCEFTCHFEqAEwslbs7yTPuluQbm8qz6HkUzknq5gKU3l%2FRSQpB9xcDvvcN%2BlE1FH8bNddDMgLU3XM5wrNfmNpFLE86lb3%2BhAG6IpgSTBfVa2nQrdOZIZyUawTZgaugHP00rlOXv9W7eMeooqbb8Yc%2FIMtt9R4WdcIKqypwBtfFCO5XzDUyKLUBjqkAcqyGfWuj706dFX92sy04uHUkG%2F6KqfA9fWSM0Cds6QtU7InhC3h8nraFAUBGOIsNFZBiNKeITEa9E4kFB9HH8BBr3zg%2F5zR1z%2FXzIhEeXBGceFV5AyFAL%2FPDZlHdM7x8SnOBq7xwwX0HiOhbkmyb83461NsN6C7CoBHaE%2BFhkWZUy%2FOiA7BKptC1k63iv86Fw7z%2BpCTMHGSVTpAWQtMa7L1%2BU1x&X-Amz-Signature=5413dbafa41a39633abc78a298016478a6fe56efce7704d1cdf164e45f5113cc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> Using the DOM

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2ec15e97-1724-42f5-ae5d-78a178e002b7/image36.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665B5W7QL7%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIA6XQudF%2BPn6QqSnD%2BWO9xxIX1Tc4vDJwrBAGlNEes0HAiAWLo2omo92cD2kYt6myU9XsYyygyn31jZv6u4Al4RvkCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIM5hu2c2UvNxq8%2BZzSKtwDBKcfFIfowqereqi4rk8wL6ozwN8VpZk%2BeZSixtQ4gz%2F4bo%2Bsw5oz%2F8SXZqFZH8Nts9dSpyQOYyBlJ7fN2k5svySAw9Y1s5zq17gA%2FHILtn1vcxNLth0rZq0AZNNaaYdz8M1yFYidDmki3ld%2FveB58%2Br%2B068hJWVzY2%2FgHeXP9dotZ3%2BNcUo2LzjUkMcI1N281UaTufSaD68E55vxF1pDqjyjj3RdnsG%2FMbeSSoHmiZisMWzhu76qnhQQH%2BVH7OEtyUloMLmpJ5yahd5QJx1FJmZR9hPkU9elTUYF7i%2FibkLN0zkoPSkcgqoVwDAAGiKMZ3TDzByegWZdh4%2BVzyhbo4HuyLiPvxGBncHPfesvzenF%2BGZHI%2B0RbOl0Lo7jFj4217iVo4fz4PfIF8aUL7Lp9KlHMJsdxUQ97ZTcwc6%2F3j8YzAgsqdH5D8V9trxc3ylNNPpYvKnJd336a4mJJ%2FDt5tey%2FzhIArjp%2B89Lmkqj0GbJgjPFiYpdIrGfNhWxcYjL3lUqe4s9QA%2BZqkCtAPELkUxa%2FZ2j%2FixeVLrjoffuL602SgMweNxWaVYvMoc7SNPYpEGO9DPeEW9UIUcyQ1hDIu8DPRULfaMyguYjy%2FRfRoSyxvU1ZBqNYvhwCUkwmcai1AY6pgHaTwt4zzh8%2BJbCz7DJxhkg%2FrgxpxzGyHoRm%2Fs6b0dZ%2FtZC%2BAknQL%2BVYUev%2BDQoK1FjxRQRlFaWxWS%2F3Z%2FTqjAp%2F%2BRhB%2FwPRvk%2F6rrtBYXjh33wUyRMw1aUaPF4OTgV%2FJhFJY31B3%2BdCZ2OsQbP%2F%2F3%2BQdFdgtGBGwnhdi7Bn3olJlFIRMBL015nfrqRq5n%2F5nhhJx5py5AgKPbU%2BVQh6ra%2BmXIqlM3u&X-Amz-Signature=94370f0a57f4d7c6e9015442453a64c421d483367ddc356e34f8e33f8c8c6b81&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/dbc01141-0948-4d3a-afea-92ce6da91c23/image37.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VIXNNJSI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210213Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCICy%2FmDHUHpv%2BPx%2Bk2bfoJHqtJspZpnv4JeXvAAvXXU8eAiEA2gOfSBkjHdz0HxwsWdOSxmTT0mfJrF7qTM6hcqjJxBcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGRcpSBH0u2qNL75ZyrcA4uCsrOwcF1NKqTTNIAgeAwkPjh9B9qXpLPs2wcwl24J%2FBV0Lu2SWsapwQOImynwHlQb2p6TxRFd2SsUNGyGjbzZ3Z0ovlptzTCi4HfvIusYoxzD7VWD0tqpcH2diqIuM1Md6Pa8VnQIUJr0e8nOAfOaiAWYK6B1B4%2BwP25nCnTuXbpKG210GSBJolfayw7Sr%2B0fUm%2FJnBlpvPGBNzMIm1gOVmhzxrlmdiX7l5M5pMngIvjtWv0E6FAByQFkY1zfL%2FRXK14wpwYDI46DOal5I%2BeANGYK5p4CH10Pueb9CBSjlgU2iLE3rN8IU4oh6E9ftBWNDl%2BqyXCN93GVsZfcqSm8ncWzzZc%2BNJCz5L4SRbfI4TmCibt%2BPgq8vdG6fRtRzJ4EU2bLcRSROfoT0bIRtGTH2WEcF%2FJqXK4DJi8gPuCszWZT%2Fao2o9LKoD4mqnd%2B96vAXgyqm3CyVVpYGRT90guvL2E6nq0af1DN81Jj%2BIScR9ewUuAWOp1JCsPpuA1nJw0zXY5IBlj0v3He8yIQoybN%2FlgK8cRH4t6w0oxrTwr8lznBuHpiKQTI3n88dziZg1EHzpdH4GrxNL0i7obAy4NPESluZ3bf23HDL15qbaAyxViX3CaNiKyQzsiKMJfJotQGOqUB2iDKFlT3kysU8r%2FLcdcu2IEK0kt6qmJTlXgSNoqUL5i11LmT0lhLP3W13DEgz081i2vW9kTQFIC0BX1NxkbZAXqPtMmy5sk4WDEEG1tTAB1ovg4YhFyKh115RfKdViYQ4AWii5hIuWrSHyxvfi0JVzASwEPd04uTaSFqlSNV8pFmTTJAflQhR%2Fuq7kQQW5gNRBCVwNwMbIR%2BXiGdy%2BYqsER4IHfT&X-Amz-Signature=e732f781f96b9065465cb12b267c934490ba428c0cce6a6c54e54cb287affbb6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


### Ajax Asynchronous JavaScript and XML

- **Client-side scripts can fetch data without reloading the entire page**
- **Allow you to drag Google Maps around**
Example

- **Google Maps API**
- **Links Ch 3h, 3i**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/78714397-b67f-409f-a927-863918602b6a/image39.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=39b05dc06d13f707a5b7520e55f2af2c6b80676336a32900657693b7c12388da&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### JSON JavaScript Object Notation

- **Client-side JavaScript uses the XMLHttpRequest API to request data from a server**
- **Data is returned in JSON format:**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d5107810-cf7f-4c9f-b8b6-2c8a27972b11/image40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=aea13292d89e109326fa7d65666bfaba496246c4c4da8c7b0df3aef6fc3810f8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Updating Data with JSON**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8a052a4a-a1ca-4118-befa-dcdbdd60673f/image41.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=c8cf2eacc595035da41f979b114162bb261f6fe99433ce85bfe420273a9afe65&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Same-Origin Policy

- **Prevents content from different origins interfering with each other in a browser**
- **Content from one website can only read and modify data from the same website**
  - **Ex: scripts on Facebook can't read or write to data on your online banking page**
- **When this process fails, you get Cross-Site Scripting, Cross-Site Request Forgery, and other attacks**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e5b710f9-ba71-4b37-aefa-2910a24531f7/image42.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=0cebe8348760bf6f429536458e6a377925c426fe17cc4d2bb8bc588459d13a4f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### HTML5

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/23f86878-d345-432c-9655-70265b205510/image43.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=84956d5962616760d55c90c9ce0d20cac7dd3c354c6949d5d853196957989ab0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Web 2.0

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/eb698da1-5c1c-4c62-a4b6-c51ba2dcc468/image44.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=6fa77d0c57a2bf6f88f0533c3016fd1477984fd7a0375d99bd196252790ad8d7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Browser Extensions

- Java applets
ActiveX controls
Flash objects
Silverlight objects
- **Many security problems**
- **More and more restricted in modern browsers**
## State and Sessions

- **Stateful data required to supplement stateless HTTP**
- **This data is held in a server-side structure called a *****session***
- **The session contains data such as items added to a shopping cart**
- **Some state data is stored on the client, often HTTP cookies or hidden form fields**
# Encoding Schemes

## URL Encoding

- **URLs may contain only printable ASCII characters**
  - **0x20 to 0x7e, inclusive**
- **To transfer other characters, or problematic ASCII characters, over HTTP, they must be URL- encoded**
%3d — =
n %25 — %
n %20 — Space
n %0a — New line
n %00 — Null byte

A further encoding to be aware of is the + character, which represents a
URL-encoded space (in addition to the %20 representation of a space).

**Note**

For the purpose of attacking web applications, you should URL-encode any of the following characters when you insert them *as data* into an HTTP request:

space%? & =; + #

## Unicode Encoding

- **Supports all the world's writing systems**
- **16 bits per character, starting with %u**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/47b64dda-ccec-466f-acab-9e4d27e4ab45/image46.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=58a136c45c19e4fb03655f6ddbade51be5e70aab84b88abeaf37eb49d2ccbfb3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## UTF-8 Encoding

- **Variable length**
- **Uses % character before each byte**
- **Unicode and UTF-8 are often used to bypass filters in attacks**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cb7a482a-10d9-4991-bce0-9b465e154b3a/image47.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=98798bef8dcb72385b3827ea8471dab933ba7c37b593b879edc86e8b04e3508a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## HTML Encoding

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49134948-39a5-47ff-bb0f-f2a6a005ff6d/image48.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=fcf6551840d862bab39ce18f5afa95aed996453246de79f30d078d3d9fc61fef&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

- **HTML-encoding user data before sending it to another user is used to prevent Cross-Site Scripting attacks**
## Base64 Encoding

- **Represents binary data using 64 ASCII characters**
  - **Six bits at a time**
- **Used to encode email attachments so they can be sent via SMTP**
- **Uses this character set**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0ff2ff46-574e-4c04-90bd-efe1270e15d4/image50.jpeg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=38ea28a6a1330e8fdb5cafe70a8379679257e36dc2887dc77736603ec72be95f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

## Hex Encoding

- **Hexadecimal numbers corresponding to each ASCII character**
- **ABC encodes to 414243**
> Remoting and Serialization

Frameworks

- **Allows client-side code to use server-side APIs as if they were local**
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/71a6c101-20cd-4b8c-af4b-816924af918c/image51.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XHFRXHW2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210212Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDJDEPIE6RJ7YELubPBDQ39wK2NMIhOJjRLr23qKTdb2gIgN54i98zON0k6nCvL1FVV7YfjbMEjsTTZji8Y%2ByWGIKIqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDIVosK3x4SBxxmcZXircA597lDb1EFW1dA4DMsVscn732%2FjomvGF8eGBEgZP5hmvKKHePBWnSiLbhXzbz1TCmUNc7phYw7bcFydf0yeN3smWqWkBY%2BAO%2FJIvXqGbZhCMPwRTq2Mg4CJZG75Jac6XQL2sBH2YCeacS5zBqD4YXdqWGmKFEbuobHXvO82iCp5SQli%2FpFc1nZDTPnSMTj6l0%2FehtCCVUpHG%2Fr93d16xtknQ5dpy3tkcntzMMPqohluxcJJzczz4ZD1S09HPVW4J6FCV7jrd9wVljyFXTnjEhpS8u2BxQ1QijoPo8t75pozRcS0%2Bp86UUZIew0YpEIQ5H0cnRMI9P75s%2FNgc%2BdiqxuVeiIn5CVOVdxUaGhwdDX9dCbbUwBFDPq7UgtvS68DjtIKo1tLvfrlYVr%2BDZrcA8V7pCiLefOGIkRwnyUqU9qaMbpR6KLPnerM%2BbGBVyo9IrxBm%2Bdby%2BApwaNn0nQb9b%2FCj6p7r3f2g3kOh1rLnvNN5UCYJ%2FezoRiJdZI9r4e4E%2FbPCFEmJm4PiUaiylycGRGpaYKkWTgPwZ68KmKplkH7fFskxYc2TkYgY8S9W%2B8O0kQ4UEtsogr0D9PcR4LOPCKun9iY9I4ZO9nndqypaDZSz%2F2pacVUBbiYYX7VPMPPJotQGOqUBQXX555c%2FFNMDgkQqbm8HY%2F6GoAPKDEDdNfkBtO8c%2Bh2yb4VstEn10uqSAgeFGPw4gLTQ%2FoUGP3OcASHB6FAWoxoLwT9ZX0FL8k2cp6sGMaRJLtuVbLJm0tFCM689ffK8Kt9VzZWF46AaY0ZQQIlyoUlnE7%2FOFPty3rJYjbMpmkLnKx5bsgmYzNGQnnwJfQYEzpS8uw9PH80sUKinZ5JyfTSQS51r&X-Amz-Signature=2d8170eb0e69f86320ec6100d914812d0bf78faa03d2894b5656e6bac345f380&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

