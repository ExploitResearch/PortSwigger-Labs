# Insecure direct object references

### Target Goal - 

find the password for the user `carlos`, and log into the account.

### Analysis/Exploitation -

- Select the **Live chat** tab.
- Send a message and then select **View transcript**.

**It’s sending a GET request to **`/download-transcript/2.txt`**! and we can see our own session’s transcript in response.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/43fe081c-ae5c-4bd3-938c-4c1e20dbf72b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WUA37QD3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215519Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqrkHWqiRNUm%2F6WUgtAE0MmbN2da9%2Fhsry0BAobEw2ZwIge5si%2Bn%2FgZjG2kAuGst1eRQbinyyneliI644dZQ459XMqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJvIR02JewNCAeAVfircAxeznl3IcPC%2Bk5TKF6wYkrB1J2bzPvNg%2BjB3f35v8DB39gzmUqsymeRSVIph605%2Be%2FQlNDFTXsmxkBM6Ezs6OhcOyXrtUJIgNYGgD2EBEfbwbFXavOEHO9rp1FFczlCJHmROE2ILKjjRv8JSc8RZQApRPuj8rXoV5M5HptYp%2FtZIv%2FnyuVdUWWyhrmWlgqc3buZGs%2FmywDlUGQhMLIzDZTzBftYipd1bi7ETbQB3y2dUlKRs2VdH2ng7gSENBuINjnThM2WgGAVwxvvB7Z%2FLGcSvmTYlT5cGK%2BlLeJcpEj0SRHt6%2F1DLIaii31HrMj0%2FspPn4SRz97X37UJ1nfBm5V5ozIeLy2O8O%2FFeoWzhifPvKkH2W0E6Djusc18qfqLwtio3ByrROvw8pWWOjGPPCI1hsSIpdLssV%2BErxng3xDvz%2FVB%2BnkYgCMFM3SyODy3KQ8Y1CHfN1B1OYle3YorYn%2BkJdYHux6iPs3ldsShwbPHOyjrZN5VknzlB9C70DUn2TOmQ%2BkrtA2%2B3fFgChhKyqIH2Aq89%2Bkw98w7FU7m3aOmAWixctdbOuCDmU7l7CKNNjwA2jD%2FS7RGhsO96lNMf43HNtpKJ2B0cBVj3oGiz7WSmJivwGPJi8OcO6t9EMIqHo9QGOqUBrrX6rFLthD82tJKaGtFoiNasuUz%2Fq5ajafNV2lpsY%2FjSW0HbICl1eCbZQh5ma0loo2%2FjqfdFVermqb8KSLJvrHsPL8OWrwRdAHP2nRMBfIHoGSdrj1wqsJICgkdut7b%2FE4IM4mUHK1UXUuhiqsFqSUnfd1MJkQnYn8dC1QrH9mvuAkEclJKLjwxSVYWZrLvDRILAAGsWD0KAn1j%2BklIWlYly5z9A&X-Amz-Signature=31f472dce1a62023fb2e6fca7401f007f88672d1513314b90e472ecd834e299d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**What if I change the **`2.txt`** to **`1.txt`** Or **`3.txt`**, and so on?**

Change the filename to `1.txt` and review the text. Notice a password within the chat transcript.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c2f0a595-8a0c-45e3-ab3e-1abdbd8020c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WUA37QD3%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215519Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqrkHWqiRNUm%2F6WUgtAE0MmbN2da9%2Fhsry0BAobEw2ZwIge5si%2Bn%2FgZjG2kAuGst1eRQbinyyneliI644dZQ459XMqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDJvIR02JewNCAeAVfircAxeznl3IcPC%2Bk5TKF6wYkrB1J2bzPvNg%2BjB3f35v8DB39gzmUqsymeRSVIph605%2Be%2FQlNDFTXsmxkBM6Ezs6OhcOyXrtUJIgNYGgD2EBEfbwbFXavOEHO9rp1FFczlCJHmROE2ILKjjRv8JSc8RZQApRPuj8rXoV5M5HptYp%2FtZIv%2FnyuVdUWWyhrmWlgqc3buZGs%2FmywDlUGQhMLIzDZTzBftYipd1bi7ETbQB3y2dUlKRs2VdH2ng7gSENBuINjnThM2WgGAVwxvvB7Z%2FLGcSvmTYlT5cGK%2BlLeJcpEj0SRHt6%2F1DLIaii31HrMj0%2FspPn4SRz97X37UJ1nfBm5V5ozIeLy2O8O%2FFeoWzhifPvKkH2W0E6Djusc18qfqLwtio3ByrROvw8pWWOjGPPCI1hsSIpdLssV%2BErxng3xDvz%2FVB%2BnkYgCMFM3SyODy3KQ8Y1CHfN1B1OYle3YorYn%2BkJdYHux6iPs3ldsShwbPHOyjrZN5VknzlB9C70DUn2TOmQ%2BkrtA2%2B3fFgChhKyqIH2Aq89%2Bkw98w7FU7m3aOmAWixctdbOuCDmU7l7CKNNjwA2jD%2FS7RGhsO96lNMf43HNtpKJ2B0cBVj3oGiz7WSmJivwGPJi8OcO6t9EMIqHo9QGOqUBrrX6rFLthD82tJKaGtFoiNasuUz%2Fq5ajafNV2lpsY%2FjSW0HbICl1eCbZQh5ma0loo2%2FjqfdFVermqb8KSLJvrHsPL8OWrwRdAHP2nRMBfIHoGSdrj1wqsJICgkdut7b%2FE4IM4mUHK1UXUuhiqsFqSUnfd1MJkQnYn8dC1QrH9mvuAkEclJKLjwxSVYWZrLvDRILAAGsWD0KAn1j%2BklIWlYly5z9A&X-Amz-Signature=8832ec0288bb44e2a6d5d1d53c47813c8a9070966975049a969cbda2fcfd1c80&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It should be **user **`carlos`**’s password!**

Login as carlos with this password
