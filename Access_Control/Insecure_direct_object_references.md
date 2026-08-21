# Insecure direct object references

### Target Goal - 

find the password for the user `carlos`, and log into the account.

### Analysis/Exploitation -

- Select the **Live chat** tab.
- Send a message and then select **View transcript**.

**It’s sending a GET request to **`/download-transcript/2.txt`**! and we can see our own session’s transcript in response.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/43fe081c-ae5c-4bd3-938c-4c1e20dbf72b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YB6PGZCR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221919Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHzNAIIh%2Fu%2BKcP%2BUOhIs%2BkdVcwzhU%2FFBe2fJ4qAiuSgyAiBCR1a9eamKMoVjakV%2BE8pyuWqqkEAs6nevErtlOCZafiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMx3XNlQo0nule27oiKtwDp%2FrZzFZXdOh4wpQxed4cnI2fsS%2FM7U2IiadZIkNoFDGvqOTIb4X1asC7d2sMlhPyZioZ%2FuS1CDDPwqTMqGK7dixAN62LVD91fdYWuzcP%2B4S%2B3ntTd7XIWaBhB2fgTMdJUQ7%2BfYqVffMffzYY%2FozXVA27WJSo0tuEy%2B%2BdEs0Gr%2B2JkLAzHosGW5P74xWqTnvtnUQltJcZIr94kjLd6Vj%2F8CdJKLKFq1mF1YiyhPFIa5mGt6PbS4ApNkON7lR4H5qb3s65dKK4OabEiqN5167xan1w7swkcB15rHJUTyVAXjeURdUsm89rXwl1DPKLHiP%2FlFRjNxEPEYNDwwgpI8XcQAEF5UKAvZ%2Buqpcy8T8ErnamnKZlNEkyN0batMLJUVppg4HomLad1MIOcAfjf7Puh7Gpr%2BFWXl%2BruG1M%2FY2j%2FZju5B20cufn44syIP12vgu3ScRVmgzoqPurH%2BH%2BGiBFUHKRDrd30ZzqJ5wiWmqPaBMthjQJBD9Zkv7SR1xk1%2B2N3n7yC00PTVoRAU%2FVKDLdSxCfaEQpm6gc1yvBWnJLrid1e7VAKUNGj40lej%2FAv31v0IWnbqXkwagaX7TAXdcmqHC8gSRXygHNg%2BU%2Fcl81xCY9ebjPEkuEv1L6e4Mw%2FoOj1AY6pgHHVvAwkDhytR9iSmIlaYJOUTQp3qKRfax0HxDW4TO0Mk3Jj3RnwrkBTyNJg1z6a3jisogzknepGpm3uch5ac9d%2Fdr%2Fw52QkibUKrhU2x8WOMLfkVboeUVtwYyCKXS0%2BkS%2Br%2F%2FIfYYjVHdA54sQN8%2BnRunIGarlBauNHNmpDqFzpY7NNXmR4OdnmsDdSvEUjGEanuajStCdCJul3cVEa1Ylti0Y9oE0&X-Amz-Signature=3f1b719c56df23585910d8335b20ce1356795075e671a4b72dd8c6ea25f96ac4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**What if I change the **`2.txt`** to **`1.txt`** Or **`3.txt`**, and so on?**

Change the filename to `1.txt` and review the text. Notice a password within the chat transcript.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c2f0a595-8a0c-45e3-ab3e-1abdbd8020c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YB6PGZCR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221919Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHzNAIIh%2Fu%2BKcP%2BUOhIs%2BkdVcwzhU%2FFBe2fJ4qAiuSgyAiBCR1a9eamKMoVjakV%2BE8pyuWqqkEAs6nevErtlOCZafiqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMx3XNlQo0nule27oiKtwDp%2FrZzFZXdOh4wpQxed4cnI2fsS%2FM7U2IiadZIkNoFDGvqOTIb4X1asC7d2sMlhPyZioZ%2FuS1CDDPwqTMqGK7dixAN62LVD91fdYWuzcP%2B4S%2B3ntTd7XIWaBhB2fgTMdJUQ7%2BfYqVffMffzYY%2FozXVA27WJSo0tuEy%2B%2BdEs0Gr%2B2JkLAzHosGW5P74xWqTnvtnUQltJcZIr94kjLd6Vj%2F8CdJKLKFq1mF1YiyhPFIa5mGt6PbS4ApNkON7lR4H5qb3s65dKK4OabEiqN5167xan1w7swkcB15rHJUTyVAXjeURdUsm89rXwl1DPKLHiP%2FlFRjNxEPEYNDwwgpI8XcQAEF5UKAvZ%2Buqpcy8T8ErnamnKZlNEkyN0batMLJUVppg4HomLad1MIOcAfjf7Puh7Gpr%2BFWXl%2BruG1M%2FY2j%2FZju5B20cufn44syIP12vgu3ScRVmgzoqPurH%2BH%2BGiBFUHKRDrd30ZzqJ5wiWmqPaBMthjQJBD9Zkv7SR1xk1%2B2N3n7yC00PTVoRAU%2FVKDLdSxCfaEQpm6gc1yvBWnJLrid1e7VAKUNGj40lej%2FAv31v0IWnbqXkwagaX7TAXdcmqHC8gSRXygHNg%2BU%2Fcl81xCY9ebjPEkuEv1L6e4Mw%2FoOj1AY6pgHHVvAwkDhytR9iSmIlaYJOUTQp3qKRfax0HxDW4TO0Mk3Jj3RnwrkBTyNJg1z6a3jisogzknepGpm3uch5ac9d%2Fdr%2Fw52QkibUKrhU2x8WOMLfkVboeUVtwYyCKXS0%2BkS%2Br%2F%2FIfYYjVHdA54sQN8%2BnRunIGarlBauNHNmpDqFzpY7NNXmR4OdnmsDdSvEUjGEanuajStCdCJul3cVEa1Ylti0Y9oE0&X-Amz-Signature=574ef48ba5c37abab6c684cd782f9fbb7b6235ba466c7a191c7388e503f5535b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It should be **user **`carlos`**’s password!**

Login as carlos with this password
