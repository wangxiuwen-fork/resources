# Encoding

A _stream of bytes_ can be decoded using a number of different encodings. The bytes themselves don't indicate what encoding they use:

- **Encoding is out-of-band.**
- **You cannot infer the encoding of bytes**
- **You must be told or you have to guess**

TODO: give examples

Explicitly set the encoding, do not let the browser auto-detect.



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
