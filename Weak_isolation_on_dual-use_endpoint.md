# Weak isolation on dual-use endpoint

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

One thing that catches my eye is the password change functionality:

Why does it contain the username as an input field? I'd expect either the password to be changed for the logged-in user, `wiener`. In this case, the input field for the username would be unnecessary.

What happens if I use it and simply change the username to `administrator`?

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb5a0148-e37a-4709-9b8f-4255565d4c2e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VJ66KGJ5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204725Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCAZchCoypXEyOGd6gQDue0b59cNm%2F3uF6wO43ak%2F6AdgIhAJJbDVWG08z0A%2Bb8sEamcDbf%2Bx9716M34xi8zCkOzNOSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxRFW%2Fgugq6J3yvo4Mq3ANZPfIJx%2BfPjS2U96tnwNSx2puETDt0QsqjQrjUIF5wBpLZsmtXg7Lzcv41%2BXchdcgmUp2PvuT7GFe4sk%2FVUbxA7xzLsNI9H1ltM3%2BIpSCrdeBjZb%2BeyRZIlNR0Uiget8Nl8O7nE0A%2BQDEN5oF4%2Fwlose9HifrcQGNah0BOYrm3p4S2HlG4CmL3vWmkstd9uOyvgfxdr%2FTZbgPu3mJ8AOZgAFoec7m7zScaeya0Lug1QvxPUDKT44NuCd4OQY5872sDeQSsi3PB9AeJEGnX2nttl2C2tA4pjdnVgbAl6LUVUCfY%2Ba8Sr1LcqIw3UNl2FXNiHsA3Ff7uezv5j07LiO78Wz%2BhOlZ%2B1mcIRgGzQDuZjLlypg5%2Bx3yDJLdoFvT7bstdwzBZBI3%2F02Om8JtaEFBIlRPKAgrfNEQC7cNRPgdJtYJE5poXF7eT9A5t3oz4BDCl0doOUfgixkBgHn13SBDkNMeCXYaDw7c82kQ4Bze169oTDkntk1qIYGktOLP0QyoxswsC0PEnxLKDunI5kcB40JhWoV0yncbPBCTQBY7ioEPuF6SezK%2Fe1g14b7TeauzQ6a%2FRf3OeEX0SXyTF4AFOO4f4jZu0Vpw7IQFF4KDS2Eomno5o16S6XZnc5zCvyaLUBjqkAVwc0yVMud5syLTDCl90QuJ32EZpUY%2FDvPW88S6Y7DWVBi2DxpdtUWr%2FLkLuAhRTPPIwcUvcsMAcPFbU00QaiYGEwlvj50cs7ThqCDJ8SPCGNz8RstOx%2B8Swd4SzNmTr40%2B%2FkeLdr8CUbRBaayW%2FyuMmW48eOvI7xvSi4Wny6pji6IezyLXcKuJ9M8PgWVWvoUPyevdBGZBRbseH5tGdPsr%2BZd8s&X-Amz-Signature=b289cb02e98ad27f3183b05b69ffcabfcede0c2c0e54a5f69cc71afe68f5e810&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We get error Current password is incorrect:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e6e26397-57bd-4650-a628-543c7609a0a8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664VPHNIFZ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204726Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC6hZAlUSJMdYtpMNo755IhphAob2VkBS5O44PZWWJUmgIhAMw3TJuBf6yxUk83M8U8jF%2FPECzDVcJy2%2BRMp8KFXGBGKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igz%2BaE1b%2BoG1p8VyRwMq3AMUD7mtT%2BUGqUU5eTsRllNMtMhJqVS9ZiPSu4xMAY424UL3ZLgY5SSH9PTdwHuXFcCGxDNjx4o4SMGZd9YBA1QPlcinuEJ6tRo2VcnQ0RX1B9WrGk52dKBTKcyeJEepsq7Xl%2BPUs%2F9mORddsYNpYSr3eXk2EeA59neeHpFaEp0Iv9ePOH4vr%2BE5iFNAX9ub7WQIwjQIAqKJ7sbCnzp81FMnNaWl8c41FeI4Jg3UEdG26zxsP0JMyHVkvDiLZee7Lm6fRFvoHold73JBQCKCKG39%2FTVlHH2JpEcICUoq%2BU5vBV%2BJ4mO8GmsMuT4Ws%2FacdtAU1qBDpaIIRCEXEGQ%2BLI8SMnyVvXIn%2BUyTPWEhZrkA1448SW0XH2euQwwQWtSJlKOc7AyKvB8KpMSWW47f1Gejx3wvJewo%2FEI633m3JrU2qeqfCCWCUL79dXkoQiAgBoM%2FSIlU6e3f7X4rwRa%2BgaskJPQ75HsVFuxebjm6P0voi312PATrDIvtDkX8KdNrJf0cLEo3vCtipGIhxBPuYoy%2B29%2FWEAvr7lnR%2FFIGquTbR7s%2FrNgOOfI3UoxYVo7Fvfd92owVVql8ogCPtiMq4AuIxNqtmCcx6thP%2F%2B%2FKmzf1WS6SismrgjdirfOpAjDyxaLUBjqkAUloN81zgDZTYAT8oqy%2BGTtjcmvcybB2%2FmaC6BsMWppPZm1011jSodRtnRKa8OhzyINlPgzfu15KUQIctidjPC%2BZ0GdMgB6PYBlhKAaEdC4eBfd9qw%2Bj1G%2BouF55uweM979%2F604X43NwFwRhH2B5aGHGEZv2mFuBZuqPFs8VnRqbz4ccH%2FjZ943iFPzph86JxmYmY7VMd075kNIXtkn97P%2Fn8vNe&X-Amz-Signature=717de648fe3b937e98a40111a67857177d2ba73a74de95fc1ba666709952a243&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From this result I can derive a few pieces of information:

1. The password change failed due to a wrong current password.
1. The password comparison was not performed with the password account that is logged in but with the password of the account set in `Username`
1. At the point the 'Update password' form was generated, the application did use the logged-in user again.
But at some point during the generation of the response, the application assumed that my username is `administrator`. This points to some weird logic behind the scenes that warrant further investigation.

To verify that no password was changed despite the error message, I attempt to log in with both `wiener` and `administrator` using the newly set password. It fails as expected.

### Analyzing the traffic

When we clicked the `Change password` button, **it send a POST request to **`/my-account/change-password`**, with parameter **`csrf`**, **`username`**, **`current-password`**, **`new-password-1`**, and **`new-password-2`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/81e66630-f649-477b-94d3-afd5f40c0120/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VJ66KGJ5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204725Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCAZchCoypXEyOGd6gQDue0b59cNm%2F3uF6wO43ak%2F6AdgIhAJJbDVWG08z0A%2Bb8sEamcDbf%2Bx9716M34xi8zCkOzNOSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxRFW%2Fgugq6J3yvo4Mq3ANZPfIJx%2BfPjS2U96tnwNSx2puETDt0QsqjQrjUIF5wBpLZsmtXg7Lzcv41%2BXchdcgmUp2PvuT7GFe4sk%2FVUbxA7xzLsNI9H1ltM3%2BIpSCrdeBjZb%2BeyRZIlNR0Uiget8Nl8O7nE0A%2BQDEN5oF4%2Fwlose9HifrcQGNah0BOYrm3p4S2HlG4CmL3vWmkstd9uOyvgfxdr%2FTZbgPu3mJ8AOZgAFoec7m7zScaeya0Lug1QvxPUDKT44NuCd4OQY5872sDeQSsi3PB9AeJEGnX2nttl2C2tA4pjdnVgbAl6LUVUCfY%2Ba8Sr1LcqIw3UNl2FXNiHsA3Ff7uezv5j07LiO78Wz%2BhOlZ%2B1mcIRgGzQDuZjLlypg5%2Bx3yDJLdoFvT7bstdwzBZBI3%2F02Om8JtaEFBIlRPKAgrfNEQC7cNRPgdJtYJE5poXF7eT9A5t3oz4BDCl0doOUfgixkBgHn13SBDkNMeCXYaDw7c82kQ4Bze169oTDkntk1qIYGktOLP0QyoxswsC0PEnxLKDunI5kcB40JhWoV0yncbPBCTQBY7ioEPuF6SezK%2Fe1g14b7TeauzQ6a%2FRf3OeEX0SXyTF4AFOO4f4jZu0Vpw7IQFF4KDS2Eomno5o16S6XZnc5zCvyaLUBjqkAVwc0yVMud5syLTDCl90QuJ32EZpUY%2FDvPW88S6Y7DWVBi2DxpdtUWr%2FLkLuAhRTPPIwcUvcsMAcPFbU00QaiYGEwlvj50cs7ThqCDJ8SPCGNz8RstOx%2B8Swd4SzNmTr40%2B%2FkeLdr8CUbRBaayW%2FyuMmW48eOvI7xvSi4Wny6pji6IezyLXcKuJ9M8PgWVWvoUPyevdBGZBRbseH5tGdPsr%2BZd8s&X-Amz-Signature=6b7a59828a58ebd9b969f977ea43975c1dbc3afb42085aa83d28b870ca279545&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

OK, so I have the csrf token, username and the three password parameters.

While the application generated the response, at the moment my username was embedded, I was the `administrator` user. I was also considered `administrator` while the current password was checked and the error message got inserted. As such, the password change failed as it was not the correct password for that user.

So what happens if I remove the current-password parameter from the form?

This depends on whether it always checks the current password on password change. If this is the case, then it will fail as well, as it should.

However, if the password check only occurs when the parameter is present, then it will be bad for the application but good for me.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2fc35871-6a2d-4cb6-92f8-1016672f0b1d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466VJ66KGJ5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204725Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCAZchCoypXEyOGd6gQDue0b59cNm%2F3uF6wO43ak%2F6AdgIhAJJbDVWG08z0A%2Bb8sEamcDbf%2Bx9716M34xi8zCkOzNOSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxRFW%2Fgugq6J3yvo4Mq3ANZPfIJx%2BfPjS2U96tnwNSx2puETDt0QsqjQrjUIF5wBpLZsmtXg7Lzcv41%2BXchdcgmUp2PvuT7GFe4sk%2FVUbxA7xzLsNI9H1ltM3%2BIpSCrdeBjZb%2BeyRZIlNR0Uiget8Nl8O7nE0A%2BQDEN5oF4%2Fwlose9HifrcQGNah0BOYrm3p4S2HlG4CmL3vWmkstd9uOyvgfxdr%2FTZbgPu3mJ8AOZgAFoec7m7zScaeya0Lug1QvxPUDKT44NuCd4OQY5872sDeQSsi3PB9AeJEGnX2nttl2C2tA4pjdnVgbAl6LUVUCfY%2Ba8Sr1LcqIw3UNl2FXNiHsA3Ff7uezv5j07LiO78Wz%2BhOlZ%2B1mcIRgGzQDuZjLlypg5%2Bx3yDJLdoFvT7bstdwzBZBI3%2F02Om8JtaEFBIlRPKAgrfNEQC7cNRPgdJtYJE5poXF7eT9A5t3oz4BDCl0doOUfgixkBgHn13SBDkNMeCXYaDw7c82kQ4Bze169oTDkntk1qIYGktOLP0QyoxswsC0PEnxLKDunI5kcB40JhWoV0yncbPBCTQBY7ioEPuF6SezK%2Fe1g14b7TeauzQ6a%2FRf3OeEX0SXyTF4AFOO4f4jZu0Vpw7IQFF4KDS2Eomno5o16S6XZnc5zCvyaLUBjqkAVwc0yVMud5syLTDCl90QuJ32EZpUY%2FDvPW88S6Y7DWVBi2DxpdtUWr%2FLkLuAhRTPPIwcUvcsMAcPFbU00QaiYGEwlvj50cs7ThqCDJ8SPCGNz8RstOx%2B8Swd4SzNmTr40%2B%2FkeLdr8CUbRBaayW%2FyuMmW48eOvI7xvSi4Wny6pji6IezyLXcKuJ9M8PgWVWvoUPyevdBGZBRbseH5tGdPsr%2BZd8s&X-Amz-Signature=b2f11274baae77abaef103a5f7a99b004ab55be601e4c18a49f7dee1112830de&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We successfully changed `administrator`’s password!

Try to logout and login again, this time with the credentials `administrator:peter`:


And I appear to be inside the administrator account. The application states that my username is `administrator` and it provides me with a link to an `Admin panel`. I access it, delete `carlos` and receive a confirmation:

