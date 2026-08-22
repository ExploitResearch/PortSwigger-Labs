# JWT authentication bypass via jku header injection

## Goal - 

Forge a JWT that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

## Analysis/Exploitation -

**Login as user **`wiener`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1aaa703c-3df7-434a-b6f9-396a8e9cf1be/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S265YBKD%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222100Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC7kx6cMVsgms9XC4Y9%2FWUMeOLRfoLzygXZ6OAuE7GQRQIgLB3PXI4dSC1IXq%2FSBottF1hYpPfgkLWPwkZZQBHW%2FKwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBmtxNAHl0zzX6l8oCrcA5KJkgnzgc2o1i4AZ3gTR3gPTbrCxBbmCv0BR9ajaBpkWhv12qV0usLb1fiSXUO3j2iYRPUtQdCUjoBiX07P47qkZUp%2F%2BjaYufBs%2BC%2FFvRthATuhmBCYkONQqGQ0KtcYEHGgzSYw6aZYav%2Fh0S0CXvfiuVaao6NoN2XYpZL6WIt6HH5XNkEA67RAHhfbL0ZrIATYt%2BH%2BCeakkjsWxaTccymwoQ8MZxdvVwal4UvTxt4dkHS6D2KgzR4JUfgAJomaGdyHT%2FZjYOR0GCdTOXe5YiF4HerN7tzDvJeozUHnY%2FgJ%2FNO7oOaEJMkW2iqI460kFScWicyQ7pR7ej7yJgP3Fxt4br0JArGakUSPqHILwXZxbhooZ%2F0cV3O8WheUlnjHtG%2FL1RU4ofo%2FKM88KeZa4CIOa%2FHQqlx9leIVOJBz%2FvvUxKE8jCb10%2FiImSt87lJCuQB06joCgA2trQt8ehKDKRGoqUJbgqhBdFiUhCwnZ9hFZHaV0c0dneBsn%2FhRF%2BM8blqfv%2FODMiOw1ETsiQQPhTiwFbGYp6QcvQ2wJ%2Bv5XrDia4aBHeEsr2gRW%2FbqxLFhw7RJ4Mo6fqgtlWOr%2BtzR3r51kBXUuSPWin0BD41DWXDKWeiSf1vy9MSDDAlxMOyGo9QGOqUBRPcgbYknmddUjYWBgtLP7KhxKDyn8SmqfDrwe5dbQqFYtKa24%2F1Yw4aUA2shoenDjDWCu%2BrqEI2o0pudidxgngriw1KCwRm7q6DAcy9I29G0YrtP98oeBIMLnuJgUFGVoq918XVzDzEWk0zBYPjP71RU9nDG%2BRVtKuoy8KlnYkitRMXqbLAfUdbS9y0q2Z2LMNZ5no7%2BQx%2FYKG7ZBZnA%2BSPzwHVz&X-Amz-Signature=657e8497b5c56a1f915dde88f8901ace1b414c55f51bd47e195af5de8024316e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the header’s `alg`, it tells that **it’s using RS256(RSA + SHA-256) algorithm.**

**In the lab’s background, it said:**

> The server supports the jku(JWK Set URL) parameter in the JWT header. However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key.

### <span style="color: #337EA9">Upload a malicious JWK Set of </span><span style="color: #337EA9">**new generated RSA key pair:**</span>

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9b6e3d3c-9638-4f47-9d99-213faa330981/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S265YBKD%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222100Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC7kx6cMVsgms9XC4Y9%2FWUMeOLRfoLzygXZ6OAuE7GQRQIgLB3PXI4dSC1IXq%2FSBottF1hYpPfgkLWPwkZZQBHW%2FKwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBmtxNAHl0zzX6l8oCrcA5KJkgnzgc2o1i4AZ3gTR3gPTbrCxBbmCv0BR9ajaBpkWhv12qV0usLb1fiSXUO3j2iYRPUtQdCUjoBiX07P47qkZUp%2F%2BjaYufBs%2BC%2FFvRthATuhmBCYkONQqGQ0KtcYEHGgzSYw6aZYav%2Fh0S0CXvfiuVaao6NoN2XYpZL6WIt6HH5XNkEA67RAHhfbL0ZrIATYt%2BH%2BCeakkjsWxaTccymwoQ8MZxdvVwal4UvTxt4dkHS6D2KgzR4JUfgAJomaGdyHT%2FZjYOR0GCdTOXe5YiF4HerN7tzDvJeozUHnY%2FgJ%2FNO7oOaEJMkW2iqI460kFScWicyQ7pR7ej7yJgP3Fxt4br0JArGakUSPqHILwXZxbhooZ%2F0cV3O8WheUlnjHtG%2FL1RU4ofo%2FKM88KeZa4CIOa%2FHQqlx9leIVOJBz%2FvvUxKE8jCb10%2FiImSt87lJCuQB06joCgA2trQt8ehKDKRGoqUJbgqhBdFiUhCwnZ9hFZHaV0c0dneBsn%2FhRF%2BM8blqfv%2FODMiOw1ETsiQQPhTiwFbGYp6QcvQ2wJ%2Bv5XrDia4aBHeEsr2gRW%2FbqxLFhw7RJ4Mo6fqgtlWOr%2BtzR3r51kBXUuSPWin0BD41DWXDKWeiSf1vy9MSDDAlxMOyGo9QGOqUBRPcgbYknmddUjYWBgtLP7KhxKDyn8SmqfDrwe5dbQqFYtKa24%2F1Yw4aUA2shoenDjDWCu%2BrqEI2o0pudidxgngriw1KCwRm7q6DAcy9I29G0YrtP98oeBIMLnuJgUFGVoq918XVzDzEWk0zBYPjP71RU9nDG%2BRVtKuoy8KlnYkitRMXqbLAfUdbS9y0q2Z2LMNZ5no7%2BQx%2FYKG7ZBZnA%2BSPzwHVz&X-Amz-Signature=67e686ffffa93d99440919c7b692ddff0f3d604e057fe2a501f79ae998d0b7e6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5456a1c7-f4f1-4e85-84e7-0615d6492830/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S265YBKD%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222100Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC7kx6cMVsgms9XC4Y9%2FWUMeOLRfoLzygXZ6OAuE7GQRQIgLB3PXI4dSC1IXq%2FSBottF1hYpPfgkLWPwkZZQBHW%2FKwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBmtxNAHl0zzX6l8oCrcA5KJkgnzgc2o1i4AZ3gTR3gPTbrCxBbmCv0BR9ajaBpkWhv12qV0usLb1fiSXUO3j2iYRPUtQdCUjoBiX07P47qkZUp%2F%2BjaYufBs%2BC%2FFvRthATuhmBCYkONQqGQ0KtcYEHGgzSYw6aZYav%2Fh0S0CXvfiuVaao6NoN2XYpZL6WIt6HH5XNkEA67RAHhfbL0ZrIATYt%2BH%2BCeakkjsWxaTccymwoQ8MZxdvVwal4UvTxt4dkHS6D2KgzR4JUfgAJomaGdyHT%2FZjYOR0GCdTOXe5YiF4HerN7tzDvJeozUHnY%2FgJ%2FNO7oOaEJMkW2iqI460kFScWicyQ7pR7ej7yJgP3Fxt4br0JArGakUSPqHILwXZxbhooZ%2F0cV3O8WheUlnjHtG%2FL1RU4ofo%2FKM88KeZa4CIOa%2FHQqlx9leIVOJBz%2FvvUxKE8jCb10%2FiImSt87lJCuQB06joCgA2trQt8ehKDKRGoqUJbgqhBdFiUhCwnZ9hFZHaV0c0dneBsn%2FhRF%2BM8blqfv%2FODMiOw1ETsiQQPhTiwFbGYp6QcvQ2wJ%2Bv5XrDia4aBHeEsr2gRW%2FbqxLFhw7RJ4Mo6fqgtlWOr%2BtzR3r51kBXUuSPWin0BD41DWXDKWeiSf1vy9MSDDAlxMOyGo9QGOqUBRPcgbYknmddUjYWBgtLP7KhxKDyn8SmqfDrwe5dbQqFYtKa24%2F1Yw4aUA2shoenDjDWCu%2BrqEI2o0pudidxgngriw1KCwRm7q6DAcy9I29G0YrtP98oeBIMLnuJgUFGVoq918XVzDzEWk0zBYPjP71RU9nDG%2BRVtKuoy8KlnYkitRMXqbLAfUdbS9y0q2Z2LMNZ5no7%2BQx%2FYKG7ZBZnA%2BSPzwHVz&X-Amz-Signature=ad05d33fd4e65a0d2b87d605bf4bc9d6571d13665f9180dbd81bc5cdefa1e691&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Copy the new generated Public Key as JWK and paste in Body** **section of exploit server** into the `keys` array of JWK Set as follows:                  

```perl
{
    "keys": [
    <<PASTE PUBLIC key as JWK>>
    ]
}
```

**then **`Store`** in the exploit server:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e482895f-d5af-4140-b83e-255746344cf3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S265YBKD%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222100Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC7kx6cMVsgms9XC4Y9%2FWUMeOLRfoLzygXZ6OAuE7GQRQIgLB3PXI4dSC1IXq%2FSBottF1hYpPfgkLWPwkZZQBHW%2FKwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBmtxNAHl0zzX6l8oCrcA5KJkgnzgc2o1i4AZ3gTR3gPTbrCxBbmCv0BR9ajaBpkWhv12qV0usLb1fiSXUO3j2iYRPUtQdCUjoBiX07P47qkZUp%2F%2BjaYufBs%2BC%2FFvRthATuhmBCYkONQqGQ0KtcYEHGgzSYw6aZYav%2Fh0S0CXvfiuVaao6NoN2XYpZL6WIt6HH5XNkEA67RAHhfbL0ZrIATYt%2BH%2BCeakkjsWxaTccymwoQ8MZxdvVwal4UvTxt4dkHS6D2KgzR4JUfgAJomaGdyHT%2FZjYOR0GCdTOXe5YiF4HerN7tzDvJeozUHnY%2FgJ%2FNO7oOaEJMkW2iqI460kFScWicyQ7pR7ej7yJgP3Fxt4br0JArGakUSPqHILwXZxbhooZ%2F0cV3O8WheUlnjHtG%2FL1RU4ofo%2FKM88KeZa4CIOa%2FHQqlx9leIVOJBz%2FvvUxKE8jCb10%2FiImSt87lJCuQB06joCgA2trQt8ehKDKRGoqUJbgqhBdFiUhCwnZ9hFZHaV0c0dneBsn%2FhRF%2BM8blqfv%2FODMiOw1ETsiQQPhTiwFbGYp6QcvQ2wJ%2Bv5XrDia4aBHeEsr2gRW%2FbqxLFhw7RJ4Mo6fqgtlWOr%2BtzR3r51kBXUuSPWin0BD41DWXDKWeiSf1vy9MSDDAlxMOyGo9QGOqUBRPcgbYknmddUjYWBgtLP7KhxKDyn8SmqfDrwe5dbQqFYtKa24%2F1Yw4aUA2shoenDjDWCu%2BrqEI2o0pudidxgngriw1KCwRm7q6DAcy9I29G0YrtP98oeBIMLnuJgUFGVoq918XVzDzEWk0zBYPjP71RU9nDG%2BRVtKuoy8KlnYkitRMXqbLAfUdbS9y0q2Z2LMNZ5no7%2BQx%2FYKG7ZBZnA%2BSPzwHVz&X-Amz-Signature=1a15fc33c51970bd0798d30a20dce467138fa50606dcc78f833a1e1cf04f6f60&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### <span style="color: #337EA9">Modify and sign the JWT</span>

Send the post-login `GET /my-account?id=wiener` request to Burp Repeater, then remove id parameter    

- In the header of the JWT, replace the current value of the `kid` parameter with the `kid` of the JWK that you uploaded to the exploit server.
Add a new `jku` parameter to the header of the JWT. Set its value to the URL of your JWK Set on the exploit server.

> 💡 Remember all parameter end with comma , except last one

- In the payload, change the value of the `sub` claim to `administrator`.
- At the bottom of the tab, click **Sign**, then select the RSA key that you generated. Make sure that the **Don't modify header** option is selected, then click **OK**.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fc076ff1-8f65-4dd0-9bc7-4b2f0b767ac3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S265YBKD%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222100Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC7kx6cMVsgms9XC4Y9%2FWUMeOLRfoLzygXZ6OAuE7GQRQIgLB3PXI4dSC1IXq%2FSBottF1hYpPfgkLWPwkZZQBHW%2FKwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDBmtxNAHl0zzX6l8oCrcA5KJkgnzgc2o1i4AZ3gTR3gPTbrCxBbmCv0BR9ajaBpkWhv12qV0usLb1fiSXUO3j2iYRPUtQdCUjoBiX07P47qkZUp%2F%2BjaYufBs%2BC%2FFvRthATuhmBCYkONQqGQ0KtcYEHGgzSYw6aZYav%2Fh0S0CXvfiuVaao6NoN2XYpZL6WIt6HH5XNkEA67RAHhfbL0ZrIATYt%2BH%2BCeakkjsWxaTccymwoQ8MZxdvVwal4UvTxt4dkHS6D2KgzR4JUfgAJomaGdyHT%2FZjYOR0GCdTOXe5YiF4HerN7tzDvJeozUHnY%2FgJ%2FNO7oOaEJMkW2iqI460kFScWicyQ7pR7ej7yJgP3Fxt4br0JArGakUSPqHILwXZxbhooZ%2F0cV3O8WheUlnjHtG%2FL1RU4ofo%2FKM88KeZa4CIOa%2FHQqlx9leIVOJBz%2FvvUxKE8jCb10%2FiImSt87lJCuQB06joCgA2trQt8ehKDKRGoqUJbgqhBdFiUhCwnZ9hFZHaV0c0dneBsn%2FhRF%2BM8blqfv%2FODMiOw1ETsiQQPhTiwFbGYp6QcvQ2wJ%2Bv5XrDia4aBHeEsr2gRW%2FbqxLFhw7RJ4Mo6fqgtlWOr%2BtzR3r51kBXUuSPWin0BD41DWXDKWeiSf1vy9MSDDAlxMOyGo9QGOqUBRPcgbYknmddUjYWBgtLP7KhxKDyn8SmqfDrwe5dbQqFYtKa24%2F1Yw4aUA2shoenDjDWCu%2BrqEI2o0pudidxgngriw1KCwRm7q6DAcy9I29G0YrtP98oeBIMLnuJgUFGVoq918XVzDzEWk0zBYPjP71RU9nDG%2BRVtKuoy8KlnYkitRMXqbLAfUdbS9y0q2Z2LMNZ5no7%2BQx%2FYKG7ZBZnA%2BSPzwHVz&X-Amz-Signature=c0f176be01bc18d4fb4fa8d67987f271e3dd174841fe0d9b9fbd1ab60a46d679&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Copy the JWT and update session cookie in the browser**, then refresh the page:**

go to the admin panel and delete user `carlos`
