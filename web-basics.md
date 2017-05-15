Table of Contents
=================

   * [URL](#url)
      * [URL Format](#url-format)
         * [Fragment](#fragment)
      * [URL vs URI](#url-vs-uri)
      * [I18N URL](#i18n-url)
         * [When to encode](#when-to-encode)
      * [References](#references)

# URL

## URL Format

```
scheme:[//[user:password@]host[:port]][/]path[?query][#fragment]
```

### Fragment

Clients are not supposed to send the fragment to servers when retrieving resources. The fragment is processed exclusively _client-side_.

## URL vs URI

URLs are a subset of URIs. A URL implies the means to access an indicated resource, which is not true of every URI.

## I18N URL

* **Domain**: use [International Domain Name](https://en.wikipedia.org/wiki/Internationalized_domain_name) (IDN) with [_Punycode_](https://en.wikipedia.org/wiki/Punycode)
* **Path**: use [_percent-encoding_](https://en.wikipedia.org/wiki/Percent-encoding)

### When to encode

| Classification    | Included characters     | Encoding required? |
|----|----|-----|
| Safe characters          | Alphanumerics [0-9a-zA-Z], special characters ``$-_.+!*'(),,`` and reserved characters used for their reserved purposes (e.g., question mark used to denote a query string) | NO                 |
| ASCII Control characters | Includes the ISO-8859-1 (ISO-Latin) character ranges 00-1F hex (0-31 decimal) and 7F (127 decimal.)                                                                     | YES                |
| Non-ASCII characters     | Includes the entire “top half” of the ISO-Latin set 80-FF hex (128-255 decimal.)                                                                                        | YES                |
| Reserved characters      | ``; / ? : @ = &`` (does not include blank space)                                                                                                                            | YES (*)             |
| Unsafe characters        | Includes the blank/empty space and ``" < > # % { } | \ ^ ~ [ ] ```                                                                                                          | YES                |

* Note: Reserved characters only need encoding when not used for their defined, reserved purposes.

## References

- https://tools.ietf.org/html/rfc3986
- https://en.wikipedia.org/wiki/Uniform_Resource_Locator

# HTTP

- https://frontendmasters.gitbooks.io/front-end-handbook-2017/content/learning/http-networks.html
- https://code.tutsplus.com/tutorials/http-succinctly-http-connections--net-33707
- https://code.tutsplus.com/tutorials/http-the-protocol-every-web-developer-must-know-part-1--net-31177
- http://chimera.labs.oreilly.com/books/1230000000545/index.html

## HTTP Verbs

TRACE: main purpose is for debuging HTTP protocol. When a TRACE request is sent to a server, the server simply echoes back the original request.

## HTTP Codes

- 1xx Hold on
- 2xx Here you go
- 3xx Go away
- 4xx You fucked up
- 5xx I fucked up

# Cookies

http://erik.io/blog/2014/03/04/definitive-guide-to-cookie-domains/

# General resources

- https://developers.google.com/web/fundamentals/
