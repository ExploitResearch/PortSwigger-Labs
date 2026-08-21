# Method-based access control can be circumvented

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator

### Analysis/Exploitation -

<details><summary>Summary</summary>

We can see this request with administrator user.

```text
POST /admin-roles HTTP/1.1
...
username=carlos&action=upgrade

```

```text

POST /admin-roles - HTTP/1.1   -->401 Unauthorized
GET /admin - HTTP/1.1   -->400 Missing parameter'username'
```

With non privileged user, we  get 401 Unauthorized error.

But we can bypass the error with another type of request instead of using POST.

```text
GET /admin-roles?username=wiener&action=upgrade HTTP/1.1 --> 302 Found
GET /admin --> 200 OK
```

</details>

familiarize yourself with the admin panel by logging in using the credentials `administrator:admin` 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3fea78d0-0b43-4ccf-a7b7-0409c6c0b92b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215521Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=0cc485b687d2fb4d9dcad80a2b2d627b023380984e8d8328e1054f66877461a8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Here, administrator can upgrade or downgrade a user.

When we try to upgrade a user:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bf966fe2-5feb-4e1c-a3a5-452eb29a929e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215521Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=6cc751bac50b6f5d21d3bfed472b44bb843d8c28fd3b371e2c323addd9d7aac5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**It’s sending a POST request to **`/admin-roles`**, and with the **`username`** and **`action`**.**

Now, let’s log out and login as user `wiener` to do vertical privilege escalation!

After login send any GET request to repeater and change the ** **location to** **`/admin-roles`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/db04fb1e-ff4c-44b9-9f91-323f66a393fd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215521Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=94c8deb1a836284548739bd29b54bc6861d2092a09c8ad3345d0cec84363d68c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As you can see, looks like we can access `/admin-roles` when we’re sending a GET request to `/admin-roles` without any parameters.

If we change it to POST method we  get 401 Unauthorized . **So we’re allowed to send a GET request to **`/admin-roles`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0d60d2ee-8640-49ac-b6b5-46faa4aa89f6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663SXZZWUN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215522Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGaiGDZlzUGbVe7APYBRVD3lP6HryjDYkz%2BqIFb3yiT4AiEA134UYih7wTSFV0gpm5OXs0u3FMjrwZFi9shYJGuHPBsqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGw8HS3UH4VDwFqNTCrcAwppnRvLoghVsUtlpmOQdZSWQuO3I5tyUdkw4%2FHbSIEv3cU2gq6EafJndkBrGYusEneFuEYBzoTTLsp9KzaUjrBht8DOYEXR4V5jRHTXKXd6Ql%2F3ZbNn7Hp209trfGR%2FJ0M4QScdbmz%2BtYXIBg%2BTHXW%2Bb5fLRSkGiEvOYvqUSYJnt5aNdTjTbNoNTKmPppkLGSwMBLQM%2BpouO0kdGCPNJp37HE6p7IvSZ7l5AjuLPNwKW%2BqMDdTiMCi9Hc%2BRWr7ynUylb6tHs6EhpBDAqMDXz5zULa96vtCsXGo5%2BWNfhBEARF6ZO0XJB5PRWowfDAZwOObKYo98WM9JK%2BdvfKmL3hxyfqrygJqOJcWz6pbUl96USiqRt7D6XV65NFzkjEw2d%2BBn9jqjdXg%2FLt7dDJKtCxNvQZ4AIZMwiSDFdScL2WteTp7rHLsb%2FxH48%2F4cbM8yWaDqEmAoC3u2h7qxpRcXra4QABGoAkkDueI7oswYqW1%2BBAOSsSEHBJ0gp803qwl2jijYrkfWAzkekEBHZZw2%2FTdWn9Vraot9tOW3%2FODlzYJXsTDfSH6GcMvJBjgQEbZd8iEa344KLAPEGjXBIT0iYXBjQXcf0DtirITvY%2FmPqKw3S9nT%2BRR1VoUjmltnMO6Eo9QGOqUBdS9YDLqCDHDS6R93%2FtzocJ6sYAAjPPbxhikQCvHblDfncmLbQK5MWZUS1G496uUyOE9UQdHrcWIPGUIZXA5wIwaWFSKEcS8KyRWoNYsoAfWg5wS%2FZrFqzzfbPbK0diKthawV1sefD%2FGmsoFMkBL7wSp3assfAPpU6Qd0jzr2a5pg%2FlNhwfVkuLGXpUDA2WJYbr2xGQI0qZOWLeQ6sgX7cZGi%2FHPl&X-Amz-Signature=6139862a4b167abeeb6609171a5c29c54acec0dc57f9702834fb05a7df1b18f4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**send a GET request to **`/admin-roles`**, with parameters: **`username=wiener&action=upgrade`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6012c499-f073-4ec4-873a-0494ba2fd88f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215521Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=9ffb2e8500518ddde60b8a8d0aea1fdfa3e67bc52bde5d18d01641ddbb998209&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
