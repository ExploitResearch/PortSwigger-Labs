# File path traversal, traversal sequences stripped with superfluous URL-decode

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

open any product or open any image in new tab

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/475ced47-f148-41c1-8ec6-0c1c5e097f33/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LKCJWTH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215535Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAvg8pscDYRVv4CbLc%2BDpq2hHk8x90bEOmI8c9lnr4DkAiBwRH%2FTU4UNEHclmxYGEb924mJZHwvPoaSERpvN0ceDoCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMddQRRV7SRMcmjEbzKtwDBP%2FewxexOMol6ImHbqwsBPXbumewsroW1VnTawXkBhSLdRho0LeouuAo95YPIEL1L9fvdHdUSnW4PUoAo5G4TT2pvBFixj7adzaCbnVT8fwv%2FXtY5rofRV9EK7rc4SP1M%2B2zxHRBZLdxt3oD984NJrsB8tIskzGVDjt3KyTj54KgUpROeKXJRAo3v5UT5EeHwx4X4%2BDvDPWDOoKXAa%2BUP1s1%2FOSgYR2BPqb7kMJp9x4jZhKpfEW5VDnI1T7%2BK2Wm32otiMGgGONtvJmI93xZh75PqPWjMvTOv3dYvi15Iy7xqPiMTWAKdiX0jtEJDgqdhCOYJ2dO3INdzAiZQtYAztYAU7Jxz%2BEUbgsUfde9vthqwa1mXB7UJgVV3ed%2BBHgBwnYjPoorhWo%2BEVrZm%2FxJvB8%2F9q9QLb%2FoFdI%2BKoal6fF%2BsR2AMDj3b94fTZSu%2FEuApBWs%2Bw5l%2B6tZA0fbGBJindCvDtlQjdxhb34o6tpIzYO%2F9G2FjjLzIoGGyK4WOkJyNmtFUgbe3kbolwHgDyqYJXM0fupSC7rFN9LFEtggrYH0kEnBbpxVfBEhxoiU4XcAhmOSQsl4U9EPhDPXZ8Y4USiweQ4WJEth4jt6rUuh6ng6%2FoMQj9b5oUT12C4wx4aj1AY6pgGwui50Q1ow2YMWIPxabC2R4uzqzAvgdVmxZqhgXHNbAb%2B0v93sJNFDLeGeMj45pI0MJxFOH8Su%2FMELE6PJ7pHu0KH3w%2B8ylOeBt6uI030jrMXKyFpP0XyEwmZrFWnWOeuTNBRDPAUx%2Fk61UV6u%2FU8qDyvhoOGKpDWnoSjjFrtf%2Bi9YTk59a9iQ4RH5KFL4r08L9d51kw2BRbKZe4EA8Zc%2F3Sx5aOgB&X-Amz-Signature=d30664cafa31c52f0c3bf6c1305388656f3c5ecad115e8cf89938eea206c9511&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

apply above filter to see image request and sent it to repeater

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/be73ff94-1b0b-4941-90e1-fefafce76325/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LKCJWTH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215535Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAvg8pscDYRVv4CbLc%2BDpq2hHk8x90bEOmI8c9lnr4DkAiBwRH%2FTU4UNEHclmxYGEb924mJZHwvPoaSERpvN0ceDoCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMddQRRV7SRMcmjEbzKtwDBP%2FewxexOMol6ImHbqwsBPXbumewsroW1VnTawXkBhSLdRho0LeouuAo95YPIEL1L9fvdHdUSnW4PUoAo5G4TT2pvBFixj7adzaCbnVT8fwv%2FXtY5rofRV9EK7rc4SP1M%2B2zxHRBZLdxt3oD984NJrsB8tIskzGVDjt3KyTj54KgUpROeKXJRAo3v5UT5EeHwx4X4%2BDvDPWDOoKXAa%2BUP1s1%2FOSgYR2BPqb7kMJp9x4jZhKpfEW5VDnI1T7%2BK2Wm32otiMGgGONtvJmI93xZh75PqPWjMvTOv3dYvi15Iy7xqPiMTWAKdiX0jtEJDgqdhCOYJ2dO3INdzAiZQtYAztYAU7Jxz%2BEUbgsUfde9vthqwa1mXB7UJgVV3ed%2BBHgBwnYjPoorhWo%2BEVrZm%2FxJvB8%2F9q9QLb%2FoFdI%2BKoal6fF%2BsR2AMDj3b94fTZSu%2FEuApBWs%2Bw5l%2B6tZA0fbGBJindCvDtlQjdxhb34o6tpIzYO%2F9G2FjjLzIoGGyK4WOkJyNmtFUgbe3kbolwHgDyqYJXM0fupSC7rFN9LFEtggrYH0kEnBbpxVfBEhxoiU4XcAhmOSQsl4U9EPhDPXZ8Y4USiweQ4WJEth4jt6rUuh6ng6%2FoMQj9b5oUT12C4wx4aj1AY6pgGwui50Q1ow2YMWIPxabC2R4uzqzAvgdVmxZqhgXHNbAb%2B0v93sJNFDLeGeMj45pI0MJxFOH8Su%2FMELE6PJ7pHu0KH3w%2B8ylOeBt6uI030jrMXKyFpP0XyEwmZrFWnWOeuTNBRDPAUx%2Fk61UV6u%2FU8qDyvhoOGKpDWnoSjjFrtf%2Bi9YTk59a9iQ4RH5KFL4r08L9d51kw2BRbKZe4EA8Zc%2F3Sx5aOgB&X-Amz-Signature=60be988a8470cb9829758096096c3f8f02a1b56fc42054cb3503a90466d4b06a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0dc06af9-28a6-42d2-859b-c4683d5fdb0d/2024-02-16_00-02.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LKCJWTH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215535Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAvg8pscDYRVv4CbLc%2BDpq2hHk8x90bEOmI8c9lnr4DkAiBwRH%2FTU4UNEHclmxYGEb924mJZHwvPoaSERpvN0ceDoCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMddQRRV7SRMcmjEbzKtwDBP%2FewxexOMol6ImHbqwsBPXbumewsroW1VnTawXkBhSLdRho0LeouuAo95YPIEL1L9fvdHdUSnW4PUoAo5G4TT2pvBFixj7adzaCbnVT8fwv%2FXtY5rofRV9EK7rc4SP1M%2B2zxHRBZLdxt3oD984NJrsB8tIskzGVDjt3KyTj54KgUpROeKXJRAo3v5UT5EeHwx4X4%2BDvDPWDOoKXAa%2BUP1s1%2FOSgYR2BPqb7kMJp9x4jZhKpfEW5VDnI1T7%2BK2Wm32otiMGgGONtvJmI93xZh75PqPWjMvTOv3dYvi15Iy7xqPiMTWAKdiX0jtEJDgqdhCOYJ2dO3INdzAiZQtYAztYAU7Jxz%2BEUbgsUfde9vthqwa1mXB7UJgVV3ed%2BBHgBwnYjPoorhWo%2BEVrZm%2FxJvB8%2F9q9QLb%2FoFdI%2BKoal6fF%2BsR2AMDj3b94fTZSu%2FEuApBWs%2Bw5l%2B6tZA0fbGBJindCvDtlQjdxhb34o6tpIzYO%2F9G2FjjLzIoGGyK4WOkJyNmtFUgbe3kbolwHgDyqYJXM0fupSC7rFN9LFEtggrYH0kEnBbpxVfBEhxoiU4XcAhmOSQsl4U9EPhDPXZ8Y4USiweQ4WJEth4jt6rUuh6ng6%2FoMQj9b5oUT12C4wx4aj1AY6pgGwui50Q1ow2YMWIPxabC2R4uzqzAvgdVmxZqhgXHNbAb%2B0v93sJNFDLeGeMj45pI0MJxFOH8Su%2FMELE6PJ7pHu0KH3w%2B8ylOeBt6uI030jrMXKyFpP0XyEwmZrFWnWOeuTNBRDPAUx%2Fk61UV6u%2FU8qDyvhoOGKpDWnoSjjFrtf%2Bi9YTk59a9iQ4RH5KFL4r08L9d51kw2BRbKZe4EA8Zc%2F3Sx5aOgB&X-Amz-Signature=8844da2de655ade0322b1fbae3441d1814ef8e343f11c2489a48110ff7846a95&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Therefore A valid filename for the path traversal for `../../../etc/passwd`is  `%252e%252e%252f%252e%252e%252f%252e%252e%252fetc/passwd`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3aef0c4f-c3b5-4921-8807-cc7e2eb3d2e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LKCJWTH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215535Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAvg8pscDYRVv4CbLc%2BDpq2hHk8x90bEOmI8c9lnr4DkAiBwRH%2FTU4UNEHclmxYGEb924mJZHwvPoaSERpvN0ceDoCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMddQRRV7SRMcmjEbzKtwDBP%2FewxexOMol6ImHbqwsBPXbumewsroW1VnTawXkBhSLdRho0LeouuAo95YPIEL1L9fvdHdUSnW4PUoAo5G4TT2pvBFixj7adzaCbnVT8fwv%2FXtY5rofRV9EK7rc4SP1M%2B2zxHRBZLdxt3oD984NJrsB8tIskzGVDjt3KyTj54KgUpROeKXJRAo3v5UT5EeHwx4X4%2BDvDPWDOoKXAa%2BUP1s1%2FOSgYR2BPqb7kMJp9x4jZhKpfEW5VDnI1T7%2BK2Wm32otiMGgGONtvJmI93xZh75PqPWjMvTOv3dYvi15Iy7xqPiMTWAKdiX0jtEJDgqdhCOYJ2dO3INdzAiZQtYAztYAU7Jxz%2BEUbgsUfde9vthqwa1mXB7UJgVV3ed%2BBHgBwnYjPoorhWo%2BEVrZm%2FxJvB8%2F9q9QLb%2FoFdI%2BKoal6fF%2BsR2AMDj3b94fTZSu%2FEuApBWs%2Bw5l%2B6tZA0fbGBJindCvDtlQjdxhb34o6tpIzYO%2F9G2FjjLzIoGGyK4WOkJyNmtFUgbe3kbolwHgDyqYJXM0fupSC7rFN9LFEtggrYH0kEnBbpxVfBEhxoiU4XcAhmOSQsl4U9EPhDPXZ8Y4USiweQ4WJEth4jt6rUuh6ng6%2FoMQj9b5oUT12C4wx4aj1AY6pgGwui50Q1ow2YMWIPxabC2R4uzqzAvgdVmxZqhgXHNbAb%2B0v93sJNFDLeGeMj45pI0MJxFOH8Su%2FMELE6PJ7pHu0KH3w%2B8ylOeBt6uI030jrMXKyFpP0XyEwmZrFWnWOeuTNBRDPAUx%2Fk61UV6u%2FU8qDyvhoOGKpDWnoSjjFrtf%2Bi9YTk59a9iQ4RH5KFL4r08L9d51kw2BRbKZe4EA8Zc%2F3Sx5aOgB&X-Amz-Signature=5303c8ca0dfa7766a5d8870508492d6cc92e24202f8da191f8f4b6c5ddd16c1a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### An alternative payload

Of course, when using Burp Repeater it is much easier to just type the `../../../` part in, than select it and `right-click -> Convert Selection -> URL -> URL encode all characters` twice.

This also encodes the `2 5 e f` characters from the first conversion, leading to a filename of `%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66etc/passwd`, which is also perfectly fine here:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39cf9dee-255d-4d2e-8760-7c7459129acc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662LKCJWTH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215535Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIAvg8pscDYRVv4CbLc%2BDpq2hHk8x90bEOmI8c9lnr4DkAiBwRH%2FTU4UNEHclmxYGEb924mJZHwvPoaSERpvN0ceDoCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMddQRRV7SRMcmjEbzKtwDBP%2FewxexOMol6ImHbqwsBPXbumewsroW1VnTawXkBhSLdRho0LeouuAo95YPIEL1L9fvdHdUSnW4PUoAo5G4TT2pvBFixj7adzaCbnVT8fwv%2FXtY5rofRV9EK7rc4SP1M%2B2zxHRBZLdxt3oD984NJrsB8tIskzGVDjt3KyTj54KgUpROeKXJRAo3v5UT5EeHwx4X4%2BDvDPWDOoKXAa%2BUP1s1%2FOSgYR2BPqb7kMJp9x4jZhKpfEW5VDnI1T7%2BK2Wm32otiMGgGONtvJmI93xZh75PqPWjMvTOv3dYvi15Iy7xqPiMTWAKdiX0jtEJDgqdhCOYJ2dO3INdzAiZQtYAztYAU7Jxz%2BEUbgsUfde9vthqwa1mXB7UJgVV3ed%2BBHgBwnYjPoorhWo%2BEVrZm%2FxJvB8%2F9q9QLb%2FoFdI%2BKoal6fF%2BsR2AMDj3b94fTZSu%2FEuApBWs%2Bw5l%2B6tZA0fbGBJindCvDtlQjdxhb34o6tpIzYO%2F9G2FjjLzIoGGyK4WOkJyNmtFUgbe3kbolwHgDyqYJXM0fupSC7rFN9LFEtggrYH0kEnBbpxVfBEhxoiU4XcAhmOSQsl4U9EPhDPXZ8Y4USiweQ4WJEth4jt6rUuh6ng6%2FoMQj9b5oUT12C4wx4aj1AY6pgGwui50Q1ow2YMWIPxabC2R4uzqzAvgdVmxZqhgXHNbAb%2B0v93sJNFDLeGeMj45pI0MJxFOH8Su%2FMELE6PJ7pHu0KH3w%2B8ylOeBt6uI030jrMXKyFpP0XyEwmZrFWnWOeuTNBRDPAUx%2Fk61UV6u%2FU8qDyvhoOGKpDWnoSjjFrtf%2Bi9YTk59a9iQ4RH5KFL4r08L9d51kw2BRbKZe4EA8Zc%2F3Sx5aOgB&X-Amz-Signature=8e1b257e3e73a543b6bb78085b83c04e416481494263864d844ab6536ec9d0e3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
