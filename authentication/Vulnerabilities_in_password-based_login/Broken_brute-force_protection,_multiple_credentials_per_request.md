# Broken brute-force protection, multiple credentials per request

## Edit in VScode text file

- With Burp running, investigate the login page. Notice that the `POST /login` request submits the login credentials in `JSON` format. Send this request to Burp Repeater.
- In Burp Repeater, replace the single string value of the password with an array of strings containing all of the candidate passwords. For example: `"username" : "carlos",
"password" : [ "123456", "password", "qwerty" ...
]`
- Send the request. This will return a 302 response.
- Right-click on this request and select **Show response in browser**. Copy the URL and load it in the browser. The page loads and you are logged in as `carlos`.
- Click **My account** to access Carlos's account page and solve the lab.

![](https://i.stack.imgur.com/kXJrl.gif)

Here is an easy way to do this:

1. Ctrl+A to select all or select your desired text.
1. Shift+Alt+I to put a cursor at the end of each line.
1. Type your ' (or whatever you want at the end).
1. Home will move all your cursors to the beginning of the lines.
1. Type your ' (or whatever you want at the beginning of all the lines).
