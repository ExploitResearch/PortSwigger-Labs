# Source code disclosure via backup files

### Goal - 

Identify and submit the database password, which is hard-coded in the leaked source code.

### Analysis/Exploitation -

When analyzing a web page, one of the first steps is always to check for the existence of a `robots.txt` file.

> 💡 It is a file that requests search engine crawlers to either include or exclude certain parts of the site from their index. Sometimes, interesting locations are revealed.It is up to the crawler whether they obey these wishes or ignore them.

In this case, it points straight to the subdirectory `/backup` 

> 💡 (other means to discover it would be tools like Burp Content Discovery, Ffuf, gobuster, wfuzz, ...)

Checking the directory shows a backup file for some Java code:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2b7b94a3-db1f-4203-b57b-00e330de07b6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YYUTNNB7%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222039Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDGBz4nd7nNIHiIgPV9JrKhVS5BAHr%2FKFEIDIhIc0A6AwIgRyGpgohSvNrnHiuYJhZaYbUumEfHWtzuGvVVO471QwYqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOGGCVhLrKyc5LuhXyrcA2yScn9wFSVfTp%2F1Oyz5FCgTeSEWsfKjJYAPNrc7H1rwDHLl2xgSOgfVSuXm%2F%2FCRGy01jkij5aTjEerLupCckaOaIj%2FwwdoqJ1he6u9gyeOjNM6OAvLLwOEUutVSCP7N91SiDweAp2rXKg7RCpM1zIcScm5H2NK%2BG%2B%2BGBcJQg0F1gsmF4O4U4O4utlJ2h%2FU47yYr3Fz06AL4CRbWqrl23GeoGtwNQgH4h9wWRh0MwIbQgzvHE5OozQ%2BTNOkAn4j88ZmnqgTBIWZnNM4oyiM65c5PvNpEU9UjUuYpwId5kDT3yuaig6eImR9xQG9RxCu1nm%2BXCaIt9N3v4TEiuf8GqDbVxxKmhdJTYfLUWrI4o59W9KHk%2FgsqBqa1%2FxnRIdPEo43D5agymTPt%2Fy76N55JWnhaPz1vSwDhcCGHAEg2Z0ZKjHqB1WakTlDaCP3DkBG9wuDZfPzm7skeOELRG7tbCY86is%2Fzx2ZdCmm6y9er6ZqkYgGBZaLxTGhL6%2B1GjNSUrCtxETlMSkHHVYIuv4bNhQ%2FV8W%2FXiw%2FpUC5mwshA0x6hjYK28wYUvOmpGrXK1ljs6P%2FkbLeVx7w7u%2FFnr%2FwaEgNkXX3hmUJvi2kiBmreR%2FSYAnhHj3Jyo34FKGlKMOmDo9QGOqUBDxwee0qyFfhSWuv0U%2FyleZgTga%2FAzPuwua8voLV33%2B05JSQgd71hPCF%2FNhV4QHCjFIqlQAGviiZJVQwzMMhVieSUWnR2OH1bPyrzAeEwXVowVngtLXTHI%2F1GZUVyeZekTY0cRIPpRgQS7ZUGiTUwDoYd6wSGKRTf%2Boy5LNoCFXGoQZlFeeUuv9rRCdJ90U8oo7CKA%2FQ1epnyJeeeyCDzyiTzqfsU&X-Amz-Signature=a158dc9c7980f457bd9cd217ba049bccc76190e5cd4d9402de707456efc3ea9f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the code, the credentials for the Postgres database connections can be found:

