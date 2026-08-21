# File path traversal, traversal sequences stripped with superfluous URL-decode

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

open any product or open any image in new tab

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/475ced47-f148-41c1-8ec6-0c1c5e097f33/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667IIIQRKY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204700Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCEVsusSrqlRsDDl1RhNNQDYgsvxFCaSD4kquzCTekkDgIhANfsWXRLZEieNgf7VN7apJw5wmShox0ful4X4%2FuQKY9rKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzJ60pXaeVvW11rMQEq3APCQQH5E6QfEe5NYO34G0%2B444AJ5it4Fo9mrv%2BbRsBrRVaFIoTtbQXsFQC0jvIEeZwmMa11N5HIL9A65QLhXP8Pql28c2gBs0tM4%2FBb3M1u%2BMw%2BxCvph4rYodZ9ql8LeTeRg7e4%2BYae7dmuPxB1CAEH4ihlHVUmpTHMFeeZm1W9ICq93Lwi6AlIt4J%2BzP0qlytFZw9FwUooeub7DJ2aX5NYriLoUjo9Z5kBDaE0Vk%2BWbPHstSODW4eVbGYTYZD17WSvQUfKslGBP4R8xnrTOu95N%2Fyc5x6LpeyXg5u3NFIPAnIgL%2BI1cEaO1a87lT7eluy3TceES46ZemcWvdyeOG9x8LsG4tjAxlJXlalzfwIEK6vZH16kb%2BmM%2BMF5z3Bic8ct6tdAib77hyfDXKx%2FvxOZPdofGdoGSG%2Fi6imP6J5gycuBCp5919QoaFMZkwbULCN69ov4WgFTgukLGOtGa%2BUuhH9UHK1fWbzl2mb5GmTUE63kdvpJVTZhnAAy8rYG3rixpSbDnxFYwYXMoujPeRw59hGNV6rM5NPViHbOzkJWwTAYMTHHaWKxHZGuTo8mjdxA9kjC4sMAfB%2Bx5JYk%2FOfdDpIkrD1w30Gidaqx9j1TqvI6CuRQ2sQaXQer0zCaxqLUBjqkAaKwVj6xYqvZsNdr9b3cOJu5RppQ0tr0sy8vwbhllbLHmpqBL%2F4IVNFIUyvjgpDEtCAIeL8u7mP1JQoapSbaWeEUDK9DIBB1805C3OIIQTl3bFr%2BolCVH8zRC%2B470ldOfcAULNHdxi5%2FZWMqZOv9XKBfo2FZ%2B3mAFcyZEpLLVfBQru5yJMaIyuWq8ySLKne%2Fl3dnTmYM1IlvY7T3vxfWnctya8Wi&X-Amz-Signature=a78bae4b94b4eb7c8de0536f708f02f75b0c737a79a1184ce4e27fb9d0751253&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

apply above filter to see image request and sent it to repeater

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/be73ff94-1b0b-4941-90e1-fefafce76325/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667IIIQRKY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204700Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCEVsusSrqlRsDDl1RhNNQDYgsvxFCaSD4kquzCTekkDgIhANfsWXRLZEieNgf7VN7apJw5wmShox0ful4X4%2FuQKY9rKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzJ60pXaeVvW11rMQEq3APCQQH5E6QfEe5NYO34G0%2B444AJ5it4Fo9mrv%2BbRsBrRVaFIoTtbQXsFQC0jvIEeZwmMa11N5HIL9A65QLhXP8Pql28c2gBs0tM4%2FBb3M1u%2BMw%2BxCvph4rYodZ9ql8LeTeRg7e4%2BYae7dmuPxB1CAEH4ihlHVUmpTHMFeeZm1W9ICq93Lwi6AlIt4J%2BzP0qlytFZw9FwUooeub7DJ2aX5NYriLoUjo9Z5kBDaE0Vk%2BWbPHstSODW4eVbGYTYZD17WSvQUfKslGBP4R8xnrTOu95N%2Fyc5x6LpeyXg5u3NFIPAnIgL%2BI1cEaO1a87lT7eluy3TceES46ZemcWvdyeOG9x8LsG4tjAxlJXlalzfwIEK6vZH16kb%2BmM%2BMF5z3Bic8ct6tdAib77hyfDXKx%2FvxOZPdofGdoGSG%2Fi6imP6J5gycuBCp5919QoaFMZkwbULCN69ov4WgFTgukLGOtGa%2BUuhH9UHK1fWbzl2mb5GmTUE63kdvpJVTZhnAAy8rYG3rixpSbDnxFYwYXMoujPeRw59hGNV6rM5NPViHbOzkJWwTAYMTHHaWKxHZGuTo8mjdxA9kjC4sMAfB%2Bx5JYk%2FOfdDpIkrD1w30Gidaqx9j1TqvI6CuRQ2sQaXQer0zCaxqLUBjqkAaKwVj6xYqvZsNdr9b3cOJu5RppQ0tr0sy8vwbhllbLHmpqBL%2F4IVNFIUyvjgpDEtCAIeL8u7mP1JQoapSbaWeEUDK9DIBB1805C3OIIQTl3bFr%2BolCVH8zRC%2B470ldOfcAULNHdxi5%2FZWMqZOv9XKBfo2FZ%2B3mAFcyZEpLLVfBQru5yJMaIyuWq8ySLKne%2Fl3dnTmYM1IlvY7T3vxfWnctya8Wi&X-Amz-Signature=e47fdd36c568eb026e95ec1777afa9a441fd476129777f50f8653faaa036d18b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0dc06af9-28a6-42d2-859b-c4683d5fdb0d/2024-02-16_00-02.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667IIIQRKY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204700Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCEVsusSrqlRsDDl1RhNNQDYgsvxFCaSD4kquzCTekkDgIhANfsWXRLZEieNgf7VN7apJw5wmShox0ful4X4%2FuQKY9rKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzJ60pXaeVvW11rMQEq3APCQQH5E6QfEe5NYO34G0%2B444AJ5it4Fo9mrv%2BbRsBrRVaFIoTtbQXsFQC0jvIEeZwmMa11N5HIL9A65QLhXP8Pql28c2gBs0tM4%2FBb3M1u%2BMw%2BxCvph4rYodZ9ql8LeTeRg7e4%2BYae7dmuPxB1CAEH4ihlHVUmpTHMFeeZm1W9ICq93Lwi6AlIt4J%2BzP0qlytFZw9FwUooeub7DJ2aX5NYriLoUjo9Z5kBDaE0Vk%2BWbPHstSODW4eVbGYTYZD17WSvQUfKslGBP4R8xnrTOu95N%2Fyc5x6LpeyXg5u3NFIPAnIgL%2BI1cEaO1a87lT7eluy3TceES46ZemcWvdyeOG9x8LsG4tjAxlJXlalzfwIEK6vZH16kb%2BmM%2BMF5z3Bic8ct6tdAib77hyfDXKx%2FvxOZPdofGdoGSG%2Fi6imP6J5gycuBCp5919QoaFMZkwbULCN69ov4WgFTgukLGOtGa%2BUuhH9UHK1fWbzl2mb5GmTUE63kdvpJVTZhnAAy8rYG3rixpSbDnxFYwYXMoujPeRw59hGNV6rM5NPViHbOzkJWwTAYMTHHaWKxHZGuTo8mjdxA9kjC4sMAfB%2Bx5JYk%2FOfdDpIkrD1w30Gidaqx9j1TqvI6CuRQ2sQaXQer0zCaxqLUBjqkAaKwVj6xYqvZsNdr9b3cOJu5RppQ0tr0sy8vwbhllbLHmpqBL%2F4IVNFIUyvjgpDEtCAIeL8u7mP1JQoapSbaWeEUDK9DIBB1805C3OIIQTl3bFr%2BolCVH8zRC%2B470ldOfcAULNHdxi5%2FZWMqZOv9XKBfo2FZ%2B3mAFcyZEpLLVfBQru5yJMaIyuWq8ySLKne%2Fl3dnTmYM1IlvY7T3vxfWnctya8Wi&X-Amz-Signature=87886bc2ac1e1ee342208a2efe1706d5b362322d466e3960af3db9c7a8824b4e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Therefore A valid filename for the path traversal for `../../../etc/passwd`is  `%252e%252e%252f%252e%252e%252f%252e%252e%252fetc/passwd`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3aef0c4f-c3b5-4921-8807-cc7e2eb3d2e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667IIIQRKY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204700Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCEVsusSrqlRsDDl1RhNNQDYgsvxFCaSD4kquzCTekkDgIhANfsWXRLZEieNgf7VN7apJw5wmShox0ful4X4%2FuQKY9rKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzJ60pXaeVvW11rMQEq3APCQQH5E6QfEe5NYO34G0%2B444AJ5it4Fo9mrv%2BbRsBrRVaFIoTtbQXsFQC0jvIEeZwmMa11N5HIL9A65QLhXP8Pql28c2gBs0tM4%2FBb3M1u%2BMw%2BxCvph4rYodZ9ql8LeTeRg7e4%2BYae7dmuPxB1CAEH4ihlHVUmpTHMFeeZm1W9ICq93Lwi6AlIt4J%2BzP0qlytFZw9FwUooeub7DJ2aX5NYriLoUjo9Z5kBDaE0Vk%2BWbPHstSODW4eVbGYTYZD17WSvQUfKslGBP4R8xnrTOu95N%2Fyc5x6LpeyXg5u3NFIPAnIgL%2BI1cEaO1a87lT7eluy3TceES46ZemcWvdyeOG9x8LsG4tjAxlJXlalzfwIEK6vZH16kb%2BmM%2BMF5z3Bic8ct6tdAib77hyfDXKx%2FvxOZPdofGdoGSG%2Fi6imP6J5gycuBCp5919QoaFMZkwbULCN69ov4WgFTgukLGOtGa%2BUuhH9UHK1fWbzl2mb5GmTUE63kdvpJVTZhnAAy8rYG3rixpSbDnxFYwYXMoujPeRw59hGNV6rM5NPViHbOzkJWwTAYMTHHaWKxHZGuTo8mjdxA9kjC4sMAfB%2Bx5JYk%2FOfdDpIkrD1w30Gidaqx9j1TqvI6CuRQ2sQaXQer0zCaxqLUBjqkAaKwVj6xYqvZsNdr9b3cOJu5RppQ0tr0sy8vwbhllbLHmpqBL%2F4IVNFIUyvjgpDEtCAIeL8u7mP1JQoapSbaWeEUDK9DIBB1805C3OIIQTl3bFr%2BolCVH8zRC%2B470ldOfcAULNHdxi5%2FZWMqZOv9XKBfo2FZ%2B3mAFcyZEpLLVfBQru5yJMaIyuWq8ySLKne%2Fl3dnTmYM1IlvY7T3vxfWnctya8Wi&X-Amz-Signature=afcb0b89ac46b063256c6b01836dd96b50af23818cf1b9d9c0ffa0f1f9e621be&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### An alternative payload

Of course, when using Burp Repeater it is much easier to just type the `../../../` part in, than select it and `right-click -> Convert Selection -> URL -> URL encode all characters` twice.

This also encodes the `2 5 e f` characters from the first conversion, leading to a filename of `%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66etc/passwd`, which is also perfectly fine here:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39cf9dee-255d-4d2e-8760-7c7459129acc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667IIIQRKY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204700Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCEVsusSrqlRsDDl1RhNNQDYgsvxFCaSD4kquzCTekkDgIhANfsWXRLZEieNgf7VN7apJw5wmShox0ful4X4%2FuQKY9rKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzJ60pXaeVvW11rMQEq3APCQQH5E6QfEe5NYO34G0%2B444AJ5it4Fo9mrv%2BbRsBrRVaFIoTtbQXsFQC0jvIEeZwmMa11N5HIL9A65QLhXP8Pql28c2gBs0tM4%2FBb3M1u%2BMw%2BxCvph4rYodZ9ql8LeTeRg7e4%2BYae7dmuPxB1CAEH4ihlHVUmpTHMFeeZm1W9ICq93Lwi6AlIt4J%2BzP0qlytFZw9FwUooeub7DJ2aX5NYriLoUjo9Z5kBDaE0Vk%2BWbPHstSODW4eVbGYTYZD17WSvQUfKslGBP4R8xnrTOu95N%2Fyc5x6LpeyXg5u3NFIPAnIgL%2BI1cEaO1a87lT7eluy3TceES46ZemcWvdyeOG9x8LsG4tjAxlJXlalzfwIEK6vZH16kb%2BmM%2BMF5z3Bic8ct6tdAib77hyfDXKx%2FvxOZPdofGdoGSG%2Fi6imP6J5gycuBCp5919QoaFMZkwbULCN69ov4WgFTgukLGOtGa%2BUuhH9UHK1fWbzl2mb5GmTUE63kdvpJVTZhnAAy8rYG3rixpSbDnxFYwYXMoujPeRw59hGNV6rM5NPViHbOzkJWwTAYMTHHaWKxHZGuTo8mjdxA9kjC4sMAfB%2Bx5JYk%2FOfdDpIkrD1w30Gidaqx9j1TqvI6CuRQ2sQaXQer0zCaxqLUBjqkAaKwVj6xYqvZsNdr9b3cOJu5RppQ0tr0sy8vwbhllbLHmpqBL%2F4IVNFIUyvjgpDEtCAIeL8u7mP1JQoapSbaWeEUDK9DIBB1805C3OIIQTl3bFr%2BolCVH8zRC%2B470ldOfcAULNHdxi5%2FZWMqZOv9XKBfo2FZ%2B3mAFcyZEpLLVfBQru5yJMaIyuWq8ySLKne%2Fl3dnTmYM1IlvY7T3vxfWnctya8Wi&X-Amz-Signature=6133665f6ac1956666cf6fbdb48ac5398097c9da51e2f7db3ddd292368446498&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

