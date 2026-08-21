# Authentication bypass via flawed state machine

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

What immediately jumps to attention is that the login is a two-stage process. After providing the username and the password, I can select the role I want to login as:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8f85723a-9796-4bce-8951-94eb87058afa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S65DSKMW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222029Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBCpxvLNSMs1krW2Jtdizib%2Fx9IYXg86OHx95UBGm%2BA6AiEA1bs9PULkRd0EGEs0vpa5bZ%2BTBeHfOhCHIshWsoosyrIqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAFGPowxMA0tJA5G2yrcAwYKoVgIUl6Fwvl0nhcT3D0B5ZO9%2Bv7D3CgHt3xxh3moGs2IFPTBnZpm3PjJ4LMe%2FtjD9%2FiqrLMu7vycH3EyZRNo4lm9pZxlEqlXfuI7Cr9w0DB%2BUdi4%2BaD5Z8qsFo8n9q%2BILqqD3SYyS2QQziFBJP54vAWkRS0GvtfOYckCexpPWLV3%2BL81zY0FwcBXjpVa1OZVYr5uOWOZPUgKxgAOm82wmUJbcw0wldoxm7mj83Zu5I1AX5oTlIA6UQ%2BtFHQdPT1mRoPo8NSyYDV%2Bhj7PUWnKsLXFYMxM8fUquGFTukc%2Fu4L8BnjcVNBeVrokKfuorV7PZD3m10EdwuyFDizHopAStyfh%2BdK%2FIsbkg7UnFAcjugVHiYBvhiRtshF5%2FnhOBrd1s3%2BOiObUfX6IcdPVCI81aq9x9P8GSX5XBOs5qi6XGtrok%2FDG%2BD7pXjKZkVe4c0tabs32vREa5QQAPY6pTmKJcYiLfWeyvweMGgNmq3UgenN4Dy%2Fx2A6SHwWUkME%2BPhnfDcUbh9Rm%2BuD%2BzWCgCkTVHLGjhNj6OBra8Kn0t5QRKOkbKqk3zyhAr9nIVBbdczxjIEOC9NaEGxRnH9K1MkFtzHk%2B2AVEaVfPKA%2Bb%2B%2BaYMuw23UQdrQB%2B5%2BQCMMuDo9QGOqUBEXT0G9YwGV7P%2Ft0T%2FGI%2FMi0cUFqWr%2Byn8zA%2F7rOyG9Us1pcZ1N8QN2jkRZlwqXw6rfYWZoAdKiSccj2OFr8cG5IWm6lqH0sAW2pQGFf7%2F%2FWZOeNWO%2B%2BfADrxg9l1hvy8pA08Eddp3PGJ55PVhD2Oxvzhfc%2F6jy0vGSik2LXcfCSwHu9x1x3QG%2BdUXHmV7%2FIRBwtDHl0JZd3yfS%2BcCbFrQgIMFqbm&X-Amz-Signature=fe0c658e7923cf0276f16e07b2aa87d0004c7f4b7d19b40e48a8b2c790ac789f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Such an option does make sense. It allows users with higher privileges to restrict their permissions when they don't need them. This reduces both the attack surface during everyday activities as well as the risk of stupid and expensive mistakes. At least, if done properly. Having two dedicated accounts for this is both easier and less error-prone.

I select `user` and have a look at the `/role-selector` request in Burp Proxy:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7f5f1009-20d2-4c5a-a7c3-e6801b35ad10/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S65DSKMW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222029Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBCpxvLNSMs1krW2Jtdizib%2Fx9IYXg86OHx95UBGm%2BA6AiEA1bs9PULkRd0EGEs0vpa5bZ%2BTBeHfOhCHIshWsoosyrIqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAFGPowxMA0tJA5G2yrcAwYKoVgIUl6Fwvl0nhcT3D0B5ZO9%2Bv7D3CgHt3xxh3moGs2IFPTBnZpm3PjJ4LMe%2FtjD9%2FiqrLMu7vycH3EyZRNo4lm9pZxlEqlXfuI7Cr9w0DB%2BUdi4%2BaD5Z8qsFo8n9q%2BILqqD3SYyS2QQziFBJP54vAWkRS0GvtfOYckCexpPWLV3%2BL81zY0FwcBXjpVa1OZVYr5uOWOZPUgKxgAOm82wmUJbcw0wldoxm7mj83Zu5I1AX5oTlIA6UQ%2BtFHQdPT1mRoPo8NSyYDV%2Bhj7PUWnKsLXFYMxM8fUquGFTukc%2Fu4L8BnjcVNBeVrokKfuorV7PZD3m10EdwuyFDizHopAStyfh%2BdK%2FIsbkg7UnFAcjugVHiYBvhiRtshF5%2FnhOBrd1s3%2BOiObUfX6IcdPVCI81aq9x9P8GSX5XBOs5qi6XGtrok%2FDG%2BD7pXjKZkVe4c0tabs32vREa5QQAPY6pTmKJcYiLfWeyvweMGgNmq3UgenN4Dy%2Fx2A6SHwWUkME%2BPhnfDcUbh9Rm%2BuD%2BzWCgCkTVHLGjhNj6OBra8Kn0t5QRKOkbKqk3zyhAr9nIVBbdczxjIEOC9NaEGxRnH9K1MkFtzHk%2B2AVEaVfPKA%2Bb%2B%2BaYMuw23UQdrQB%2B5%2BQCMMuDo9QGOqUBEXT0G9YwGV7P%2Ft0T%2FGI%2FMi0cUFqWr%2Byn8zA%2F7rOyG9Us1pcZ1N8QN2jkRZlwqXw6rfYWZoAdKiSccj2OFr8cG5IWm6lqH0sAW2pQGFf7%2F%2FWZOeNWO%2B%2BfADrxg9l1hvy8pA08Eddp3PGJ55PVhD2Oxvzhfc%2F6jy0vGSik2LXcfCSwHu9x1x3QG%2BdUXHmV7%2FIRBwtDHl0JZd3yfS%2BcCbFrQgIMFqbm&X-Amz-Signature=573903808a5a3f339f55aeb2282cd85a6b259f3979fbc366c97b0304410d813b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Attempt 1: Adjust role

The second login stage contains the user role. The roles available to me are listed on the page. I don't know whether another check is done during the POST of this form.

What happens if I change the role to 'admin' or 'administrator'? Of course, I don't know the role names, but it is worth a try.

Unfortunately, this does not lead to anything, neither error nor more privileges. This indicates that on processing that POST, it validates against allowed roles and defaults to something that is not admin.

### Attempt 2: Drop request

Speaking about defaulting, what happens if the full second request is dropped? Common sense would indicate that the session is dropped if any request is made before the second stage is finished. Easy to find out.

Using Burp proxy I log in with `wiener:peter` but drop the `GET` request to `/role-selector` completely. Afterwards, then manually browse to `/my-account`. Observe that role has defaulted to the `administrator` role and have access to the admin panel.           

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa7cb002-4763-4034-85ee-5c15a07d2fd1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466S65DSKMW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T222029Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIBCpxvLNSMs1krW2Jtdizib%2Fx9IYXg86OHx95UBGm%2BA6AiEA1bs9PULkRd0EGEs0vpa5bZ%2BTBeHfOhCHIshWsoosyrIqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDAFGPowxMA0tJA5G2yrcAwYKoVgIUl6Fwvl0nhcT3D0B5ZO9%2Bv7D3CgHt3xxh3moGs2IFPTBnZpm3PjJ4LMe%2FtjD9%2FiqrLMu7vycH3EyZRNo4lm9pZxlEqlXfuI7Cr9w0DB%2BUdi4%2BaD5Z8qsFo8n9q%2BILqqD3SYyS2QQziFBJP54vAWkRS0GvtfOYckCexpPWLV3%2BL81zY0FwcBXjpVa1OZVYr5uOWOZPUgKxgAOm82wmUJbcw0wldoxm7mj83Zu5I1AX5oTlIA6UQ%2BtFHQdPT1mRoPo8NSyYDV%2Bhj7PUWnKsLXFYMxM8fUquGFTukc%2Fu4L8BnjcVNBeVrokKfuorV7PZD3m10EdwuyFDizHopAStyfh%2BdK%2FIsbkg7UnFAcjugVHiYBvhiRtshF5%2FnhOBrd1s3%2BOiObUfX6IcdPVCI81aq9x9P8GSX5XBOs5qi6XGtrok%2FDG%2BD7pXjKZkVe4c0tabs32vREa5QQAPY6pTmKJcYiLfWeyvweMGgNmq3UgenN4Dy%2Fx2A6SHwWUkME%2BPhnfDcUbh9Rm%2BuD%2BzWCgCkTVHLGjhNj6OBra8Kn0t5QRKOkbKqk3zyhAr9nIVBbdczxjIEOC9NaEGxRnH9K1MkFtzHk%2B2AVEaVfPKA%2Bb%2B%2BaYMuw23UQdrQB%2B5%2BQCMMuDo9QGOqUBEXT0G9YwGV7P%2Ft0T%2FGI%2FMi0cUFqWr%2Byn8zA%2F7rOyG9Us1pcZ1N8QN2jkRZlwqXw6rfYWZoAdKiSccj2OFr8cG5IWm6lqH0sAW2pQGFf7%2F%2FWZOeNWO%2B%2BfADrxg9l1hvy8pA08Eddp3PGJ55PVhD2Oxvzhfc%2F6jy0vGSik2LXcfCSwHu9x1x3QG%2BdUXHmV7%2FIRBwtDHl0JZd3yfS%2BcCbFrQgIMFqbm&X-Amz-Signature=c132147f9408544a5fa8011d55be9efc830e633ec1c494a0d4da9feb71233392&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now simply go to the Admin panel and use the link to delete user `carlos`. 
