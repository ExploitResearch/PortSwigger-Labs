# File path traversal, traversal sequences stripped with superfluous URL-decode

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

open any product or open any image in new tab

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/475ced47-f148-41c1-8ec6-0c1c5e097f33/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YTS4PLFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210406Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDt3IX6%2FfDiYPGXcGkabygluW6KfQDJu8diLrzXRLiU5AiAz6d%2BRJBzTDZbERfL7LlzJIH5JskFFMKs7XityCjPtPyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMuzqUB8Wvh2MN36yTKtwDh4t3m1%2BGbel6cowN6nZa7DVkC%2ByGMywvx5mKQY1hRFrvbeuO0BiYfwGHcrbYSeJ1aTPfthY4VDiVuRguKGUVDzOX%2FYIUUaV2uHs8bKvbUJ6Oblyix1EmCFUjL09vUNjaXcR8NtXx9e%2FsitSw2cv0NSlBZ1eVP3RNnrpmr8REHfMBuqDvwL8pgPlT9OwMwyom%2Bw4mDG9NGdR49lLkBEATXANa%2FST8olvfszV%2Ft5zguecNA0jsKTkDoNdzoC1jaHpHBySn%2B%2BZKdW3xmTfUmw%2BRaRmBotV5BQA%2BLJMV7i5RXqcmZ2r6kzn2HkvJk3RmHPcurpo02NFfd99P8b21psY5VC6gSEU0BDVUow8ECYmn%2F1lLoD7cMD3d2llIJmywgLlB%2BKgJA0lyuF9pZR%2BskA3nAAfO9mr2ELQjF7Fv6fzuQPGrC%2F3E4x%2F%2BGcIS9505D%2F1mNZJ1lPvIpydmHZ6KXAsr3LMzNjlbnUdLS0I5KOCdBAeRP%2FuYlmC0rAuqe%2FIqzcy1P4qQp7T6O0aurq01PFFELxxQw%2FhnqkuiwOAI%2BQdxT%2FaD7LDB1LGtdKkNseNpMMDcDP1391QQ6U5uGATXdDnJGkPZ7SSrl1CxaD92HMzts%2FX0rp5McKpdapSdP1gw78ai1AY6pgHOVQm%2Fk3aRUYg%2BGqKDMp31dftUep3CBar3m4%2BNaOancds5H6DGpxYrB1jKySQj5gpZ5a8WaAUT2iWqBZ5qh3v3%2FkAj5XKKmZLRLsYc6%2FR8xwGrHJtGI6bxKPyYRaAKh113zBVH9czSC5iFhubLL1opFgegpLo5gFg%2Brpgv%2BKqgND%2BdCyGfp9asIv4KJGTvgTaabnUuvSQWCAVKkojHN1qFlCuyPhF9&X-Amz-Signature=529d13637360b30e065a3cd626c96a96f34f7988b7d3678849a702ecf492acc0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

apply above filter to see image request and sent it to repeater

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/be73ff94-1b0b-4941-90e1-fefafce76325/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YTS4PLFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210406Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDt3IX6%2FfDiYPGXcGkabygluW6KfQDJu8diLrzXRLiU5AiAz6d%2BRJBzTDZbERfL7LlzJIH5JskFFMKs7XityCjPtPyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMuzqUB8Wvh2MN36yTKtwDh4t3m1%2BGbel6cowN6nZa7DVkC%2ByGMywvx5mKQY1hRFrvbeuO0BiYfwGHcrbYSeJ1aTPfthY4VDiVuRguKGUVDzOX%2FYIUUaV2uHs8bKvbUJ6Oblyix1EmCFUjL09vUNjaXcR8NtXx9e%2FsitSw2cv0NSlBZ1eVP3RNnrpmr8REHfMBuqDvwL8pgPlT9OwMwyom%2Bw4mDG9NGdR49lLkBEATXANa%2FST8olvfszV%2Ft5zguecNA0jsKTkDoNdzoC1jaHpHBySn%2B%2BZKdW3xmTfUmw%2BRaRmBotV5BQA%2BLJMV7i5RXqcmZ2r6kzn2HkvJk3RmHPcurpo02NFfd99P8b21psY5VC6gSEU0BDVUow8ECYmn%2F1lLoD7cMD3d2llIJmywgLlB%2BKgJA0lyuF9pZR%2BskA3nAAfO9mr2ELQjF7Fv6fzuQPGrC%2F3E4x%2F%2BGcIS9505D%2F1mNZJ1lPvIpydmHZ6KXAsr3LMzNjlbnUdLS0I5KOCdBAeRP%2FuYlmC0rAuqe%2FIqzcy1P4qQp7T6O0aurq01PFFELxxQw%2FhnqkuiwOAI%2BQdxT%2FaD7LDB1LGtdKkNseNpMMDcDP1391QQ6U5uGATXdDnJGkPZ7SSrl1CxaD92HMzts%2FX0rp5McKpdapSdP1gw78ai1AY6pgHOVQm%2Fk3aRUYg%2BGqKDMp31dftUep3CBar3m4%2BNaOancds5H6DGpxYrB1jKySQj5gpZ5a8WaAUT2iWqBZ5qh3v3%2FkAj5XKKmZLRLsYc6%2FR8xwGrHJtGI6bxKPyYRaAKh113zBVH9czSC5iFhubLL1opFgegpLo5gFg%2Brpgv%2BKqgND%2BdCyGfp9asIv4KJGTvgTaabnUuvSQWCAVKkojHN1qFlCuyPhF9&X-Amz-Signature=73ad213f5fe194f1996053b46e187a96cfb5809a547d09be37eab241d183eb1c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The lab description mentions that the application removes path traversal sequences first, then URLdecodes the remaining.

URL encoding is a means to ensure data is within the character range that is allowed in URLs, regardless of the actual value of the data. It is usually used for data that either contains characters
 that have a special meaning within URLs (e.g. `&`) or is non-printable data. But of course, it can be used for any printable ASCII characters.

In the case of characters within the normal ASCII range, the character is represented by a `%`, followed by its ASCII value in hex. The characters required for a path traversal and their encodings are:

```text
. --> %2e
/ --> %2f
```

### Accessing /etc/passwd

One level of URLdecoding is usually done by the server itself upon receiving the request. Therefore just encoding `../` as `%2e%2e%2f` will not be enough. The server performs the URLdecoding and passes `../` to the application, which filters it out. So URLencode the encoded string again before sending.

For this, we need to  also encode the `%` character itself:

```text
. --> %2e
/ --> %2f
% --> %25
```

One possible string would be `%252e%252e%252f`. The server decodes each `%25` to `%`, the strings `2e` and `2f `by themselves have no special meaning and will be treated as literal characters. The application, therefore, receives the sequence `%2e%2e%2f`, strips path traversal components (which are not there at this point), then URLdecodes it to `../`

**Now, we can use **`%252E%252E%252F`** as **`../`**:**

or we can **use **[**CyberChef**](https://gchq.github.io/CyberChef/)** to do URL encoding:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0dc06af9-28a6-42d2-859b-c4683d5fdb0d/2024-02-16_00-02.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YTS4PLFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210406Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDt3IX6%2FfDiYPGXcGkabygluW6KfQDJu8diLrzXRLiU5AiAz6d%2BRJBzTDZbERfL7LlzJIH5JskFFMKs7XityCjPtPyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMuzqUB8Wvh2MN36yTKtwDh4t3m1%2BGbel6cowN6nZa7DVkC%2ByGMywvx5mKQY1hRFrvbeuO0BiYfwGHcrbYSeJ1aTPfthY4VDiVuRguKGUVDzOX%2FYIUUaV2uHs8bKvbUJ6Oblyix1EmCFUjL09vUNjaXcR8NtXx9e%2FsitSw2cv0NSlBZ1eVP3RNnrpmr8REHfMBuqDvwL8pgPlT9OwMwyom%2Bw4mDG9NGdR49lLkBEATXANa%2FST8olvfszV%2Ft5zguecNA0jsKTkDoNdzoC1jaHpHBySn%2B%2BZKdW3xmTfUmw%2BRaRmBotV5BQA%2BLJMV7i5RXqcmZ2r6kzn2HkvJk3RmHPcurpo02NFfd99P8b21psY5VC6gSEU0BDVUow8ECYmn%2F1lLoD7cMD3d2llIJmywgLlB%2BKgJA0lyuF9pZR%2BskA3nAAfO9mr2ELQjF7Fv6fzuQPGrC%2F3E4x%2F%2BGcIS9505D%2F1mNZJ1lPvIpydmHZ6KXAsr3LMzNjlbnUdLS0I5KOCdBAeRP%2FuYlmC0rAuqe%2FIqzcy1P4qQp7T6O0aurq01PFFELxxQw%2FhnqkuiwOAI%2BQdxT%2FaD7LDB1LGtdKkNseNpMMDcDP1391QQ6U5uGATXdDnJGkPZ7SSrl1CxaD92HMzts%2FX0rp5McKpdapSdP1gw78ai1AY6pgHOVQm%2Fk3aRUYg%2BGqKDMp31dftUep3CBar3m4%2BNaOancds5H6DGpxYrB1jKySQj5gpZ5a8WaAUT2iWqBZ5qh3v3%2FkAj5XKKmZLRLsYc6%2FR8xwGrHJtGI6bxKPyYRaAKh113zBVH9czSC5iFhubLL1opFgegpLo5gFg%2Brpgv%2BKqgND%2BdCyGfp9asIv4KJGTvgTaabnUuvSQWCAVKkojHN1qFlCuyPhF9&X-Amz-Signature=72c3504cf3ac84b46bc7ca7c6d3a36cf7da42a6f8b91d854834308de61359d38&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Therefore A valid filename for the path traversal for `../../../etc/passwd`is  `%252e%252e%252f%252e%252e%252f%252e%252e%252fetc/passwd`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3aef0c4f-c3b5-4921-8807-cc7e2eb3d2e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YTS4PLFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210406Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDt3IX6%2FfDiYPGXcGkabygluW6KfQDJu8diLrzXRLiU5AiAz6d%2BRJBzTDZbERfL7LlzJIH5JskFFMKs7XityCjPtPyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMuzqUB8Wvh2MN36yTKtwDh4t3m1%2BGbel6cowN6nZa7DVkC%2ByGMywvx5mKQY1hRFrvbeuO0BiYfwGHcrbYSeJ1aTPfthY4VDiVuRguKGUVDzOX%2FYIUUaV2uHs8bKvbUJ6Oblyix1EmCFUjL09vUNjaXcR8NtXx9e%2FsitSw2cv0NSlBZ1eVP3RNnrpmr8REHfMBuqDvwL8pgPlT9OwMwyom%2Bw4mDG9NGdR49lLkBEATXANa%2FST8olvfszV%2Ft5zguecNA0jsKTkDoNdzoC1jaHpHBySn%2B%2BZKdW3xmTfUmw%2BRaRmBotV5BQA%2BLJMV7i5RXqcmZ2r6kzn2HkvJk3RmHPcurpo02NFfd99P8b21psY5VC6gSEU0BDVUow8ECYmn%2F1lLoD7cMD3d2llIJmywgLlB%2BKgJA0lyuF9pZR%2BskA3nAAfO9mr2ELQjF7Fv6fzuQPGrC%2F3E4x%2F%2BGcIS9505D%2F1mNZJ1lPvIpydmHZ6KXAsr3LMzNjlbnUdLS0I5KOCdBAeRP%2FuYlmC0rAuqe%2FIqzcy1P4qQp7T6O0aurq01PFFELxxQw%2FhnqkuiwOAI%2BQdxT%2FaD7LDB1LGtdKkNseNpMMDcDP1391QQ6U5uGATXdDnJGkPZ7SSrl1CxaD92HMzts%2FX0rp5McKpdapSdP1gw78ai1AY6pgHOVQm%2Fk3aRUYg%2BGqKDMp31dftUep3CBar3m4%2BNaOancds5H6DGpxYrB1jKySQj5gpZ5a8WaAUT2iWqBZ5qh3v3%2FkAj5XKKmZLRLsYc6%2FR8xwGrHJtGI6bxKPyYRaAKh113zBVH9czSC5iFhubLL1opFgegpLo5gFg%2Brpgv%2BKqgND%2BdCyGfp9asIv4KJGTvgTaabnUuvSQWCAVKkojHN1qFlCuyPhF9&X-Amz-Signature=19d89bcebae575fedaba4121818ff48d2638bbbec4f6a1ecf795cbfb2e605ec2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### An alternative payload

Of course, when using Burp Repeater it is much easier to just type the `../../../` part in, than select it and `right-click -> Convert Selection -> URL -> URL encode all characters` twice.

This also encodes the `2 5 e f` characters from the first conversion, leading to a filename of `%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66etc/passwd`, which is also perfectly fine here:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39cf9dee-255d-4d2e-8760-7c7459129acc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YTS4PLFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210406Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDt3IX6%2FfDiYPGXcGkabygluW6KfQDJu8diLrzXRLiU5AiAz6d%2BRJBzTDZbERfL7LlzJIH5JskFFMKs7XityCjPtPyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMuzqUB8Wvh2MN36yTKtwDh4t3m1%2BGbel6cowN6nZa7DVkC%2ByGMywvx5mKQY1hRFrvbeuO0BiYfwGHcrbYSeJ1aTPfthY4VDiVuRguKGUVDzOX%2FYIUUaV2uHs8bKvbUJ6Oblyix1EmCFUjL09vUNjaXcR8NtXx9e%2FsitSw2cv0NSlBZ1eVP3RNnrpmr8REHfMBuqDvwL8pgPlT9OwMwyom%2Bw4mDG9NGdR49lLkBEATXANa%2FST8olvfszV%2Ft5zguecNA0jsKTkDoNdzoC1jaHpHBySn%2B%2BZKdW3xmTfUmw%2BRaRmBotV5BQA%2BLJMV7i5RXqcmZ2r6kzn2HkvJk3RmHPcurpo02NFfd99P8b21psY5VC6gSEU0BDVUow8ECYmn%2F1lLoD7cMD3d2llIJmywgLlB%2BKgJA0lyuF9pZR%2BskA3nAAfO9mr2ELQjF7Fv6fzuQPGrC%2F3E4x%2F%2BGcIS9505D%2F1mNZJ1lPvIpydmHZ6KXAsr3LMzNjlbnUdLS0I5KOCdBAeRP%2FuYlmC0rAuqe%2FIqzcy1P4qQp7T6O0aurq01PFFELxxQw%2FhnqkuiwOAI%2BQdxT%2FaD7LDB1LGtdKkNseNpMMDcDP1391QQ6U5uGATXdDnJGkPZ7SSrl1CxaD92HMzts%2FX0rp5McKpdapSdP1gw78ai1AY6pgHOVQm%2Fk3aRUYg%2BGqKDMp31dftUep3CBar3m4%2BNaOancds5H6DGpxYrB1jKySQj5gpZ5a8WaAUT2iWqBZ5qh3v3%2FkAj5XKKmZLRLsYc6%2FR8xwGrHJtGI6bxKPyYRaAKh113zBVH9czSC5iFhubLL1opFgegpLo5gFg%2Brpgv%2BKqgND%2BdCyGfp9asIv4KJGTvgTaabnUuvSQWCAVKkojHN1qFlCuyPhF9&X-Amz-Signature=251d38487b937e0010cf63a7fc7fd3efdecf9945e7c2f220807aeb0d3efce5d0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

