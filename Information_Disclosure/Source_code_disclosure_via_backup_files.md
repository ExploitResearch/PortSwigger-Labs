# Source code disclosure via backup files

### Goal - 

Identify and submit the database password, which is hard-coded in the leaked source code.

### Analysis/Exploitation -

When analyzing a web page, one of the first steps is always to check for the existence of a `robots.txt` file.

> 💡 It is a file that requests search engine crawlers to either include or exclude certain parts of the site from their index. Sometimes, interesting locations are revealed.It is up to the crawler whether they obey these wishes or ignore them.

In this case, it points straight to the subdirectory `/backup` 

> 💡 (other means to discover it would be tools like Burp Content Discovery, Ffuf, gobuster, wfuzz, ...)

Checking the directory shows a backup file for some Java code:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2b7b94a3-db1f-4203-b57b-00e330de07b6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665X3DIZGV%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215623Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDeUfr8CWixO4U7EWQlrxZpcfgGOXIYuRFV%2BzuuI3JLZgIgdsCz3uGS0N7a7kfHOZyOmXAMMODhR2dgbWTSe66p2W0qiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDCaUnxoU%2FTpun96N%2BircA6H4Svx0XYaC3YDDVVFBpfOhu%2BbEMsCi3TP0GW%2BBe3%2BLSlEn%2BV2j905DmlbNQcfi7av835QM51vgDyjWqGjIwRL7LezTgyMzGytvb40qdL1foH2VJiDWIaDR5ACp%2F2xMWxf0AS0Tb%2FwNWlJIMSzM6IuflitybRUtDSwQ1Cnd9ZOmiia%2FOMHwzIK%2FtsDBEQkRVxsvQf42a7TUhSUVhsNWhDsuvFUKUzYlFl2Wz3FiEPVhC6ls4urPoAk0FjrTsT5JufhK%2BA79vpf46MUbMcAZnNkJ%2BP%2BCCWFZwWMomb%2BesJlkKHWOXlRn9qEIrZiBpa3AM26XzNIbegrsVl7pOAWo8K4JjNOqbGzBDHRe34xIQmnmwAn8pr0g3fmV6Xhrx7PvE57H7xI0JxMCMg3jAw9wUkB%2B%2BLxnEUvJnM4cVpn8185bcnbe%2BvI1b4YHgXrGA2mn3g2h8zgQv9ZOXyRniBUp81yC8rkkDV1%2BuSrFlIFPsew2BruCcFztadTFI6DQMvavi%2BNT8Tb%2B27v47uZDpFYN1kyUjHucx1TMg%2BbIVfz2IeExljadH9sswz3CJBtXmco02Tphtq6w3TJHuNGTIYca33ZDZ9JEwe27nCVZPdXC8CzrKSSppaBuHUgV9O2LMMqDo9QGOqUBc62MzwUYMSEVL8cIx0ad2R4J0qWrbajL3FtMXvpsyfo3LhLpffvM3tuZGHYKwbRJnBKX%2FyyyUSpP1N4FykJtEcaNmIJ2zO6WmkyXT2E7EjgBqnMvPO5g7E0VMWCAWWIbcT4u0mZexpFOSC6NM0NZi2heo2gwuAdzHmFDM0%2FKnF097N3HtHtbMoh2hD3eIRn01NVcN0S%2BcPwd5epfvrdP8jqyQarp&X-Amz-Signature=bae04558c862e361f98d0eac0775cc69b19b8e8d04a1556358f451d2209baace&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the code, the credentials for the Postgres database connections can be found:

