# Encoding

A _stream of bytes_ can be decoded using a number of different encodings. The bytes themselves don't indicate what encoding they use:

- **Encoding is out-of-band.**
- **You cannot infer the encoding of bytes**
- **You must be told or you have to guess**

TODO: give examples

Explicitly set the encoding, do not let the browser auto-detect.

# HTTP headers encoding

__Per RFC 2109 (sec. 4.2.2) and RFC 2616 (sec. 2.2, 4.2), HTTP headers may only be transmitted in ISO-8859-1.__ (There is an 
exception, but this is primarily used for MIME and is pretty much never seen in HTTP.) Since ISO-8859-1 is really just a 
series of octets, the server can choose to use a different encoding (UTF8, in this case) if it wishes, since cookies are
intended to be treated opaquely by the client anyway. Thus it should be round-tripped correctly in all cases, but if the 
client tries parsing the cookie it will get different results based on whether or not it is following the RFCs.

Please try to avoid sending non-ASCII characters in headers if at all possible. The HTTP spec never really accounted for 
this properly, and as a result it causes pain and heartache when used in practice. :(

## Good To Know

### Java properties

By _default_:
- Text (line-oriented) properties files must be encoded in ISO 8859-1.
- XML formated properties files must be encoded in UTF-8

### JSON

JSON documents can be encoded in UTF-8, UTF-16 or UTF-32, the default encoding being UTF-8.

# Tools

- **https://r12a.github.io/apps/conversion/**
- **https://r12a.github.io/uniview/**
- https://software.hixie.ch/utilities/cgi/unicode-decoder/utf8-decoder
- http://www.online-toolz.com/tools/text-unicode-entities-convertor.php

# Resources

- [Dark corners of Unicode](https://eev.ee/blog/2015/09/12/dark-corners-of-unicode/)
- https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/
- http://nedbatchelder.com/text/unipain.html
- https://en.wikipedia.org/wiki/Mojibake
- http://haacked.com/archive/2012/01/30/hazards-of-converting-binary-data-to-a-string.aspx/
- https://www.smashingmagazine.com/2016/11/character-sets-encoding-emoji/
