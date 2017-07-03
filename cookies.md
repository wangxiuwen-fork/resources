https://curl.haxx.se/rfc/cookie_spec.html

https://www.ietf.org/rfc/rfc2109.txt : 

4.3.1  Interpreting Set-Cookie

The user agent keeps separate track of state information that arrives via Set-Cookie response headers from each origin server (as
distinguished by name or IP address and port).  The user agent applies these defaults for optional attributes that are missing:

- `Version` Defaults to "old cookie" behavior as originally specified by Netscape.  See the HISTORICAL section.
- `Domain` Defaults to the request-host. (Note that there is no dot at the beginning of request-host.)
- `Max-AgeThe` default behavior is to discard the cookie when the user agent exits.
- `Path` __Defaults to the path of the request URL that generated the Set-Cookie response, up to, but not including, the right-most /.__
- `Secure` If absent, the user agent may send the cookie over an insecure channel.

