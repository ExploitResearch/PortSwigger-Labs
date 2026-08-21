# Authentication bypass via flawed state machine

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

What immediately jumps to attention is that the login is a two-stage process. After providing the username and the password, I can select the role I want to login as:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8f85723a-9796-4bce-8951-94eb87058afa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q32ILCQW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHEcY7Zoj2wm%2Fg1uB0em1c%2B20iUeTsrlN48CZIPf3157AiAkl8iFbLQk7eRHVn85%2BHHzgCrlYmZvqGMs5HP13qGGjSqIBAit%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMynHmTavss3YpbJWxKtwDnc%2BKLltPDMwUc70snJ%2BKAaq0IkJENBSlmBoEEMzhkwwhPhgkQP23ssDWN48100q3MV2qR6w9soFJ8NIUYDSP%2BPOrdVFdggVwOmGWhJ5O1iKiU48PmeZ6sQWuuuA%2FFloeuvzCl90488NzWe96K97b6LHCIR5bJUyCKFt%2FqXJvJYkuYCxRO4tdKZFL14m4dj8fDdoU8HLWu%2FQXjPMUPgtQiAHdtbpkIbEbbitiqdYTgRFRGn90Oc3RwmoOVYS9RgSiNYIKANVBamWi5cb6bSkFZxvRdjmpZZG2m7a0gz%2B2W2RxCz5wioGVTXmcVfc7ulndcM4ohlwXZ349Ip4Rccg1PePROltaHONKMm8n0lqX51HfgN1ZBfr5UfwsJtsXcwHPw1%2BnvXWPNMRYM66DZs3GL2yTSB6ND6QD7er3xqGY8SPQdqbMrqobk9MUKJlc1ItGHrXu4qWOYYel21O%2Bu1LGPocF7fIeEStj7kjpquSpehQ9ZjKlOr4lPgZAG0f%2BbnD2YvpshOynPuBMCu%2F7NT9v%2FiG4RtyBIZhmGMWar7wGuMBxGMfrzktuqBYNKD%2FGNrlGGFOOxTbom0iytOJmoz%2FeCQajQAPPafGpL9A95G2kg6SOxl9cSADJY3Lu87QwwtOi1AY6pgEEuykhSSOC26uQepgb%2FwWZDfzVPX%2FA8gCaFk0xTGB%2Bq3k9GgODPRbe0L2FhF6jaOZVLBcSTltT73SbwQeLW4f06bLt%2FrZ%2FbxukThNVkruGlOj8kTlTF4lhEbAzpCVEYSgbHXiGnOGyFJkpBH0yjGAEfCYVWhWEv%2BIqThjP0rOoJDOYFFmZkivY3h%2B%2BdRIFo5yBkg56CQHazEv1I5q%2FXK4g1UUjfM%2FL&X-Amz-Signature=53cf753495e3aad5cbf33970cd57924c974451c922f0fdef4fba370085a00255&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Such an option does make sense. It allows users with higher privileges to restrict their permissions when they don't need them. This reduces both the attack surface during everyday activities as well as the risk of stupid and expensive mistakes. At least, if done properly. Having two dedicated accounts for this is both easier and less error-prone.

I select `user` and have a look at the `/role-selector` request in Burp Proxy:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7f5f1009-20d2-4c5a-a7c3-e6801b35ad10/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q32ILCQW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHEcY7Zoj2wm%2Fg1uB0em1c%2B20iUeTsrlN48CZIPf3157AiAkl8iFbLQk7eRHVn85%2BHHzgCrlYmZvqGMs5HP13qGGjSqIBAit%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMynHmTavss3YpbJWxKtwDnc%2BKLltPDMwUc70snJ%2BKAaq0IkJENBSlmBoEEMzhkwwhPhgkQP23ssDWN48100q3MV2qR6w9soFJ8NIUYDSP%2BPOrdVFdggVwOmGWhJ5O1iKiU48PmeZ6sQWuuuA%2FFloeuvzCl90488NzWe96K97b6LHCIR5bJUyCKFt%2FqXJvJYkuYCxRO4tdKZFL14m4dj8fDdoU8HLWu%2FQXjPMUPgtQiAHdtbpkIbEbbitiqdYTgRFRGn90Oc3RwmoOVYS9RgSiNYIKANVBamWi5cb6bSkFZxvRdjmpZZG2m7a0gz%2B2W2RxCz5wioGVTXmcVfc7ulndcM4ohlwXZ349Ip4Rccg1PePROltaHONKMm8n0lqX51HfgN1ZBfr5UfwsJtsXcwHPw1%2BnvXWPNMRYM66DZs3GL2yTSB6ND6QD7er3xqGY8SPQdqbMrqobk9MUKJlc1ItGHrXu4qWOYYel21O%2Bu1LGPocF7fIeEStj7kjpquSpehQ9ZjKlOr4lPgZAG0f%2BbnD2YvpshOynPuBMCu%2F7NT9v%2FiG4RtyBIZhmGMWar7wGuMBxGMfrzktuqBYNKD%2FGNrlGGFOOxTbom0iytOJmoz%2FeCQajQAPPafGpL9A95G2kg6SOxl9cSADJY3Lu87QwwtOi1AY6pgEEuykhSSOC26uQepgb%2FwWZDfzVPX%2FA8gCaFk0xTGB%2Bq3k9GgODPRbe0L2FhF6jaOZVLBcSTltT73SbwQeLW4f06bLt%2FrZ%2FbxukThNVkruGlOj8kTlTF4lhEbAzpCVEYSgbHXiGnOGyFJkpBH0yjGAEfCYVWhWEv%2BIqThjP0rOoJDOYFFmZkivY3h%2B%2BdRIFo5yBkg56CQHazEv1I5q%2FXK4g1UUjfM%2FL&X-Amz-Signature=43cbd6f6177bdec30dea41496202d7e818fdb45855b1f540e384ccd14f2ed387&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Attempt 1: Adjust role

The second login stage contains the user role. The roles available to me are listed on the page. I don't know whether another check is done during the POST of this form.

What happens if I change the role to 'admin' or 'administrator'? Of course, I don't know the role names, but it is worth a try.

Unfortunately, this does not lead to anything, neither error nor more privileges. This indicates that on processing that POST, it validates against allowed roles and defaults to something that is not admin.

### Attempt 2: Drop request

Speaking about defaulting, what happens if the full second request is dropped? Common sense would indicate that the session is dropped if any request is made before the second stage is finished. Easy to find out.

Using Burp proxy I log in with `wiener:peter` but drop the `GET` request to `/role-selector` completely. Afterwards, then manually browse to `/my-account`. Observe that role has defaulted to the `administrator` role and have access to the admin panel.           

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/aa7cb002-4763-4034-85ee-5c15a07d2fd1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466Q32ILCQW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHEcY7Zoj2wm%2Fg1uB0em1c%2B20iUeTsrlN48CZIPf3157AiAkl8iFbLQk7eRHVn85%2BHHzgCrlYmZvqGMs5HP13qGGjSqIBAit%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMynHmTavss3YpbJWxKtwDnc%2BKLltPDMwUc70snJ%2BKAaq0IkJENBSlmBoEEMzhkwwhPhgkQP23ssDWN48100q3MV2qR6w9soFJ8NIUYDSP%2BPOrdVFdggVwOmGWhJ5O1iKiU48PmeZ6sQWuuuA%2FFloeuvzCl90488NzWe96K97b6LHCIR5bJUyCKFt%2FqXJvJYkuYCxRO4tdKZFL14m4dj8fDdoU8HLWu%2FQXjPMUPgtQiAHdtbpkIbEbbitiqdYTgRFRGn90Oc3RwmoOVYS9RgSiNYIKANVBamWi5cb6bSkFZxvRdjmpZZG2m7a0gz%2B2W2RxCz5wioGVTXmcVfc7ulndcM4ohlwXZ349Ip4Rccg1PePROltaHONKMm8n0lqX51HfgN1ZBfr5UfwsJtsXcwHPw1%2BnvXWPNMRYM66DZs3GL2yTSB6ND6QD7er3xqGY8SPQdqbMrqobk9MUKJlc1ItGHrXu4qWOYYel21O%2Bu1LGPocF7fIeEStj7kjpquSpehQ9ZjKlOr4lPgZAG0f%2BbnD2YvpshOynPuBMCu%2F7NT9v%2FiG4RtyBIZhmGMWar7wGuMBxGMfrzktuqBYNKD%2FGNrlGGFOOxTbom0iytOJmoz%2FeCQajQAPPafGpL9A95G2kg6SOxl9cSADJY3Lu87QwwtOi1AY6pgEEuykhSSOC26uQepgb%2FwWZDfzVPX%2FA8gCaFk0xTGB%2Bq3k9GgODPRbe0L2FhF6jaOZVLBcSTltT73SbwQeLW4f06bLt%2FrZ%2FbxukThNVkruGlOj8kTlTF4lhEbAzpCVEYSgbHXiGnOGyFJkpBH0yjGAEfCYVWhWEv%2BIqThjP0rOoJDOYFFmZkivY3h%2B%2BdRIFo5yBkg56CQHazEv1I5q%2FXK4g1UUjfM%2FL&X-Amz-Signature=732b0c5715a364744ff13b7444cf3124444e0de7f0c9c5247d128b9fbc55b8b3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Now simply go to the Admin panel and use the link to delete user `carlos`. 

