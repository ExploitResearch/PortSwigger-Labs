# Broken brute-force protection, multiple credentials per request

## Edit in VScode text file

- With Burp running, investigate the login page. Notice that the `POST /login` request submits the login credentials in `JSON` format. Send this request to Burp Repeater.
- In Burp Repeater, replace the single string value of the password with an array of strings containing all of the candidate passwords. For example: `"username" : "carlos",
"password" : [ "123456", "password", "qwerty" ...
]`
- Send the request. This will return a 302 response.
- Right-click on this request and select **Show response in browser**. Copy the URL and load it in the browser. The page loads and you are logged in as `carlos`.
- Click **My account** to access Carlos's account page and solve the lab.

Here is an easy way to do this:

1. Ctrl+A to select all or select your desired text.
1. Shift+Alt+I to put a cursor at the end of each line.
1. Type your ' (or whatever you want at the end).
1. Home will move all your cursors to the beginning of the lines.
1. Type your ' (or whatever you want at the beginning of all the lines).

### Why It Works

The exploit succeeds because this lab is vulnerable due to a logic flaw in its brute-force protection. to solve the lab, brute-force carlos's password, then access his account page.

The official solution confirms: With Burp running, investigate the login page. Notice that the POST /login request submits the login credentials in JSON format. Send this request to 

The root cause is a failure in the application's security architecture specific to this authentication scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable due to a logic flaw in its brute-force protection. To solve the lab, brute-fo"
- Consistent error messages and rate-limiting prevent enumeration and brute-force.
