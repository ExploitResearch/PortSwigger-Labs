# Authentication bypass via encryption oracle

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

The login form provides the option to stay logged in. If the option is set a `stay-logged-in` then After logged in, **a new cookie called **`stay-logged-in`** has been set.**

![](./images/1e8c624545c4_001.png)

The does not show anything else that appears interesting so After poking around the web site, I found something interesting:In all posts, users can leave comments.

### Posting a comment

**Let’s take a look at the HTML form:**

```html
<form action="/post/comment" method="POST" enctype="application/x-www-form-urlencoded">
	<input required type="hidden" name="csrf" value="xMBJcQT8l3tlo2jTAMnr78eLKCi1p7tG">
	<input required type="hidden" name="postId" value="3">
	<label>Comment:</label>
	<textarea required rows="12" cols="300" name="comment"></textarea>
		<label>Name:</label>
		<input required type="text" name="name">
		<label>Email:</label>
		<input required name="email">
		<label>Website:</label>
		<input pattern="(http:|https:).+" type="text" name="website">
	<button class="button" type="submit">Post Comment</button>
</form>
```

As you can see, only the website field is not required.

I play with some of the parameters and mix valid and invalid content for email and website.

The website parameter gets checked via client-side javascript which can be circumvented but does not lead to anything interesting.

It is a different story for the email parameter:

When we send a valid request, it’ll redirect user to `/post/comment/confirmation`.

![](./images/1e8c624545c4_002.png)

**When I send an invalid email address, **It sets a new cookie called `notification` with the value `5mDWKkbL2t7ui%2fRxrDKeHRx3bRdxaPBsjqHIfyT34sGQMxg8tmY8Q6fKLlhJTc4Z`.

![](./images/1e8c624545c4_003.png)

the error is not displayed in the immediate response to the `POST` request.I guessed that the `notification` cookie contains the error information that is converted to the error message in the subsequent `GET /post?postId=x` request. 

![](./images/1e8c624545c4_004.png)

The content of the cookie does not appear to be simply encoded as no decoding variant results in anything legible.One detail that jumps to attention about this cookie is that its content is very similar to the `stay-logged-in` cookie from above. Both appear to URL- and base64 encoded.

Send both requests `POST /post/comment` and the subsequent `GET /post?postId=x` to repeater  and for simplicity rename the tabs `encrypt` and `decrypt` respectively.

Replace the content of the `notification` cookie with the content of my `stay-logged-in` cookie:

![](./images/1e8c624545c4_005.png)

We successfully decrypted the `stay-logged-in` cookie value: `wiener:1671605400893`. (Format = username:timestamp).

To impersonate the administrator I need to obtain the encrypted string `administrator:1710099291617` to forge a `stay-logged-in` cookie for the administrative user.

Whatever content I put in the email field will get encrypted the same way as the `stay-logged-in` cookie. Go to the encrypt request and change the email parameter to `administrator:your-timestamp`.Send the request and then copy the new `notification` cookie from the response then decrypt it.                  

Unfortunately, the server adds a descriptive error message in front of it, in this case, `Invalid email address`

![](./images/1e8c624545c4_006.png)

First, let’s find how long is that string:It’s the 23-character "`Invalid email address: `"

In Decoder, URL-decode and Base64-decode the cookie. Then, we can remove those 23 characters.

![](./images/1e8c624545c4_007.png)

After Deleting 23 bytes Encode that.

![](./images/1e8c624545c4_008.png)

**Let’s copy that encoded output and paste it to the **`notification`** cookie!**

![](./images/1e8c624545c4_009.png)

an error message indicates that a block-based encryption algorithm is used and that the input length must be a multiple of 16. You need to pad the "`Invalid email address: `" prefix with enough bytes so that the number of bytes you will remove is a multiple of 16.

By now I know that I can remove a full block of the ciphertext without negatively affecting the following blocks. There are 7 bytes of the error message that are within the second block: `dress:` I cannot simply remove these 7 bytes from the second block as this violates the block integrity:
However, If I add another 9 bytes in front of my desired plaintext, then it will fill the second 16 bytes block completely and my plaintext starts at the beginning of the third block.                    

![](./images/1e8c624545c4_010.png)

Send `123456789administrator:1710099291617` as the email to encrypting method in Burp Repeater:

![](./images/1e8c624545c4_011.png)

send the cookie value to Decoder, URL- and base64-decode it and remove the first two blocks of the hex representation (32 bytes) then encode it.

![](./images/1e8c624545c4_012.png)

### Logging in

I use the cookie editor to change the `stay-logged-in` cookie in my browser:

It appears that the session also contains user information and takes precedence over the `stay-logged-in` cookie. I remove the session cookie completely and refresh the page:

![](./images/1e8c624545c4_013.png)

Now to the `Admin panel` to remove user `carlos` 
