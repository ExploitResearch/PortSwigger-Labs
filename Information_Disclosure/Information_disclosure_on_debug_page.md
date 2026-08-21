# Information disclosure on debug page

### Goal - 

Obtain and submit the `SECRET_KEY` environment variable.

### Analysis/Exploitation -

### Using free tools

When I try to avoid using features from Burp Professional, several good free tools allow for content discovery. The one I use here is [ffuf](https://github.com/ffuf/ffuf) together with the great wordlists provided by [SecLists](https://github.com/danielmiessler/SecLists).

First, I search for common directories within the web root of the application with

```bash
ffuf -w /usr/share/wordlists/SecLists-master/Discovery/Web-Content/directory-list-2.3-small.txt -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/FUZZ
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/30e0f4ad-9807-4e14-bd8f-f1a79b0171c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TD56P2KR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210456Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBDiOAiMzkn09irSedhPg86Gfl1czIE%2FEAK4RAiXmcOfAiBW5ZTMC31SLrtnGLhuRfzA%2B0mSzJaNgE5so1JV9qDEaSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzpuCEKqUfj4t4NyRKtwDpUVww9k%2FHOLhTQ7P5gS8TdRpF%2FvPW7HrJ4jehj8uKb22eEpXhJSBJ9tDXlNTCzQMjHijjyvv2IbnM8QjF9wR%2FatFh7ij2iqYSCuZO36AVzSk4j7r6AsOAWETNEslHHneSViIFU%2FVKq96KZ0d3XWUC%2B8146AXXFUkdh7%2ByWMKNYsaiuFb1w%2Fy1r5PiQ7WK63szebxbxMDN2xV28nm27Cgb86JpBBupwTtUdBVZDv9TTHrdilCmzEuldVkK2KdRl2QYWeUshvg2XFf42rge%2B3xGhuE4Pd9cr1%2Fh6o4u7j2vF4A69lb7Ozcu9gtS3TQjAJ%2BcFeumjLf3WJGwfxdyXqMIrDqX2ROeyZm8djYlSeP%2BoN9UQB77eVszQ4qWvR9Gf0USSITU1M0UZWVH3mo%2B4Nrt%2FEQYiQcr9VhnlFOnaz%2F8bD%2BtedgzzzJ4EH8vERzlvw5VXDOeMZViDZ%2FHG50AvbPcMz9xwwoMO5%2FBqONofKs74vWXeCq9LSpvHMKZpnODoTyv9tLcOZYKiJyW%2F35B0gWRqJoBG3vw2K17xfk4mK%2B1CjP%2FhLxSy%2Fq4D2rQQNXGGBTX5Du7qnf9DrsxZCTY6v3EPc27jZ%2BU0M7vUkMswTJHVqCv1Z7Hu%2FdnWHFwcgw%2Fcai1AY6pgH%2F1Nt1%2B1wt1fH7RC6XikWCE3iViPIa1XbORw71z7RcIPR%2FF%2FS8FPqeCLgLdGmiugbpf690t2STS%2FJ%2F3xK%2FPSFJJ1LiJADnqMCbTnNXMxpP1fQFhZRo9mvyqPmL6eyscy6bjoiSIQFWBU47curKvYPxrOc8J5PVtYaM27ybcyQEhrR%2BR8oa%2FWFT%2FaqP44CvQ%2FpViybdnVTVivQkyXUph2ovrgnVVwsL&X-Amz-Signature=e09bc0100ad7a7e97b34f6f88e4f585484bfd084204c50199dde448568d1ae4f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

I can now search within this directory for common files with

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery-content/Web-Content/common.txt  -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/cgi-bin/FUZZ
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/37effcbf-768e-40cd-9bc5-8544f17e3ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TD56P2KR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210456Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBDiOAiMzkn09irSedhPg86Gfl1czIE%2FEAK4RAiXmcOfAiBW5ZTMC31SLrtnGLhuRfzA%2B0mSzJaNgE5so1JV9qDEaSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzpuCEKqUfj4t4NyRKtwDpUVww9k%2FHOLhTQ7P5gS8TdRpF%2FvPW7HrJ4jehj8uKb22eEpXhJSBJ9tDXlNTCzQMjHijjyvv2IbnM8QjF9wR%2FatFh7ij2iqYSCuZO36AVzSk4j7r6AsOAWETNEslHHneSViIFU%2FVKq96KZ0d3XWUC%2B8146AXXFUkdh7%2ByWMKNYsaiuFb1w%2Fy1r5PiQ7WK63szebxbxMDN2xV28nm27Cgb86JpBBupwTtUdBVZDv9TTHrdilCmzEuldVkK2KdRl2QYWeUshvg2XFf42rge%2B3xGhuE4Pd9cr1%2Fh6o4u7j2vF4A69lb7Ozcu9gtS3TQjAJ%2BcFeumjLf3WJGwfxdyXqMIrDqX2ROeyZm8djYlSeP%2BoN9UQB77eVszQ4qWvR9Gf0USSITU1M0UZWVH3mo%2B4Nrt%2FEQYiQcr9VhnlFOnaz%2F8bD%2BtedgzzzJ4EH8vERzlvw5VXDOeMZViDZ%2FHG50AvbPcMz9xwwoMO5%2FBqONofKs74vWXeCq9LSpvHMKZpnODoTyv9tLcOZYKiJyW%2F35B0gWRqJoBG3vw2K17xfk4mK%2B1CjP%2FhLxSy%2Fq4D2rQQNXGGBTX5Du7qnf9DrsxZCTY6v3EPc27jZ%2BU0M7vUkMswTJHVqCv1Z7Hu%2FdnWHFwcgw%2Fcai1AY6pgH%2F1Nt1%2B1wt1fH7RC6XikWCE3iViPIa1XbORw71z7RcIPR%2FF%2FS8FPqeCLgLdGmiugbpf690t2STS%2FJ%2F3xK%2FPSFJJ1LiJADnqMCbTnNXMxpP1fQFhZRo9mvyqPmL6eyscy6bjoiSIQFWBU47curKvYPxrOc8J5PVtYaM27ybcyQEhrR%2BR8oa%2FWFT%2FaqP44CvQ%2FpViybdnVTVivQkyXUph2ovrgnVVwsL&X-Amz-Signature=473e093cbc366e34a3d59107b10753307113d0d7703ff2413a4a2f98fcff286a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Using Burp Professional

Go to the "Target" > "Site Map" tab. Right-click on the top-level entry for the lab and select "Engagement tools" > "Find comments". Notice that the home page contains an HTML comment that contains a link called "Debug". This points to `/cgi-bin/phpinfo.php`.

or Use the default options and start the content discovery. Burp quickly shows the `phpinfo.php` file in the site map:

Opening this file in the browser and scrolling through the content shows the answer:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ebc3c145-2e85-4bdd-86c9-badcaff70ec6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TD56P2KR%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210456Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBDiOAiMzkn09irSedhPg86Gfl1czIE%2FEAK4RAiXmcOfAiBW5ZTMC31SLrtnGLhuRfzA%2B0mSzJaNgE5so1JV9qDEaSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzpuCEKqUfj4t4NyRKtwDpUVww9k%2FHOLhTQ7P5gS8TdRpF%2FvPW7HrJ4jehj8uKb22eEpXhJSBJ9tDXlNTCzQMjHijjyvv2IbnM8QjF9wR%2FatFh7ij2iqYSCuZO36AVzSk4j7r6AsOAWETNEslHHneSViIFU%2FVKq96KZ0d3XWUC%2B8146AXXFUkdh7%2ByWMKNYsaiuFb1w%2Fy1r5PiQ7WK63szebxbxMDN2xV28nm27Cgb86JpBBupwTtUdBVZDv9TTHrdilCmzEuldVkK2KdRl2QYWeUshvg2XFf42rge%2B3xGhuE4Pd9cr1%2Fh6o4u7j2vF4A69lb7Ozcu9gtS3TQjAJ%2BcFeumjLf3WJGwfxdyXqMIrDqX2ROeyZm8djYlSeP%2BoN9UQB77eVszQ4qWvR9Gf0USSITU1M0UZWVH3mo%2B4Nrt%2FEQYiQcr9VhnlFOnaz%2F8bD%2BtedgzzzJ4EH8vERzlvw5VXDOeMZViDZ%2FHG50AvbPcMz9xwwoMO5%2FBqONofKs74vWXeCq9LSpvHMKZpnODoTyv9tLcOZYKiJyW%2F35B0gWRqJoBG3vw2K17xfk4mK%2B1CjP%2FhLxSy%2Fq4D2rQQNXGGBTX5Du7qnf9DrsxZCTY6v3EPc27jZ%2BU0M7vUkMswTJHVqCv1Z7Hu%2FdnWHFwcgw%2Fcai1AY6pgH%2F1Nt1%2B1wt1fH7RC6XikWCE3iViPIa1XbORw71z7RcIPR%2FF%2FS8FPqeCLgLdGmiugbpf690t2STS%2FJ%2F3xK%2FPSFJJ1LiJADnqMCbTnNXMxpP1fQFhZRo9mvyqPmL6eyscy6bjoiSIQFWBU47curKvYPxrOc8J5PVtYaM27ybcyQEhrR%2BR8oa%2FWFT%2FaqP44CvQ%2FpViybdnVTVivQkyXUph2ovrgnVVwsL&X-Amz-Signature=8c7889daaf5c7daa96feb33046d5a9b0ea6dc4ea0191199384589b00e3812e05&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

