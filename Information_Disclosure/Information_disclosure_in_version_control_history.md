# Information disclosure in version control history

### Goal - 

Obtain the password for the `administrator` user then log in and delete the user `carlos`.

### Analysis/Exploitation -

Let’s enumerate hidden directories via `ffuf`

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/dirsearch.txt -u https://0a5d00c3035ad5be807d9a1700a800c4.web-security-academy.net/FUZZ
```

In here, we found a `/.git` directory! Which is the a GitHub repository directory!

Let’s download all the files via `wget`!

```bash
wget -b -r https://0a5d00c3035ad5be807d9a1700a800c4.web-security-academy.net/.git
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8ccb515d-7908-4190-a835-e296c6708b49/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663COPP5KB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215624Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCR5B%2FTsB7ASH3QYfMJK3XldvGaOkKKqQ3zYs6wx1jbvwIhAKe%2BmmiQ%2FdCma6741%2F0%2Fe6I%2Fe9nkKCJyYUuQT7xzMGOUKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxv0np1aeVCQo9Kb94q3ANjl2ljj%2F9HbdfFdWNBAS1BExTms0ddwJ%2FD2qbn6BYJaq4VWoHvx1lTbzVErpJjqBACzfrDRoimgLHra0GhgoyVZj%2B09bdsPXD%2Bu4HK%2B2qvPHvZ8ibxeq%2FxfGbMeqvVvldw%2F8nm695XcI%2Fe5eFIUKHzLTvk%2FVKdYt6gm%2BKU%2BAWlGesDGj%2BrZusdqCFEDFFJmqWQI%2Bxnc7cLtKVaWkJvx3Uiuf2py%2FuXXSwq%2Ffqat6bHwWMyCRaB%2FxMvnAdFLgG6Md4imsMOFWAACzDQkdyCwClkvwOR31zRWBjPp1RQ4rvLRvibcnzh0%2FoFsyYJ7792btlRUp3YboIH12UGbCIQB8pcqHZDbVymb00J0BdYcFy6BfjZiW5d81YeUGfgaWXJrcEBwz%2FpxTJbtWoVJ93kbuWJvZHUaVes%2BELQc0%2B53Za5%2BBVVEia%2B%2B6y5UVml4%2FZvX0fpSFksUPJNJarsVivP7RdlyPDDs7BDzCrWe6AdYTfP1%2BjyKfUyTwUHdE62PB972%2Fo%2F7Fe4oMGsFzQm%2FpLyTcssYFs%2Fj2cE4wdCLSF0%2Bay87Ma3ZTpv5IyTi2dvRV9bMCr93mRnPU0uYq3HpGdZER7hM5uxoe2NBGEqiDBWwhvgxoSB6oUw%2FgdG92LzSzCxhKPUBjqkAfy59c8flGaD4%2BTPuiNANyjcln%2BCTpRaIogalf3tAdGexN%2BdYKS28tzHFb0qK7lwTzMzhL0e5w%2FtaVomDZ8Gmy2meLpJc1cupgn21kXaXoktTTutpxZAmd1bzR2LJX2JxP8m4c9aqDhfk1%2F6QTcNDuBZFS5KhVBmfidYHOXvkIE5cdX79FkX8nntidLTuI7516nxzfVNfT6gnMRFxK5%2BXVk%2B130l&X-Amz-Signature=9fd7244c427af709fec4f683542f260cee10dfa3b36dd5b0cc9a0dccbfa6c4e4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

go to that directory and list all files inside it

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/5b98504f-03da-49eb-8983-ff6b4daaad07/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663COPP5KB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215624Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCR5B%2FTsB7ASH3QYfMJK3XldvGaOkKKqQ3zYs6wx1jbvwIhAKe%2BmmiQ%2FdCma6741%2F0%2Fe6I%2Fe9nkKCJyYUuQT7xzMGOUKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxv0np1aeVCQo9Kb94q3ANjl2ljj%2F9HbdfFdWNBAS1BExTms0ddwJ%2FD2qbn6BYJaq4VWoHvx1lTbzVErpJjqBACzfrDRoimgLHra0GhgoyVZj%2B09bdsPXD%2Bu4HK%2B2qvPHvZ8ibxeq%2FxfGbMeqvVvldw%2F8nm695XcI%2Fe5eFIUKHzLTvk%2FVKdYt6gm%2BKU%2BAWlGesDGj%2BrZusdqCFEDFFJmqWQI%2Bxnc7cLtKVaWkJvx3Uiuf2py%2FuXXSwq%2Ffqat6bHwWMyCRaB%2FxMvnAdFLgG6Md4imsMOFWAACzDQkdyCwClkvwOR31zRWBjPp1RQ4rvLRvibcnzh0%2FoFsyYJ7792btlRUp3YboIH12UGbCIQB8pcqHZDbVymb00J0BdYcFy6BfjZiW5d81YeUGfgaWXJrcEBwz%2FpxTJbtWoVJ93kbuWJvZHUaVes%2BELQc0%2B53Za5%2BBVVEia%2B%2B6y5UVml4%2FZvX0fpSFksUPJNJarsVivP7RdlyPDDs7BDzCrWe6AdYTfP1%2BjyKfUyTwUHdE62PB972%2Fo%2F7Fe4oMGsFzQm%2FpLyTcssYFs%2Fj2cE4wdCLSF0%2Bay87Ma3ZTpv5IyTi2dvRV9bMCr93mRnPU0uYq3HpGdZER7hM5uxoe2NBGEqiDBWwhvgxoSB6oUw%2FgdG92LzSzCxhKPUBjqkAfy59c8flGaD4%2BTPuiNANyjcln%2BCTpRaIogalf3tAdGexN%2BdYKS28tzHFb0qK7lwTzMzhL0e5w%2FtaVomDZ8Gmy2meLpJc1cupgn21kXaXoktTTutpxZAmd1bzR2LJX2JxP8m4c9aqDhfk1%2F6QTcNDuBZFS5KhVBmfidYHOXvkIE5cdX79FkX8nntidLTuI7516nxzfVNfT6gnMRFxK5%2BXVk%2B130l&X-Amz-Signature=be7f76a7d2a8e784b47406bdae2ce4daba281271eee97e2ab7202300961d5c68&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Now, we can use **`git`** to view all the commit logs!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e9e5fd1b-927e-4206-8b45-8cd6a00058df/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663COPP5KB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215624Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCR5B%2FTsB7ASH3QYfMJK3XldvGaOkKKqQ3zYs6wx1jbvwIhAKe%2BmmiQ%2FdCma6741%2F0%2Fe6I%2Fe9nkKCJyYUuQT7xzMGOUKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxv0np1aeVCQo9Kb94q3ANjl2ljj%2F9HbdfFdWNBAS1BExTms0ddwJ%2FD2qbn6BYJaq4VWoHvx1lTbzVErpJjqBACzfrDRoimgLHra0GhgoyVZj%2B09bdsPXD%2Bu4HK%2B2qvPHvZ8ibxeq%2FxfGbMeqvVvldw%2F8nm695XcI%2Fe5eFIUKHzLTvk%2FVKdYt6gm%2BKU%2BAWlGesDGj%2BrZusdqCFEDFFJmqWQI%2Bxnc7cLtKVaWkJvx3Uiuf2py%2FuXXSwq%2Ffqat6bHwWMyCRaB%2FxMvnAdFLgG6Md4imsMOFWAACzDQkdyCwClkvwOR31zRWBjPp1RQ4rvLRvibcnzh0%2FoFsyYJ7792btlRUp3YboIH12UGbCIQB8pcqHZDbVymb00J0BdYcFy6BfjZiW5d81YeUGfgaWXJrcEBwz%2FpxTJbtWoVJ93kbuWJvZHUaVes%2BELQc0%2B53Za5%2BBVVEia%2B%2B6y5UVml4%2FZvX0fpSFksUPJNJarsVivP7RdlyPDDs7BDzCrWe6AdYTfP1%2BjyKfUyTwUHdE62PB972%2Fo%2F7Fe4oMGsFzQm%2FpLyTcssYFs%2Fj2cE4wdCLSF0%2Bay87Ma3ZTpv5IyTi2dvRV9bMCr93mRnPU0uYq3HpGdZER7hM5uxoe2NBGEqiDBWwhvgxoSB6oUw%2FgdG92LzSzCxhKPUBjqkAfy59c8flGaD4%2BTPuiNANyjcln%2BCTpRaIogalf3tAdGexN%2BdYKS28tzHFb0qK7lwTzMzhL0e5w%2FtaVomDZ8Gmy2meLpJc1cupgn21kXaXoktTTutpxZAmd1bzR2LJX2JxP8m4c9aqDhfk1%2F6QTcNDuBZFS5KhVBmfidYHOXvkIE5cdX79FkX8nntidLTuI7516nxzfVNfT6gnMRFxK5%2BXVk%2B130l&X-Amz-Signature=0494614a9563397c3ec8d36ed8aebeca1ae9d5e8f4905d9863402227104f3a7f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Log revealing that password was removed so now **print that commit:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3b9fcdfa-4382-4947-ac7c-171876117efe/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663COPP5KB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215624Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCR5B%2FTsB7ASH3QYfMJK3XldvGaOkKKqQ3zYs6wx1jbvwIhAKe%2BmmiQ%2FdCma6741%2F0%2Fe6I%2Fe9nkKCJyYUuQT7xzMGOUKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxv0np1aeVCQo9Kb94q3ANjl2ljj%2F9HbdfFdWNBAS1BExTms0ddwJ%2FD2qbn6BYJaq4VWoHvx1lTbzVErpJjqBACzfrDRoimgLHra0GhgoyVZj%2B09bdsPXD%2Bu4HK%2B2qvPHvZ8ibxeq%2FxfGbMeqvVvldw%2F8nm695XcI%2Fe5eFIUKHzLTvk%2FVKdYt6gm%2BKU%2BAWlGesDGj%2BrZusdqCFEDFFJmqWQI%2Bxnc7cLtKVaWkJvx3Uiuf2py%2FuXXSwq%2Ffqat6bHwWMyCRaB%2FxMvnAdFLgG6Md4imsMOFWAACzDQkdyCwClkvwOR31zRWBjPp1RQ4rvLRvibcnzh0%2FoFsyYJ7792btlRUp3YboIH12UGbCIQB8pcqHZDbVymb00J0BdYcFy6BfjZiW5d81YeUGfgaWXJrcEBwz%2FpxTJbtWoVJ93kbuWJvZHUaVes%2BELQc0%2B53Za5%2BBVVEia%2B%2B6y5UVml4%2FZvX0fpSFksUPJNJarsVivP7RdlyPDDs7BDzCrWe6AdYTfP1%2BjyKfUyTwUHdE62PB972%2Fo%2F7Fe4oMGsFzQm%2FpLyTcssYFs%2Fj2cE4wdCLSF0%2Bay87Ma3ZTpv5IyTi2dvRV9bMCr93mRnPU0uYq3HpGdZER7hM5uxoe2NBGEqiDBWwhvgxoSB6oUw%2FgdG92LzSzCxhKPUBjqkAfy59c8flGaD4%2BTPuiNANyjcln%2BCTpRaIogalf3tAdGexN%2BdYKS28tzHFb0qK7lwTzMzhL0e5w%2FtaVomDZ8Gmy2meLpJc1cupgn21kXaXoktTTutpxZAmd1bzR2LJX2JxP8m4c9aqDhfk1%2F6QTcNDuBZFS5KhVBmfidYHOXvkIE5cdX79FkX8nntidLTuI7516nxzfVNfT6gnMRFxK5%2BXVk%2B130l&X-Amz-Signature=9c5c342c4f3f6d528e5253ca97d5c3ba749776932b18e0eb2adcc7d2761697d5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Found `administrator` password: `v2v6cafbhrqnfxq6i622`

**login as **`administrator`** and delete user **`carlos`**!**
