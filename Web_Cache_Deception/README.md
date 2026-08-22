# Web Cache Deception

Web cache deception is an attack where an attacker tricks a caching server into caching sensitive, user-specific content that should not be cached. By manipulating URL paths, the attacker causes the cache server to serve another user's private data from the cache.

The attack exploits differences in how the cache server and the origin server interpret URL paths. For example, the cache might treat `/account.php/foo.css` as a static CSS file and cache it, while the origin server ignores the path suffix and serves the dynamic `/account.php` content.

## Labs

- [Exploiting cache server normalization for web cache deception](./Exploiting_cache_server_normalization_for_web_cache_deception.md)
- [Exploiting exact-match cache rules for web cache deception](./Exploiting_exact-match_cache_rules_for_web_cache_deception.md)
- [Exploiting origin server normalization for web cache deception](./Exploiting_origin_server_normalization_for_web_cache_deception.md)
- [Exploiting path delimiters for web cache deception](./Exploiting_path_delimiters_for_web_cache_deception.md)
- [Exploiting path mapping for web cache deception](./Exploiting_path_mapping_for_web_cache_deception.md)
