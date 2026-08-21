# Insecure direct object references

### Target Goal - 

find the password for the user `carlos`, and log into the account.

### Analysis/Exploitation -

- Select the **Live chat** tab.
- Send a message and then select **View transcript**.
**It’s sending a GET request to **`/download-transcript/2.txt`**! and we can see our own session’s transcript in response.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/43fe081c-ae5c-4bd3-938c-4c1e20dbf72b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46664U7LVPB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210352Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC9znQVZ%2FLejRlD8g0AGsr38637tRnBAK8X%2B0m3CBcwUQIgZV5qDIIGdzl63dwwqN0n9E3V6OBdBGe4zEjzTb8lzcMqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDH8mUuYW0QUeNw63TircA1J9AMSRIzkvtE1srLAD9hF9fbxLUKTQ%2BcATdkaY2KIKU5uA9q9Im0xiBhv%2BLvcQrSpuvGxBu9pJMWGrxVio1hDK%2BmD4IfoZb6GJLsKmVmt77r5v4BnvrwfM94wPGLT3KZxK%2FOtIbH7dquFONuiZMCArfx8C4%2FzPUrAM1yZvKtyFFGlwLVAQryEnN5hxreq%2FSLmqSn%2F%2Bh6z748sRIgT0wUMSn97HT5U4Pr15DM9t6HEu0VcyaG5DnQXOHP9hA3zdZWQ4uOrA815rTlbNYhONeORdu7irDnQJzcGtwENZwJUqyJ7CNPVLK41rt9QZUl8uwqUWPZ31gYweSWd29RoxCxCjDZFEk6KPt7Cb5y8fVOWZV7Pppm0cG4tPWsUgUxzOhM1vXqrC%2FCqH5SrnXScgy9S26Ki7A%2Bfoxgp8C1MQDLMXnm0hTvanJRWQK8nt1d%2BMnU7byZxctBy6WDatj3vLc42d07D9VzUELuHNh4iXA7D01tWf%2BbqwWFyRB%2FFwjEi%2FjExZ6hOkbWgKQXjYsx7MP9n5H%2Be2dzL3sEej5ihR6OHkEdwrnjNqn2iViyOgF7eG3yExsXQszk7N3qMuO4qNgJHBQDuqG7jUcvGSo9Xa2IqKWttjSZ1UHRTcLhwaMJHGotQGOqUBt%2BsKHmK0P8AVGjxBV4%2FqiFFMdoenBA1Hg4zztFHk6q%2FYkpuvK4ZVq0rSWE%2FzcGzuePQVfR59n%2FxPSZAqJLNZ7%2BsCtc7PzKZiFZBxbUA9kzQSt4WJLw5YGHcxx%2FvvC1YQiaCro%2BPuQBLQfYbzIDVzgK1JtAIGVzsZ1nloaHIffybiq01QtetAdYqi%2Fi34ejhpYTrJRrcI2DbXBCB9MPHDvOuFKpot&X-Amz-Signature=1019de376130b8db3f8de54e191b764f12d299bc1ff41116fb24bc0c8274de7e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**What if I change the **`2.txt`** to **`1.txt`** Or **`3.txt`**, and so on?**

Change the filename to `1.txt` and review the text. Notice a password within the chat transcript.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c2f0a595-8a0c-45e3-ab3e-1abdbd8020c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB46664U7LVPB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210352Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQC9znQVZ%2FLejRlD8g0AGsr38637tRnBAK8X%2B0m3CBcwUQIgZV5qDIIGdzl63dwwqN0n9E3V6OBdBGe4zEjzTb8lzcMqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDH8mUuYW0QUeNw63TircA1J9AMSRIzkvtE1srLAD9hF9fbxLUKTQ%2BcATdkaY2KIKU5uA9q9Im0xiBhv%2BLvcQrSpuvGxBu9pJMWGrxVio1hDK%2BmD4IfoZb6GJLsKmVmt77r5v4BnvrwfM94wPGLT3KZxK%2FOtIbH7dquFONuiZMCArfx8C4%2FzPUrAM1yZvKtyFFGlwLVAQryEnN5hxreq%2FSLmqSn%2F%2Bh6z748sRIgT0wUMSn97HT5U4Pr15DM9t6HEu0VcyaG5DnQXOHP9hA3zdZWQ4uOrA815rTlbNYhONeORdu7irDnQJzcGtwENZwJUqyJ7CNPVLK41rt9QZUl8uwqUWPZ31gYweSWd29RoxCxCjDZFEk6KPt7Cb5y8fVOWZV7Pppm0cG4tPWsUgUxzOhM1vXqrC%2FCqH5SrnXScgy9S26Ki7A%2Bfoxgp8C1MQDLMXnm0hTvanJRWQK8nt1d%2BMnU7byZxctBy6WDatj3vLc42d07D9VzUELuHNh4iXA7D01tWf%2BbqwWFyRB%2FFwjEi%2FjExZ6hOkbWgKQXjYsx7MP9n5H%2Be2dzL3sEej5ihR6OHkEdwrnjNqn2iViyOgF7eG3yExsXQszk7N3qMuO4qNgJHBQDuqG7jUcvGSo9Xa2IqKWttjSZ1UHRTcLhwaMJHGotQGOqUBt%2BsKHmK0P8AVGjxBV4%2FqiFFMdoenBA1Hg4zztFHk6q%2FYkpuvK4ZVq0rSWE%2FzcGzuePQVfR59n%2FxPSZAqJLNZ7%2BsCtc7PzKZiFZBxbUA9kzQSt4WJLw5YGHcxx%2FvvC1YQiaCro%2BPuQBLQfYbzIDVzgK1JtAIGVzsZ1nloaHIffybiq01QtetAdYqi%2Fi34ejhpYTrJRrcI2DbXBCB9MPHDvOuFKpot&X-Amz-Signature=0eb5b657e2264489668e408b61481c7ff38b9b9baa0eb4e6b416c89d60971f37&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It should be **user **`carlos`**’s password!**

Login as carlos with this password

