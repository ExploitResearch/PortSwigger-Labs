# Source code disclosure via backup files

### Goal - 

Identify and submit the database password, which is hard-coded in the leaked source code.

### Analysis/Exploitation -

When analyzing a web page, one of the first steps is always to check for the existence of a `robots.txt` file.

> 💡 It is a file that requests search engine crawlers to either include or exclude certain parts of the site from their index. Sometimes, interesting locations are revealed.It is up to the crawler whether they obey these wishes or ignore them.

In this case, it points straight to the subdirectory `/backup` 

> 💡 (other means to discover it would be tools like Burp Content Discovery, Ffuf, gobuster, wfuzz, ...)

Checking the directory shows a backup file for some Java code:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2b7b94a3-db1f-4203-b57b-00e330de07b6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665NBQZSGI%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204731Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIF8ZGGKaNkHJGNbObHaYs1BniGtjS1%2Btg4qznl8yK0ZnAiBk3MJGhAQe6ClFQvKS4Y5VUijS3hJuabd08kqJGtKnXSqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMHy2V%2BSTGmPqD6VCKKtwDodg7CePIIeWr%2BIJVzG8ij2jywOyatPctdGUdXkmtPt3ufFsM0DZVXQ0h9xoA6%2Bcy6ZMnK23p%2FpczBisZVD8bTb53GPHcb%2F17VJiBcKscP%2BZ3fD1LIDR6EHfLoyXNJcPL4C2c4vQgxaYAc2d2q%2Fm6LE76tZjJkTgxd0jL7SyOxJIGy6cK4OU0Vsr1okDlh9XJTzrYtCtpxMibKefQfyIJXFEta9k3uBRRqk3ca1zoQQXJi6Vf6NZpOiDhGVVe%2B2WyXR4m74HZBtGbvCVYkNzUSimseF7Nafz%2Fo5OmDWb4haKdtKxe1enxvUsoBQo5%2BDleT1UGYgsBL4uIKp5KH5uEOLdrtGeaNCWq9N68kDhCg29gfJNyXJkDyIzgqj9WPkQP2ZPj9ruO5GqsxWTb0xc3h6wD7RPffn2mRdt2nQmkwMGSrMmrThzxH6x6dDmmEhEp1uixSiyDkQoo%2F%2BeXeEGAAdu3d02a1VJqA%2FVxfl6KCaR5f8O2tfl9KzVgxKLBKdPLmi8xtVEiIt1TurbzsIcVC7ikCh8PdEMWQXHCsBiOL7UE9QAPiN1B2NytsdTbABMitRGW3SiwP2%2BAS9MYTLyR5R3qJXa3gbE%2B432jSfeEOUJ8mx1jgbKJa%2BbfwEwwhcmi1AY6pgEGvu4Xt72zjBdXehCfQATZ4dZYVjB8tP6NfEG%2Farbrv6mYHhyaFMN1zxgeEZ0eJ%2F76TR3lavj4RIBe3eh093Nk0%2BtFw0BkZw2ri1YnTSOX5zo5mM%2FhDYJqY148Fx9a2Tl5u51kDNRyu4iLOd2CrVlbBRkltEV0cTNLnbNdErl3zOdXgNCk%2FWqupTpTwezC0aEOwUlCbAdEhn2xKDMyjJY1b%2FIt1rRH&X-Amz-Signature=cbc579f727468f03ac4adc140bd1d9bb8fa6c7ec2f49cdaa11034174ff2a6c6a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

In the code, the credentials for the Postgres database connections can be found:


