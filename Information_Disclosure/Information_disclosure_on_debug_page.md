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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/30e0f4ad-9807-4e14-bd8f-f1a79b0171c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XL6YUMGC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222038Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBCRX7X9ISauAmfeaxjkgDLGIfs5n1nlsUoZpo9s5wAUAiEA%2Fk%2FbA%2B4gIijMb1OcltwHAqGShtTl6MXjbtpPfhAiD9UqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDpar%2Bevh%2FNpmSt5dSrcA6UK4SlioicJKxZ9M8stU0hNZ7vyq386Vd%2Fw0C0bEBsh28m3LWXrCop5Hqni2UH%2FNUSEwkT036u2Dw7ACed0DNqPn86oB82hcyXp5oD7wBhiMK%2Bx5KS%2BzCx1MdIcsdUUIrbNgCle%2B3eom5ap0Ji0NTtINf2bs8NGRTxXnwuuGj05wO7R6L1QIzhefu4aKOv%2Bb%2Bq9dJ3BbaQCl5bTK0MJfB410WYAmlScKExZlXBRkvlo8Duvm3O0ZUPiaQtGreI6%2FEZssfSof9Eeb6bfDNnwnsR6rFhMusaHDaYulb01lJtbAc2OTkwVJ65llyyRT1lWRQcQCnDHwOseOhkmvtz9f%2FU0eTDkge4s0FzJ70FhBba%2BzJ87SAsKrEbdUoYNXDnYS5CE%2BIyrToMKdubx4bpd0%2Bxpsm5P9z0MAl4xb9WiuHJQ1%2Br8ynJS4hBdV4jLglXIwQT9Sv3zoma5KLwjATAEZz2s1n2M6ecC7WfPh9oUSDf2dbXXEcaUXz0%2FbvZ0UTfm7d2ekWodjGRHwUriiBR%2FbPT4WaFk2BI3qnTPEVO8GlEAEnkEWbExiAUwzsLOPviq1QT9lfNV4OhqsO%2BK%2B1eF67qV0drBbArb6Ytc7%2FOp51Tqv0WnwgqO15jkU%2BQ2MPKDo9QGOqUBFTnEqL8H0AIjwez7BANKVWA6snbYy%2B0GuC30nWMnuGRsR7o5xmeu0uLRqvaEKTyomRkEegWBb687ll9%2Fty9l5fM0h%2FnwGIFU0hw%2BVRweG%2F8CPj8bsUjtI44NsbvNptefiwSXeqHpO%2BmisQnO6RO90ddRCKoOQ4Ui3mH4qRkvrvOtmYvssAtm4DD1ng99oR%2BcChFVBFEmu0S2sGtHy8b2yfBo6xym&X-Amz-Signature=9ba7e4b2d0318ef109a6708e22312d304c0c402be90bf9800afe5e4746181988&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

I can now search within this directory for common files with

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery-content/Web-Content/common.txt  -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/cgi-bin/FUZZ
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/37effcbf-768e-40cd-9bc5-8544f17e3ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XL6YUMGC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222038Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBCRX7X9ISauAmfeaxjkgDLGIfs5n1nlsUoZpo9s5wAUAiEA%2Fk%2FbA%2B4gIijMb1OcltwHAqGShtTl6MXjbtpPfhAiD9UqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDpar%2Bevh%2FNpmSt5dSrcA6UK4SlioicJKxZ9M8stU0hNZ7vyq386Vd%2Fw0C0bEBsh28m3LWXrCop5Hqni2UH%2FNUSEwkT036u2Dw7ACed0DNqPn86oB82hcyXp5oD7wBhiMK%2Bx5KS%2BzCx1MdIcsdUUIrbNgCle%2B3eom5ap0Ji0NTtINf2bs8NGRTxXnwuuGj05wO7R6L1QIzhefu4aKOv%2Bb%2Bq9dJ3BbaQCl5bTK0MJfB410WYAmlScKExZlXBRkvlo8Duvm3O0ZUPiaQtGreI6%2FEZssfSof9Eeb6bfDNnwnsR6rFhMusaHDaYulb01lJtbAc2OTkwVJ65llyyRT1lWRQcQCnDHwOseOhkmvtz9f%2FU0eTDkge4s0FzJ70FhBba%2BzJ87SAsKrEbdUoYNXDnYS5CE%2BIyrToMKdubx4bpd0%2Bxpsm5P9z0MAl4xb9WiuHJQ1%2Br8ynJS4hBdV4jLglXIwQT9Sv3zoma5KLwjATAEZz2s1n2M6ecC7WfPh9oUSDf2dbXXEcaUXz0%2FbvZ0UTfm7d2ekWodjGRHwUriiBR%2FbPT4WaFk2BI3qnTPEVO8GlEAEnkEWbExiAUwzsLOPviq1QT9lfNV4OhqsO%2BK%2B1eF67qV0drBbArb6Ytc7%2FOp51Tqv0WnwgqO15jkU%2BQ2MPKDo9QGOqUBFTnEqL8H0AIjwez7BANKVWA6snbYy%2B0GuC30nWMnuGRsR7o5xmeu0uLRqvaEKTyomRkEegWBb687ll9%2Fty9l5fM0h%2FnwGIFU0hw%2BVRweG%2F8CPj8bsUjtI44NsbvNptefiwSXeqHpO%2BmisQnO6RO90ddRCKoOQ4Ui3mH4qRkvrvOtmYvssAtm4DD1ng99oR%2BcChFVBFEmu0S2sGtHy8b2yfBo6xym&X-Amz-Signature=670a9818385dbe290bb51790a717b2b701a492ccce8c2c4a026c6c56774179b1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Using Burp Professional

Go to the "Target" > "Site Map" tab. Right-click on the top-level entry for the lab and select "Engagement tools" > "Find comments". Notice that the home page contains an HTML comment that contains a link called "Debug". This points to `/cgi-bin/phpinfo.php`.

or Use the default options and start the content discovery. Burp quickly shows the `phpinfo.php` file in the site map:

Opening this file in the browser and scrolling through the content shows the answer:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/ebc3c145-2e85-4bdd-86c9-badcaff70ec6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XL6YUMGC%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222038Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBCRX7X9ISauAmfeaxjkgDLGIfs5n1nlsUoZpo9s5wAUAiEA%2Fk%2FbA%2B4gIijMb1OcltwHAqGShtTl6MXjbtpPfhAiD9UqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDpar%2Bevh%2FNpmSt5dSrcA6UK4SlioicJKxZ9M8stU0hNZ7vyq386Vd%2Fw0C0bEBsh28m3LWXrCop5Hqni2UH%2FNUSEwkT036u2Dw7ACed0DNqPn86oB82hcyXp5oD7wBhiMK%2Bx5KS%2BzCx1MdIcsdUUIrbNgCle%2B3eom5ap0Ji0NTtINf2bs8NGRTxXnwuuGj05wO7R6L1QIzhefu4aKOv%2Bb%2Bq9dJ3BbaQCl5bTK0MJfB410WYAmlScKExZlXBRkvlo8Duvm3O0ZUPiaQtGreI6%2FEZssfSof9Eeb6bfDNnwnsR6rFhMusaHDaYulb01lJtbAc2OTkwVJ65llyyRT1lWRQcQCnDHwOseOhkmvtz9f%2FU0eTDkge4s0FzJ70FhBba%2BzJ87SAsKrEbdUoYNXDnYS5CE%2BIyrToMKdubx4bpd0%2Bxpsm5P9z0MAl4xb9WiuHJQ1%2Br8ynJS4hBdV4jLglXIwQT9Sv3zoma5KLwjATAEZz2s1n2M6ecC7WfPh9oUSDf2dbXXEcaUXz0%2FbvZ0UTfm7d2ekWodjGRHwUriiBR%2FbPT4WaFk2BI3qnTPEVO8GlEAEnkEWbExiAUwzsLOPviq1QT9lfNV4OhqsO%2BK%2B1eF67qV0drBbArb6Ytc7%2FOp51Tqv0WnwgqO15jkU%2BQ2MPKDo9QGOqUBFTnEqL8H0AIjwez7BANKVWA6snbYy%2B0GuC30nWMnuGRsR7o5xmeu0uLRqvaEKTyomRkEegWBb687ll9%2Fty9l5fM0h%2FnwGIFU0hw%2BVRweG%2F8CPj8bsUjtI44NsbvNptefiwSXeqHpO%2BmisQnO6RO90ddRCKoOQ4Ui3mH4qRkvrvOtmYvssAtm4DD1ng99oR%2BcChFVBFEmu0S2sGtHy8b2yfBo6xym&X-Amz-Signature=8d26cc68085f3f8da2cc17448abbdff470b04da67155a43aa7345257bad13dc0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
