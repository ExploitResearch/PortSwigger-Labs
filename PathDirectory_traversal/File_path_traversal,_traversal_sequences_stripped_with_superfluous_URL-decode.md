# File path traversal, traversal sequences stripped with superfluous URL-decode

### Goal - 

Retrieve the contents of the `/etc/passwd` file.

### Analysis/Exploitation 

open any product or open any image in new tab

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/475ced47-f148-41c1-8ec6-0c1c5e097f33/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SZYFW6HN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221935Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDuk8ymsoAzgsPqnYzeCYtnnhYC5Us8AFjqwqeGEebi2QIgEMMdM3hdAG%2FIDcYapOenlbzDk3smPchRNSbHoB9bkVMqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBBzzuu72wthJbruKSrcAymwaY8q0KUZ0w3MKr4ypw3Qj6jnPZr47Db%2BBwFY0KFDdTxoow2sukrl4FM2WZlWhPY2ki89DP6R8I1KmXB%2BuuR%2Fv054cEybKks95YecQyVc0oQ9Qd2nHxcL5gyBWYhSU4drVCgtN6Gk69lIXn3TsFXEFtvS7jPXhBaLieMaOH3Vk8wFRUA0WsuBSZdb9ujthCAa2AeD%2B0%2BzYjyKFN%2B2vAmDqeo%2FeJuvnS8u2wTHlOkhumUnVbahEclm%2BwQ6rsTb9Qn3MdfkpH5bULI6bKgBRj%2FBm8TVWoW2V0HC6aJg0rICtYikhPxU%2BU8sn0A4XDzf4z%2BOiTMuXvRdOQvSLablzq4UroHJs7dJFTuQkpDLR4KicAxZArMyYlTrg8bUkP85CZdfQrLvzZnDYaqnfkWt7Ou9DYurw%2BVGf8ikFyXXHvC9FaZmvVaqHHUK0f%2Bwd%2BYTBLSbu5wsyCz%2F6I9068IuJalIj0lQ%2FPIuWnGdLdgZ2i8ibwBe0yJ3cwgRWOecGKV8SMK9JYsl0BzZYtLWf9%2FDDmA6ZZfwV39epJnlTtCUvE7%2FPfOyM%2F%2FBNIXbdkjUPlMa5APMOUT%2BhKEHWM9yEZJPLo1pURGNcxPaAvtYt9SJ0xQj5%2BJ0DgNAuTs3n07cMPaDo9QGOqUB60HGgjGIm%2BuMp%2FHY%2BPTc9%2BO970WJoV1piThwzTjbiKdFMkXu5S8gzMiruQn6mapyGUuHynBzf2PzCaIe7dmoZ%2FCy0GU4Citalivzjb1wkT6DjdFQjFWIkOBy%2FMcELlkMWJ61of7zfsGYEVy5iHPS1HYHP2TMFMQQSU92RkkwOKFhkyxh%2BPcaqiKfrD9%2BjWN%2BFXLhTZsPGdHJO8%2BZYv3nY84lbmde&X-Amz-Signature=fe0aae3acb6561fd58cf4c55db73685b86f65068765d98407ac56ef3e0a18601&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

apply above filter to see image request and sent it to repeater

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/be73ff94-1b0b-4941-90e1-fefafce76325/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SZYFW6HN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221935Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDuk8ymsoAzgsPqnYzeCYtnnhYC5Us8AFjqwqeGEebi2QIgEMMdM3hdAG%2FIDcYapOenlbzDk3smPchRNSbHoB9bkVMqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBBzzuu72wthJbruKSrcAymwaY8q0KUZ0w3MKr4ypw3Qj6jnPZr47Db%2BBwFY0KFDdTxoow2sukrl4FM2WZlWhPY2ki89DP6R8I1KmXB%2BuuR%2Fv054cEybKks95YecQyVc0oQ9Qd2nHxcL5gyBWYhSU4drVCgtN6Gk69lIXn3TsFXEFtvS7jPXhBaLieMaOH3Vk8wFRUA0WsuBSZdb9ujthCAa2AeD%2B0%2BzYjyKFN%2B2vAmDqeo%2FeJuvnS8u2wTHlOkhumUnVbahEclm%2BwQ6rsTb9Qn3MdfkpH5bULI6bKgBRj%2FBm8TVWoW2V0HC6aJg0rICtYikhPxU%2BU8sn0A4XDzf4z%2BOiTMuXvRdOQvSLablzq4UroHJs7dJFTuQkpDLR4KicAxZArMyYlTrg8bUkP85CZdfQrLvzZnDYaqnfkWt7Ou9DYurw%2BVGf8ikFyXXHvC9FaZmvVaqHHUK0f%2Bwd%2BYTBLSbu5wsyCz%2F6I9068IuJalIj0lQ%2FPIuWnGdLdgZ2i8ibwBe0yJ3cwgRWOecGKV8SMK9JYsl0BzZYtLWf9%2FDDmA6ZZfwV39epJnlTtCUvE7%2FPfOyM%2F%2FBNIXbdkjUPlMa5APMOUT%2BhKEHWM9yEZJPLo1pURGNcxPaAvtYt9SJ0xQj5%2BJ0DgNAuTs3n07cMPaDo9QGOqUB60HGgjGIm%2BuMp%2FHY%2BPTc9%2BO970WJoV1piThwzTjbiKdFMkXu5S8gzMiruQn6mapyGUuHynBzf2PzCaIe7dmoZ%2FCy0GU4Citalivzjb1wkT6DjdFQjFWIkOBy%2FMcELlkMWJ61of7zfsGYEVy5iHPS1HYHP2TMFMQQSU92RkkwOKFhkyxh%2BPcaqiKfrD9%2BjWN%2BFXLhTZsPGdHJO8%2BZYv3nY84lbmde&X-Amz-Signature=973bb8f61dfc0e67a268b7302e192c68b45c30764620466c357ee38bddb2ce33&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0dc06af9-28a6-42d2-859b-c4683d5fdb0d/2024-02-16_00-02.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SZYFW6HN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221935Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDuk8ymsoAzgsPqnYzeCYtnnhYC5Us8AFjqwqeGEebi2QIgEMMdM3hdAG%2FIDcYapOenlbzDk3smPchRNSbHoB9bkVMqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBBzzuu72wthJbruKSrcAymwaY8q0KUZ0w3MKr4ypw3Qj6jnPZr47Db%2BBwFY0KFDdTxoow2sukrl4FM2WZlWhPY2ki89DP6R8I1KmXB%2BuuR%2Fv054cEybKks95YecQyVc0oQ9Qd2nHxcL5gyBWYhSU4drVCgtN6Gk69lIXn3TsFXEFtvS7jPXhBaLieMaOH3Vk8wFRUA0WsuBSZdb9ujthCAa2AeD%2B0%2BzYjyKFN%2B2vAmDqeo%2FeJuvnS8u2wTHlOkhumUnVbahEclm%2BwQ6rsTb9Qn3MdfkpH5bULI6bKgBRj%2FBm8TVWoW2V0HC6aJg0rICtYikhPxU%2BU8sn0A4XDzf4z%2BOiTMuXvRdOQvSLablzq4UroHJs7dJFTuQkpDLR4KicAxZArMyYlTrg8bUkP85CZdfQrLvzZnDYaqnfkWt7Ou9DYurw%2BVGf8ikFyXXHvC9FaZmvVaqHHUK0f%2Bwd%2BYTBLSbu5wsyCz%2F6I9068IuJalIj0lQ%2FPIuWnGdLdgZ2i8ibwBe0yJ3cwgRWOecGKV8SMK9JYsl0BzZYtLWf9%2FDDmA6ZZfwV39epJnlTtCUvE7%2FPfOyM%2F%2FBNIXbdkjUPlMa5APMOUT%2BhKEHWM9yEZJPLo1pURGNcxPaAvtYt9SJ0xQj5%2BJ0DgNAuTs3n07cMPaDo9QGOqUB60HGgjGIm%2BuMp%2FHY%2BPTc9%2BO970WJoV1piThwzTjbiKdFMkXu5S8gzMiruQn6mapyGUuHynBzf2PzCaIe7dmoZ%2FCy0GU4Citalivzjb1wkT6DjdFQjFWIkOBy%2FMcELlkMWJ61of7zfsGYEVy5iHPS1HYHP2TMFMQQSU92RkkwOKFhkyxh%2BPcaqiKfrD9%2BjWN%2BFXLhTZsPGdHJO8%2BZYv3nY84lbmde&X-Amz-Signature=df2c7f260f915d663aae7bba1009d00964d7cb2fc405b67f22331c8bae467824&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Therefore A valid filename for the path traversal for `../../../etc/passwd`is  `%252e%252e%252f%252e%252e%252f%252e%252e%252fetc/passwd`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3aef0c4f-c3b5-4921-8807-cc7e2eb3d2e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SZYFW6HN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221935Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDuk8ymsoAzgsPqnYzeCYtnnhYC5Us8AFjqwqeGEebi2QIgEMMdM3hdAG%2FIDcYapOenlbzDk3smPchRNSbHoB9bkVMqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBBzzuu72wthJbruKSrcAymwaY8q0KUZ0w3MKr4ypw3Qj6jnPZr47Db%2BBwFY0KFDdTxoow2sukrl4FM2WZlWhPY2ki89DP6R8I1KmXB%2BuuR%2Fv054cEybKks95YecQyVc0oQ9Qd2nHxcL5gyBWYhSU4drVCgtN6Gk69lIXn3TsFXEFtvS7jPXhBaLieMaOH3Vk8wFRUA0WsuBSZdb9ujthCAa2AeD%2B0%2BzYjyKFN%2B2vAmDqeo%2FeJuvnS8u2wTHlOkhumUnVbahEclm%2BwQ6rsTb9Qn3MdfkpH5bULI6bKgBRj%2FBm8TVWoW2V0HC6aJg0rICtYikhPxU%2BU8sn0A4XDzf4z%2BOiTMuXvRdOQvSLablzq4UroHJs7dJFTuQkpDLR4KicAxZArMyYlTrg8bUkP85CZdfQrLvzZnDYaqnfkWt7Ou9DYurw%2BVGf8ikFyXXHvC9FaZmvVaqHHUK0f%2Bwd%2BYTBLSbu5wsyCz%2F6I9068IuJalIj0lQ%2FPIuWnGdLdgZ2i8ibwBe0yJ3cwgRWOecGKV8SMK9JYsl0BzZYtLWf9%2FDDmA6ZZfwV39epJnlTtCUvE7%2FPfOyM%2F%2FBNIXbdkjUPlMa5APMOUT%2BhKEHWM9yEZJPLo1pURGNcxPaAvtYt9SJ0xQj5%2BJ0DgNAuTs3n07cMPaDo9QGOqUB60HGgjGIm%2BuMp%2FHY%2BPTc9%2BO970WJoV1piThwzTjbiKdFMkXu5S8gzMiruQn6mapyGUuHynBzf2PzCaIe7dmoZ%2FCy0GU4Citalivzjb1wkT6DjdFQjFWIkOBy%2FMcELlkMWJ61of7zfsGYEVy5iHPS1HYHP2TMFMQQSU92RkkwOKFhkyxh%2BPcaqiKfrD9%2BjWN%2BFXLhTZsPGdHJO8%2BZYv3nY84lbmde&X-Amz-Signature=f9723388af5f34d529e152539efffc28b5ff688918adf7ca8af57dc85c77417e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### An alternative payload

Of course, when using Burp Repeater it is much easier to just type the `../../../` part in, than select it and `right-click -> Convert Selection -> URL -> URL encode all characters` twice.

This also encodes the `2 5 e f` characters from the first conversion, leading to a filename of `%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66%25%32%65%25%32%65%25%32%66etc/passwd`, which is also perfectly fine here:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39cf9dee-255d-4d2e-8760-7c7459129acc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SZYFW6HN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221935Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDuk8ymsoAzgsPqnYzeCYtnnhYC5Us8AFjqwqeGEebi2QIgEMMdM3hdAG%2FIDcYapOenlbzDk3smPchRNSbHoB9bkVMqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBBzzuu72wthJbruKSrcAymwaY8q0KUZ0w3MKr4ypw3Qj6jnPZr47Db%2BBwFY0KFDdTxoow2sukrl4FM2WZlWhPY2ki89DP6R8I1KmXB%2BuuR%2Fv054cEybKks95YecQyVc0oQ9Qd2nHxcL5gyBWYhSU4drVCgtN6Gk69lIXn3TsFXEFtvS7jPXhBaLieMaOH3Vk8wFRUA0WsuBSZdb9ujthCAa2AeD%2B0%2BzYjyKFN%2B2vAmDqeo%2FeJuvnS8u2wTHlOkhumUnVbahEclm%2BwQ6rsTb9Qn3MdfkpH5bULI6bKgBRj%2FBm8TVWoW2V0HC6aJg0rICtYikhPxU%2BU8sn0A4XDzf4z%2BOiTMuXvRdOQvSLablzq4UroHJs7dJFTuQkpDLR4KicAxZArMyYlTrg8bUkP85CZdfQrLvzZnDYaqnfkWt7Ou9DYurw%2BVGf8ikFyXXHvC9FaZmvVaqHHUK0f%2Bwd%2BYTBLSbu5wsyCz%2F6I9068IuJalIj0lQ%2FPIuWnGdLdgZ2i8ibwBe0yJ3cwgRWOecGKV8SMK9JYsl0BzZYtLWf9%2FDDmA6ZZfwV39epJnlTtCUvE7%2FPfOyM%2F%2FBNIXbdkjUPlMa5APMOUT%2BhKEHWM9yEZJPLo1pURGNcxPaAvtYt9SJ0xQj5%2BJ0DgNAuTs3n07cMPaDo9QGOqUB60HGgjGIm%2BuMp%2FHY%2BPTc9%2BO970WJoV1piThwzTjbiKdFMkXu5S8gzMiruQn6mapyGUuHynBzf2PzCaIe7dmoZ%2FCy0GU4Citalivzjb1wkT6DjdFQjFWIkOBy%2FMcELlkMWJ61of7zfsGYEVy5iHPS1HYHP2TMFMQQSU92RkkwOKFhkyxh%2BPcaqiKfrD9%2BjWN%2BFXLhTZsPGdHJO8%2BZYv3nY84lbmde&X-Amz-Signature=9cb4627da824799fba180099f72fd503f7a45b816017d581decdc56e31da1592&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
