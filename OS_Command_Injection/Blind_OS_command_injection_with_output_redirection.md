# Blind OS command injection with output redirection

### Goal - 

Exploit the blind command injection and redirect the output from the whoami command to the /var/www/images

### Analysis/Exploitation 

> 💡 You can redirect the output from the injected command into a file within the web root that you can access then retrieve using the browser. 
For example, if the application serves static resources from the filesystem location `/var/www/static`, then you can submit the following input:

```bash
& whoami > /var/www/static/whoami.txt &
```

The `>` character sends the output from the `whoami` command to the specified file. You can then use the browser to fetch `https://vulnerable-website.com/whoami.txt` to retrieve the file, and view the output from the injected command.

In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f419ccfa-6c51-4811-9269-500414a57519/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667CC7HZZY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215557Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDCffKduaG8BTiIDDC6lXdwPM6b3%2F2D7uQW%2FSB1EgbdcAiBi8vHoi7nToWJEvzGYE0disY1IQo8BWczi9JLykOohUSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOLM0QFjUWkx98MK0KtwDflaOMyjt63lhSwjIwphSz0nzQ9tRu3lkEiBVRIQC9XV5ZDdhIIp6TTqexzypxgNe40RTBJcZMQ2PXe%2BCEZiTFprOQZB0lAvBZE1CDMLZrQC2EupkwlZTAG3xfXL3jsqBT96I%2B4LvFaQNZNPGsFTGjNTVbh1CVq9yi5IiDXvtDmyv%2BptgE%2FkzioqSbrkMni3bCGh%2FW78xExEzBLsJqNJnBtJwsryAidqlIzKDRRqm%2Fwh%2BfxrEV2aQDXfazfEWsG1hBteyW3%2FO3iKG4hbdYNGgtD17UVwVUtGhn2nduognjzu0ND5CAJdmd0gaBOoqk6xqgCzA0sJF9uF%2Btazw2dK%2FayiTmwAYNCNpE40Kqvv89HxaZgpQGyl3MTZkFwTygMoDfnM8SLZRjlTesjKFMc9eNRSQHtgU82nCc9G7gxsanwMTKdFHY%2BWm15TdMh%2BodEjGmvH8a75hoVKId0UDendwrgGRPPwu7UiZaW5MN0fNJkIIeOF%2B9wamLXsL97jChchoU%2FrQcppOyZqbrc5Fy8Px1LiCzIGX2OuEcKFh%2BuYxdyXvV2N5t6VtayqhW7X%2BDQdTHGrw%2FG6qSzYl5ZEtYhdyhoz4%2FgbCsNQWQ94NiA7%2BbEJSnRqFDDaVbPNjupgw%2B4aj1AY6pgEGsVEd3%2Fs4w0cn5XCW33tN2GWveCRH3kP0yOQFcxA059rgntG8ioM46ZSTf3Yqcf6xpVLO%2BcQGG5gEFCx4oyInCNMWdjuLnirx2uUl10Pmo7pgaHvmxMWBRToXAxgfbxy8eKlEWa08u1a%2B13V0T1pTGObgeKV4DCQjr7S77fdaOvLFvKb7344lixpj0KffCH2sBpkr1%2FyvahFmM%2B5Az3B3N%2BatImsE&X-Amz-Signature=8dd9acb568d3540e825b9ae8906336a463fca48178555eade28b9a6fe06ad9d5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now, instead of triggering a time delay, we can also **redirect the command’s output to a file, and stored it to where we can access.**

In the home page, we can see there are some product images:

Typically you’ll **stored the output to a static file**, like `images`.As we can see, **they are at **`/image`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e029e26c-adab-42eb-8b75-cc03aa5cb267/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667CC7HZZY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215557Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDCffKduaG8BTiIDDC6lXdwPM6b3%2F2D7uQW%2FSB1EgbdcAiBi8vHoi7nToWJEvzGYE0disY1IQo8BWczi9JLykOohUSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOLM0QFjUWkx98MK0KtwDflaOMyjt63lhSwjIwphSz0nzQ9tRu3lkEiBVRIQC9XV5ZDdhIIp6TTqexzypxgNe40RTBJcZMQ2PXe%2BCEZiTFprOQZB0lAvBZE1CDMLZrQC2EupkwlZTAG3xfXL3jsqBT96I%2B4LvFaQNZNPGsFTGjNTVbh1CVq9yi5IiDXvtDmyv%2BptgE%2FkzioqSbrkMni3bCGh%2FW78xExEzBLsJqNJnBtJwsryAidqlIzKDRRqm%2Fwh%2BfxrEV2aQDXfazfEWsG1hBteyW3%2FO3iKG4hbdYNGgtD17UVwVUtGhn2nduognjzu0ND5CAJdmd0gaBOoqk6xqgCzA0sJF9uF%2Btazw2dK%2FayiTmwAYNCNpE40Kqvv89HxaZgpQGyl3MTZkFwTygMoDfnM8SLZRjlTesjKFMc9eNRSQHtgU82nCc9G7gxsanwMTKdFHY%2BWm15TdMh%2BodEjGmvH8a75hoVKId0UDendwrgGRPPwu7UiZaW5MN0fNJkIIeOF%2B9wamLXsL97jChchoU%2FrQcppOyZqbrc5Fy8Px1LiCzIGX2OuEcKFh%2BuYxdyXvV2N5t6VtayqhW7X%2BDQdTHGrw%2FG6qSzYl5ZEtYhdyhoz4%2FgbCsNQWQ94NiA7%2BbEJSnRqFDDaVbPNjupgw%2B4aj1AY6pgEGsVEd3%2Fs4w0cn5XCW33tN2GWveCRH3kP0yOQFcxA059rgntG8ioM46ZSTf3Yqcf6xpVLO%2BcQGG5gEFCx4oyInCNMWdjuLnirx2uUl10Pmo7pgaHvmxMWBRToXAxgfbxy8eKlEWa08u1a%2B13V0T1pTGObgeKV4DCQjr7S77fdaOvLFvKb7344lixpj0KffCH2sBpkr1%2FyvahFmM%2B5Az3B3N%2BatImsE&X-Amz-Signature=2c8c5cc5af681911a1892e8f512f1c521e3095be1e07b2950ad78a3dda1807b6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

To redirect command’s output to a file, we can put it to `/var/www/image/<filename>`.since it is mentionted in lab description that Writeable folder is at `/var/www/images/`

> **Note: **In Linux, web root is usually located in **/var/www/**.

The command to execute is `whoami > /var/www/images/whoami.txt `to write the file. Inject it into the email argument. And as in the previous lab, commenting out the remainder results in a `200 OK`, while not doing so results in `500 Internal Server Error`. Both ways work though.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/dd85ec37-3d71-4f42-94bf-b434ad755201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667CC7HZZY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215557Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDCffKduaG8BTiIDDC6lXdwPM6b3%2F2D7uQW%2FSB1EgbdcAiBi8vHoi7nToWJEvzGYE0disY1IQo8BWczi9JLykOohUSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOLM0QFjUWkx98MK0KtwDflaOMyjt63lhSwjIwphSz0nzQ9tRu3lkEiBVRIQC9XV5ZDdhIIp6TTqexzypxgNe40RTBJcZMQ2PXe%2BCEZiTFprOQZB0lAvBZE1CDMLZrQC2EupkwlZTAG3xfXL3jsqBT96I%2B4LvFaQNZNPGsFTGjNTVbh1CVq9yi5IiDXvtDmyv%2BptgE%2FkzioqSbrkMni3bCGh%2FW78xExEzBLsJqNJnBtJwsryAidqlIzKDRRqm%2Fwh%2BfxrEV2aQDXfazfEWsG1hBteyW3%2FO3iKG4hbdYNGgtD17UVwVUtGhn2nduognjzu0ND5CAJdmd0gaBOoqk6xqgCzA0sJF9uF%2Btazw2dK%2FayiTmwAYNCNpE40Kqvv89HxaZgpQGyl3MTZkFwTygMoDfnM8SLZRjlTesjKFMc9eNRSQHtgU82nCc9G7gxsanwMTKdFHY%2BWm15TdMh%2BodEjGmvH8a75hoVKId0UDendwrgGRPPwu7UiZaW5MN0fNJkIIeOF%2B9wamLXsL97jChchoU%2FrQcppOyZqbrc5Fy8Px1LiCzIGX2OuEcKFh%2BuYxdyXvV2N5t6VtayqhW7X%2BDQdTHGrw%2FG6qSzYl5ZEtYhdyhoz4%2FgbCsNQWQ94NiA7%2BbEJSnRqFDDaVbPNjupgw%2B4aj1AY6pgEGsVEd3%2Fs4w0cn5XCW33tN2GWveCRH3kP0yOQFcxA059rgntG8ioM46ZSTf3Yqcf6xpVLO%2BcQGG5gEFCx4oyInCNMWdjuLnirx2uUl10Pmo7pgaHvmxMWBRToXAxgfbxy8eKlEWa08u1a%2B13V0T1pTGObgeKV4DCQjr7S77fdaOvLFvKb7344lixpj0KffCH2sBpkr1%2FyvahFmM%2B5Az3B3N%2BatImsE&X-Amz-Signature=e80f89c6b798b55d8309fb215d7b6765b9366cd3a2ee53ad07e6a300fbd7d69c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**Access the file**

Now the file is in `/var/www/images`, but the path to it within the application is unknown and perhaps not even accessible directly. But I can utilize the way the application includes its images with a GET request to `/image?filename=`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/1796e77c-5656-43a4-8c91-3fc0bde988d7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667CC7HZZY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215557Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIDCffKduaG8BTiIDDC6lXdwPM6b3%2F2D7uQW%2FSB1EgbdcAiBi8vHoi7nToWJEvzGYE0disY1IQo8BWczi9JLykOohUSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMOLM0QFjUWkx98MK0KtwDflaOMyjt63lhSwjIwphSz0nzQ9tRu3lkEiBVRIQC9XV5ZDdhIIp6TTqexzypxgNe40RTBJcZMQ2PXe%2BCEZiTFprOQZB0lAvBZE1CDMLZrQC2EupkwlZTAG3xfXL3jsqBT96I%2B4LvFaQNZNPGsFTGjNTVbh1CVq9yi5IiDXvtDmyv%2BptgE%2FkzioqSbrkMni3bCGh%2FW78xExEzBLsJqNJnBtJwsryAidqlIzKDRRqm%2Fwh%2BfxrEV2aQDXfazfEWsG1hBteyW3%2FO3iKG4hbdYNGgtD17UVwVUtGhn2nduognjzu0ND5CAJdmd0gaBOoqk6xqgCzA0sJF9uF%2Btazw2dK%2FayiTmwAYNCNpE40Kqvv89HxaZgpQGyl3MTZkFwTygMoDfnM8SLZRjlTesjKFMc9eNRSQHtgU82nCc9G7gxsanwMTKdFHY%2BWm15TdMh%2BodEjGmvH8a75hoVKId0UDendwrgGRPPwu7UiZaW5MN0fNJkIIeOF%2B9wamLXsL97jChchoU%2FrQcppOyZqbrc5Fy8Px1LiCzIGX2OuEcKFh%2BuYxdyXvV2N5t6VtayqhW7X%2BDQdTHGrw%2FG6qSzYl5ZEtYhdyhoz4%2FgbCsNQWQ94NiA7%2BbEJSnRqFDDaVbPNjupgw%2B4aj1AY6pgEGsVEd3%2Fs4w0cn5XCW33tN2GWveCRH3kP0yOQFcxA059rgntG8ioM46ZSTf3Yqcf6xpVLO%2BcQGG5gEFCx4oyInCNMWdjuLnirx2uUl10Pmo7pgaHvmxMWBRToXAxgfbxy8eKlEWa08u1a%2B13V0T1pTGObgeKV4DCQjr7S77fdaOvLFvKb7344lixpj0KffCH2sBpkr1%2FyvahFmM%2B5Az3B3N%2BatImsE&X-Amz-Signature=e8f5a54791dd2ed17b2c125074182aa8f531785ad75cc3174961eed8d634b83b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 **summary
**

  1. Find & Confirm blind command injection
-email field
  1. Check location from where application serves static resources, here images 
  1. Redirect output to file at that static location
  1. Check if file was created by accessing it
