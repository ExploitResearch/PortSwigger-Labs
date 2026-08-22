# Bypassing Referer-Based Validation

The HTTP Referrer header (which is inadvertently misspelled in the HTTP specification) is an optional request header that contains the URL of the web page that linked to the resource that is being requested. It is generally added automatically by browsers when a user triggers an HTTP request, including by clicking a link or submitting a form. Various methods exist that allow the linking page to withhold or modify the value of the Referer header. This is often done for privacy reasons.

The labs below demonstrate ways to bypass Referer header validation when
the application relies on the Referer header for CSRF protection.

## Labs

- [CSRF where Referer validation depends on header being present](./CSRF_where_Referer_validation_depends_on_header_being_present.md)
- [CSRF with broken Referer validation](./CSRF_with_broken_Referer_validation.md)
