# OS command injection, simple case

### Goal - 

Exploit command injection to execute whoami command.

### Analysis/Exploitation 

As usual, the first step is to browse around a bit. Upon viewing view details of an product we get detail information about that product and we can see upon visiting a specific product a parameter named **productId **is being set. Well this is where we can try to preform command injection and i did but no luck because it fetches information by using an API which restrict all special characters. But as there is another functionality which allows us check for availability of stocks.

Let’s click the `Check stock` button, and intercept the request via Burp Suite

When we clicked that button, it’ll send a POST request to `/product/stock`, with parameter `productId=1` and `storeId=1`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/57677f51-8e40-4a70-bab1-35d5591b4927/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WFQDKFMF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204714Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID%2BsKeRyn3ETW5dSWTONVsdcENkTReXUQKDzRn15s4Y9AiBO66x0FlgQIY3WyNYMeWQLK59c1dFUVZcEPWZfrksQKiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMetyTI4BemyVWljmkKtwDHb3zEWv0MJngTVQF6%2FqyShaT5%2BzCnJeddRrUlgdaR5FaYmPTd65FVH274JA8QdatzGssamTW6TFHcDOxjOKeH8ZLr%2BXAu7%2F5gh4%2FWI5tvGaVJyMg3SxLAhYuMBQfdXpL2t3nJK%2BzzfyTw0DwGe6l3c5yUDm6AGv6fUbjnkXIweC8E2aiJZrlrtm%2FPjVJp0PL%2BGBRqOBujI%2Bly9oI%2BFKMI00HmUafGyivk9CzCrEMP2dXeAqNPsVWvwgisEDWZu8ZtRJkhrGUW9WJDlajhRxU2CuPxmEDVahZur7NeYLqbcPRf3sECkaVwtpawFcHFFSWmai14ZJmiX%2FkV5IGvQsWyookXSEqWe6gbDYNbcXwEQT9U3UDp0gbu3IpecB6N1mk9uSYar9Rx95d4eWSXjuyi2V9IbEPVSSzha%2BFZViOxLBh6lzmeZ1h%2BlCF9hkJjprFx0n0QQb1ost%2BNZEmhwCfZP%2FXvdiGQqLaPCRLOoHZumr1xsh%2FvjAd4WWTh20hzgI2nM4tkwpAcm8g6mxcZOXOT1qaoMc1Fp5X8QDHwvab0a4d17x2ZepkiFjkM%2FgsG92Phy%2FFMPszHbsEklcnCCL1ztm6NmKCYLIGpcN16f5SKt%2FvZvYDQ0475M3NE80w5Mii1AY6pgHuUUeZ7WIwsd6wYZI%2FgWWvD6xLpOPKfPnMxUHgQ%2FjIp5pQQweA40QAMntbRwx1aH1anIotXkPVo1gLOsACRA6RzRZB5mV%2FbWVYOvv%2BkXZmRS05A9OubzaYJ6YXVO%2Bbd0Ln3dMiCHfcdypDP2XAZzRCTeGhc8yBxxj6Y4yf7%2FTBTHenBzgdunN%2Boemm3JIBzOjU%2FA71v%2F5g6NPMIilonRiZsztOgR2a&X-Amz-Signature=5284329dbb848674998fa376c56e88b78dc89aac93256be0c748fa8365a6f180&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As we have two parameters, I try to inject both with different commands. This way, I can find out which parameter is injectable and in which order they are executed.

> 💡 The script call might look something like this (likely not the exact syntax, but the general idea is the same):

```bash
echo system("someScript.sh $_REQUEST['productID'] $_REQUEST['storeId']")
```

In this case, the parameters are used as arguments for the script and the output is directly echoed back into the HTML.

There are multiple ways to execute multiple commands in one line in a shell, separating the individual commands with for example `&`, `&&`, `|`, `||`, `;`. All behave slightly differently. On Unix systems, my favorite is `;` as it completely separates the commands without side effects based on return conditions or execution order. In some conditions `&` is better as it backgrounds the command before my injection and runs my code without waiting for the other command to finish. Still, my favourite remains `;`.

**NOTE :**** when using **`&`**, it must be URLencoded**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/abae6bdd-003c-43b0-a3dc-7da788ecab25/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WFQDKFMF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204714Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID%2BsKeRyn3ETW5dSWTONVsdcENkTReXUQKDzRn15s4Y9AiBO66x0FlgQIY3WyNYMeWQLK59c1dFUVZcEPWZfrksQKiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMetyTI4BemyVWljmkKtwDHb3zEWv0MJngTVQF6%2FqyShaT5%2BzCnJeddRrUlgdaR5FaYmPTd65FVH274JA8QdatzGssamTW6TFHcDOxjOKeH8ZLr%2BXAu7%2F5gh4%2FWI5tvGaVJyMg3SxLAhYuMBQfdXpL2t3nJK%2BzzfyTw0DwGe6l3c5yUDm6AGv6fUbjnkXIweC8E2aiJZrlrtm%2FPjVJp0PL%2BGBRqOBujI%2Bly9oI%2BFKMI00HmUafGyivk9CzCrEMP2dXeAqNPsVWvwgisEDWZu8ZtRJkhrGUW9WJDlajhRxU2CuPxmEDVahZur7NeYLqbcPRf3sECkaVwtpawFcHFFSWmai14ZJmiX%2FkV5IGvQsWyookXSEqWe6gbDYNbcXwEQT9U3UDp0gbu3IpecB6N1mk9uSYar9Rx95d4eWSXjuyi2V9IbEPVSSzha%2BFZViOxLBh6lzmeZ1h%2BlCF9hkJjprFx0n0QQb1ost%2BNZEmhwCfZP%2FXvdiGQqLaPCRLOoHZumr1xsh%2FvjAd4WWTh20hzgI2nM4tkwpAcm8g6mxcZOXOT1qaoMc1Fp5X8QDHwvab0a4d17x2ZepkiFjkM%2FgsG92Phy%2FFMPszHbsEklcnCCL1ztm6NmKCYLIGpcN16f5SKt%2FvZvYDQ0475M3NE80w5Mii1AY6pgHuUUeZ7WIwsd6wYZI%2FgWWvD6xLpOPKfPnMxUHgQ%2FjIp5pQQweA40QAMntbRwx1aH1anIotXkPVo1gLOsACRA6RzRZB5mV%2FbWVYOvv%2BkXZmRS05A9OubzaYJ6YXVO%2Bbd0Ln3dMiCHfcdypDP2XAZzRCTeGhc8yBxxj6Y4yf7%2FTBTHenBzgdunN%2Boemm3JIBzOjU%2FA71v%2F5g6NPMIilonRiZsztOgR2a&X-Amz-Signature=c23a45d641c515bb4fc98537c24ee5212be3077a4b5da61e73ccdeb378b01bbd&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From the response, it can be seen that both parameters are injectable, and they are executed in the order productId first, storeId second.

**Let’s execute **`whoami`** command**

comment out the remainder of the line after the `whoami` to avoid the error message of the second parameter:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/922ea403-d4eb-47da-81af-f792b32ac69e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WFQDKFMF%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204714Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID%2BsKeRyn3ETW5dSWTONVsdcENkTReXUQKDzRn15s4Y9AiBO66x0FlgQIY3WyNYMeWQLK59c1dFUVZcEPWZfrksQKiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMetyTI4BemyVWljmkKtwDHb3zEWv0MJngTVQF6%2FqyShaT5%2BzCnJeddRrUlgdaR5FaYmPTd65FVH274JA8QdatzGssamTW6TFHcDOxjOKeH8ZLr%2BXAu7%2F5gh4%2FWI5tvGaVJyMg3SxLAhYuMBQfdXpL2t3nJK%2BzzfyTw0DwGe6l3c5yUDm6AGv6fUbjnkXIweC8E2aiJZrlrtm%2FPjVJp0PL%2BGBRqOBujI%2Bly9oI%2BFKMI00HmUafGyivk9CzCrEMP2dXeAqNPsVWvwgisEDWZu8ZtRJkhrGUW9WJDlajhRxU2CuPxmEDVahZur7NeYLqbcPRf3sECkaVwtpawFcHFFSWmai14ZJmiX%2FkV5IGvQsWyookXSEqWe6gbDYNbcXwEQT9U3UDp0gbu3IpecB6N1mk9uSYar9Rx95d4eWSXjuyi2V9IbEPVSSzha%2BFZViOxLBh6lzmeZ1h%2BlCF9hkJjprFx0n0QQb1ost%2BNZEmhwCfZP%2FXvdiGQqLaPCRLOoHZumr1xsh%2FvjAd4WWTh20hzgI2nM4tkwpAcm8g6mxcZOXOT1qaoMc1Fp5X8QDHwvab0a4d17x2ZepkiFjkM%2FgsG92Phy%2FFMPszHbsEklcnCCL1ztm6NmKCYLIGpcN16f5SKt%2FvZvYDQ0475M3NE80w5Mii1AY6pgHuUUeZ7WIwsd6wYZI%2FgWWvD6xLpOPKfPnMxUHgQ%2FjIp5pQQweA40QAMntbRwx1aH1anIotXkPVo1gLOsACRA6RzRZB5mV%2FbWVYOvv%2BkXZmRS05A9OubzaYJ6YXVO%2Bbd0Ln3dMiCHfcdypDP2XAZzRCTeGhc8yBxxj6Y4yf7%2FTBTHenBzgdunN%2Boemm3JIBzOjU%2FA71v%2F5g6NPMIilonRiZsztOgR2a&X-Amz-Signature=a72d86c9d9f0b3556689a1c58c6976354e6fe096f78a255ca0a3f568c08faabc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

