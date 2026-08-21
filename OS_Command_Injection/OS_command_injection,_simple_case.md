# OS command injection, simple case

### Goal - 

Exploit command injection to execute whoami command.

### Analysis/Exploitation 

As usual, the first step is to browse around a bit. Upon viewing view details of an product we get detail information about that product and we can see upon visiting a specific product a parameter named **productId **is being set. Well this is where we can try to preform command injection and i did but no luck because it fetches information by using an API which restrict all special characters. But as there is another functionality which allows us check for availability of stocks.

Let’s click the `Check stock` button, and intercept the request via Burp Suite

When we clicked that button, it’ll send a POST request to `/product/stock`, with parameter `productId=1` and `storeId=1`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/57677f51-8e40-4a70-bab1-35d5591b4927/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S7IBE2RN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210427Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDB102a5xyARYXPpjOpQvnHtzo8TZzK0m6rDlebk4722AiAIDPedAi9ec5flKX9XQ8%2BD%2Fu19xp9dHdGR5itWJPMHNyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMTyaUbH%2FXqbDoDvWcKtwDZsv9uT28AMh2Ichf1yerj0nbPtXlRO2nrTgO3HHMbb9YAUg599zLfy2YMA5bmLMQ%2FVZE97DaZQQdIL9AbFiByALHxTzvQReBWfYA3oxCrmFe0WAmdaRmc6ths29uaoSCf7IN%2BakITBAiLVtVy%2FTTGhZPqYCvBz9mIY6QXQUcIQU4qEi0dpzlYcd94CK8iEtG%2FxrSVHyd7qxn2602D4Fpz5u7R2BkGeExM2fh4SF8rslbBiUk87aJRQKn%2FI6tqgFcsyed0mL%2FUA592kFY%2Blf3%2BU8Rhsl%2FVAJnVCGlX97UlsRen0BJuVCvlLuHGj%2B53XUZcx4ka2SnnROr9I%2BNSJVUNcTFJafBZZuEpE%2FJ%2BZFSBlS4OFO%2BsCiVSqlaxxZwhIcyraNaWMx02xcKxssfuZ7dSvIjSMChey4355d5cur6G27dKa60th0RVooZ6yKTh9bGREeJBJb1IqNjzX3ftbyX3VgAEcTWxjXKQSgVvoBG2OkRD2aLK39cCsdMfdhczznTYtcX%2Br9ZCmRELiTs7GB24BfeCQzOwHuwSpAGpjuWcnKh3Vd4Q1x5wiV%2BvqW1uWtZpLF7LnABcXlscwnBtN%2B0YZdwJBE3WD7EuxEtPufcPfYpXnPAc7MhyntEp9AwxMii1AY6pgE24ZMcme348qBn%2BDbXMjQ%2FwV6wlu%2F73X9HXArMeMa%2BJZ5bMRJ4Ll%2F%2BThztG1wp78ZUAw1KrETuIsI7M%2BG0CnFHTPyBZ0ARCDfXxpHybYHsRS2ccokVDJdEtKrhxxgsZ3LFj894azVOnCAWPCQXqcQIC302pU%2FI%2FXZoqPvO5UBe0XWdMJDYA7%2B%2Bcu0jwn8m6VB0q3tZM5ku8RihkZAVB05Fu82%2F%2FcJn&X-Amz-Signature=4f601699791686edd0f4fa039167bfde80e002d0023f695e0553bacc056977c6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As we have two parameters, I try to inject both with different commands. This way, I can find out which parameter is injectable and in which order they are executed.

> 💡 The script call might look something like this (likely not the exact syntax, but the general idea is the same):

```bash
echo system("someScript.sh $_REQUEST['productID'] $_REQUEST['storeId']")
```

In this case, the parameters are used as arguments for the script and the output is directly echoed back into the HTML.

There are multiple ways to execute multiple commands in one line in a shell, separating the individual commands with for example `&`, `&&`, `|`, `||`, `;`. All behave slightly differently. On Unix systems, my favorite is `;` as it completely separates the commands without side effects based on return conditions or execution order. In some conditions `&` is better as it backgrounds the command before my injection and runs my code without waiting for the other command to finish. Still, my favourite remains `;`.

**NOTE :**** when using **`&`**, it must be URLencoded**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/abae6bdd-003c-43b0-a3dc-7da788ecab25/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S7IBE2RN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210427Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDB102a5xyARYXPpjOpQvnHtzo8TZzK0m6rDlebk4722AiAIDPedAi9ec5flKX9XQ8%2BD%2Fu19xp9dHdGR5itWJPMHNyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMTyaUbH%2FXqbDoDvWcKtwDZsv9uT28AMh2Ichf1yerj0nbPtXlRO2nrTgO3HHMbb9YAUg599zLfy2YMA5bmLMQ%2FVZE97DaZQQdIL9AbFiByALHxTzvQReBWfYA3oxCrmFe0WAmdaRmc6ths29uaoSCf7IN%2BakITBAiLVtVy%2FTTGhZPqYCvBz9mIY6QXQUcIQU4qEi0dpzlYcd94CK8iEtG%2FxrSVHyd7qxn2602D4Fpz5u7R2BkGeExM2fh4SF8rslbBiUk87aJRQKn%2FI6tqgFcsyed0mL%2FUA592kFY%2Blf3%2BU8Rhsl%2FVAJnVCGlX97UlsRen0BJuVCvlLuHGj%2B53XUZcx4ka2SnnROr9I%2BNSJVUNcTFJafBZZuEpE%2FJ%2BZFSBlS4OFO%2BsCiVSqlaxxZwhIcyraNaWMx02xcKxssfuZ7dSvIjSMChey4355d5cur6G27dKa60th0RVooZ6yKTh9bGREeJBJb1IqNjzX3ftbyX3VgAEcTWxjXKQSgVvoBG2OkRD2aLK39cCsdMfdhczznTYtcX%2Br9ZCmRELiTs7GB24BfeCQzOwHuwSpAGpjuWcnKh3Vd4Q1x5wiV%2BvqW1uWtZpLF7LnABcXlscwnBtN%2B0YZdwJBE3WD7EuxEtPufcPfYpXnPAc7MhyntEp9AwxMii1AY6pgE24ZMcme348qBn%2BDbXMjQ%2FwV6wlu%2F73X9HXArMeMa%2BJZ5bMRJ4Ll%2F%2BThztG1wp78ZUAw1KrETuIsI7M%2BG0CnFHTPyBZ0ARCDfXxpHybYHsRS2ccokVDJdEtKrhxxgsZ3LFj894azVOnCAWPCQXqcQIC302pU%2FI%2FXZoqPvO5UBe0XWdMJDYA7%2B%2Bcu0jwn8m6VB0q3tZM5ku8RihkZAVB05Fu82%2F%2FcJn&X-Amz-Signature=9e59cf6e3c43383ebce9ecdba4fccc62b2a2d123c9ea79c5dd987b238dd41d5b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From the response, it can be seen that both parameters are injectable, and they are executed in the order productId first, storeId second.

**Let’s execute **`whoami`** command**

comment out the remainder of the line after the `whoami` to avoid the error message of the second parameter:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/922ea403-d4eb-47da-81af-f792b32ac69e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S7IBE2RN%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210427Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDB102a5xyARYXPpjOpQvnHtzo8TZzK0m6rDlebk4722AiAIDPedAi9ec5flKX9XQ8%2BD%2Fu19xp9dHdGR5itWJPMHNyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMTyaUbH%2FXqbDoDvWcKtwDZsv9uT28AMh2Ichf1yerj0nbPtXlRO2nrTgO3HHMbb9YAUg599zLfy2YMA5bmLMQ%2FVZE97DaZQQdIL9AbFiByALHxTzvQReBWfYA3oxCrmFe0WAmdaRmc6ths29uaoSCf7IN%2BakITBAiLVtVy%2FTTGhZPqYCvBz9mIY6QXQUcIQU4qEi0dpzlYcd94CK8iEtG%2FxrSVHyd7qxn2602D4Fpz5u7R2BkGeExM2fh4SF8rslbBiUk87aJRQKn%2FI6tqgFcsyed0mL%2FUA592kFY%2Blf3%2BU8Rhsl%2FVAJnVCGlX97UlsRen0BJuVCvlLuHGj%2B53XUZcx4ka2SnnROr9I%2BNSJVUNcTFJafBZZuEpE%2FJ%2BZFSBlS4OFO%2BsCiVSqlaxxZwhIcyraNaWMx02xcKxssfuZ7dSvIjSMChey4355d5cur6G27dKa60th0RVooZ6yKTh9bGREeJBJb1IqNjzX3ftbyX3VgAEcTWxjXKQSgVvoBG2OkRD2aLK39cCsdMfdhczznTYtcX%2Br9ZCmRELiTs7GB24BfeCQzOwHuwSpAGpjuWcnKh3Vd4Q1x5wiV%2BvqW1uWtZpLF7LnABcXlscwnBtN%2B0YZdwJBE3WD7EuxEtPufcPfYpXnPAc7MhyntEp9AwxMii1AY6pgE24ZMcme348qBn%2BDbXMjQ%2FwV6wlu%2F73X9HXArMeMa%2BJZ5bMRJ4Ll%2F%2BThztG1wp78ZUAw1KrETuIsI7M%2BG0CnFHTPyBZ0ARCDfXxpHybYHsRS2ccokVDJdEtKrhxxgsZ3LFj894azVOnCAWPCQXqcQIC302pU%2FI%2FXZoqPvO5UBe0XWdMJDYA7%2B%2Bcu0jwn8m6VB0q3tZM5ku8RihkZAVB05Fu82%2F%2FcJn&X-Amz-Signature=b7612142848d262742f452e117104fc0d5854b02637fd49543a7f8aba1da3bf6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

