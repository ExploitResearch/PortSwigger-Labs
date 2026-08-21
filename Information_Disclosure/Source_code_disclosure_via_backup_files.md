# Source code disclosure via backup files

### Goal - 

Identify and submit the database password, which is hard-coded in the leaked source code.

### Analysis/Exploitation -

When analyzing a web page, one of the first steps is always to check for the existence of a `robots.txt` file.

> 💡 It is a file that requests search engine crawlers to either include or exclude certain parts of the site from their index. Sometimes, interesting locations are revealed.It is up to the crawler whether they obey these wishes or ignore them.

In this case, it points straight to the subdirectory `/backup` 

> 💡 (other means to discover it would be tools like Burp Content Discovery, Ffuf, gobuster, wfuzz, ...)

Checking the directory shows a backup file for some Java code:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2b7b94a3-db1f-4203-b57b-00e330de07b6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466474DY2QX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210456Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC6r7%2Ft7cmbqroLi2HBxgOLNw4p9Wu1pHSpof1%2BVO3fnAIhANiOJJh8dNwm%2F86%2BK5TPCi%2BGcNTpgWqa8kVk%2F6aKak9bKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxFtpQF0Xm9uJ6m2nAq3AMJuaEF1%2Fa7bdbQoWHXK6W52DjZH7CMMODzGvkgJNBr0WhryCnaEhorwjjh39V97lANce5MSEuXOacbOuI2lnQZ3B%2B%2Fl8i6y0GBmcf4ohfaBBDMrFJeUlBRJAtCwtOB15siYa2sMVonK5shRShHgbdbFe2uMhW%2BjYoc0x7eXrKYhcAi4q1wK4neeedirs0yDgftkEqBRZtDdtHPp0O44xmXhiYSfWuMHLFBqlGRFG%2FEpuTRjVY2XPw4m79tKN3%2B6q8BosZleLAy2JUYybKI6T3nFj6GG1diP1bvb33M7PzbqQa162zcaJH0mCFQHXLbIuUQs14H1xD305fCqZkbIl%2BC84NpDNnPr%2FgAkPGVRslhGy3TjyfEQoV%2FC9GhNQTXSLZNN7PladJ%2FWUefRbUS%2Fth1BCBTn7EPCxUq729ksHoiNaF1oWTW%2BoBm4fDhENuGEf1mbPOEF0DUAy%2BwqxRp3n1HASHJ0tX6c5Aip9Fd%2BJBE%2BDC1tMIzrHTA9C6l6N%2B0YnotZiq0qBH3wuAHYpRRg2z7WfbYYuewuAYIMvbAMvS9%2BZV8AzzDUzCfhNn2i2g0Gw4Y2jJpZYJmtlMD8l7pKunpE4OqDO7Bw22dR%2Bejzvz1bUejwefUvDx6%2B8%2FDODDVyaLUBjqkAZd4q1T1fJnLh%2B%2BYLG36GTRq4Eh0m6bthV55CHZ0gZ%2FujBHgOpwXsYillVlzxAD4X5LqMgdzlknDj8Uk1p0UfMuILTeQCONi233Wf2ZYDu4WHmvw32Xmus6zO5OPZ2Y2voRsdboeH3fQmDcJQ4mZPoZ8St%2Bum5mLYZQcllqgq2Ivdv0rTqEOUTeR2bdZFanm8y2djZG56nHDVLroyWb7e%2Bc4I1Yr&X-Amz-Signature=1a5889b89677a21dcf7259fdb940860ce5c115028af65bc464625148ec5b990a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the code, the credentials for the Postgres database connections can be found:


