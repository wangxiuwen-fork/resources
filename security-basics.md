# Terminology

- **HSTS** HTTP Strict Transport Security
- **PFS** Perfect Forward Secrecy
- **DHE** Diffie-Hellman cipher suites
- **ECDHE** Elliptic Curve cryptography
- **TLS** Transport Layer Security
- **SSL** Secure Sockets Layer
- **CA** Certificate Authority
- **SNI** Server Name Indication
- **CRL** Certificate Revocation List
- **OCSP** Online Certification Status Protocol

# Session

__Session__: maintain user's state information with the application between requests

The session token is as important as username and password. __I have your token, I become you!__

## Session best practices:
- Do not use URL SessionIDs
- Use a strong crypto system to generate the random session tokens
- Use TLS

### cookies:
- Do not store any state information in a cookie, except for the session token.
- All data related toe the session must be stored and tracked in the server, and never passed to the client.

### protection against session fixation:
- Never accept "chosen" (or user-generated) session IDs. Always generate a new session ID for each new login request.
- Assign a new session ID after a successful login (not easy in Java or .net)
	- Java, .net: invalidate the session, create a new session, copy the previous session data into the new session.
	- PHP: use `session_regenerate_id()`
	- other possibility: create an additional random token on top of the session token. Inlude this new token in each request/response and validate it. If it is missing or tempered, deny the access and invalidate the session.
- Bind the session ID to an ummutable property of the client, such as network address or TLS client certificate.


## Additional protection

- Store and check the user-agent string set by the browser. If the user-agent changes, terminate the session immedialtely and log the info. The will need to log in again.

## Logout

When the user logouts, the server _must_ destroy all session data related to the user.

- Set a timeout limit on the session.
	- Lack of timeout can make other vulnerabilities, such as CSRF, easier to attack.
- Set a hard limit on the whole session duration.
- Beware of the browser's back button!

# Cookies

Cookie are usually used to carry a session token, which is a critical piece of information. Any security exposure can be catastrophic.

## `secure` flag

Indicates the the cookie can be sent only over TLS.

## `httponly` flag

Prevents Javascript from accessing the cookie. First layer of defense against cross-site scripting.

Any cookie containing the session token must be protected by the `httponly` flag.

### Java:

in web.xml:

```
<session-config>
  <cookie-config>
    <secure>true</secure>
    <http-only>true</http-only>
  </cookie-config>
</session-config>
```

### PHP:

in php.ini

```
php_value session.cookie_httponly 1
php_value session.cookie_secure 1
```

# Encryption

Encryption ensure the _confidentiality_ and _integrity_ of data.

- **Cipher**:
	- algorithm used to encrypt data
	- protect privycy
- **Hash**:
	- algorithm used to sign data
	- detects changes in transit
- **Symmetric** encryption:
	- same key is used to encrypt and decrypt the data
	- fast
	- need to share a key between the parties
- **Asymmetric** encryption:
	- one public key for encryption
	- one private key for decryption
	- no key exchange necessary

## Symmetric Key Management

The hardest part of encryption is key management.

Best practices:
- Do not store key in the code
- Monitor key reading and changes at OS and filesystem level
- Always use secure channel to initiate keys

## Public Key encryption

- Asymmetric encrpytion
- Two-key encrytion system
	- Public Key
	- Private Key
- Data encrypted with the public key can only be decrypted with the private key
- The private key must always be kept secret
	- Most private key are also protected by a password



# TLS

- TLS secures data in transit
- `https://` signifies the use of TLS
- Certificate is based on `Fully Qualified Domain Name` (FQDN)
- Relies on trust

### Web of Trust

customer --> signing CA --> SSL server

1. The customer trusts the CA
2. The CA trusts the server
3. The customer trusts CA's trusts for server

### TLS pitfalls

SSL v2 and v3 have design issues. Do not use!

TLS support NULL cipher for debugging purposes. All traffic is in clear with the NULL cipher. Use with caution!

### TLS versions

TLS 1.0 is SSL 3.0

SSL 2 --> SSL 3 --> TLS 1.0 --> TLS 1.1 --> etc...

### Best practices

- SSL v1 and v2 must be disabled on all moderne servers. SSL v3 should be retiered if compatibility is not an issue.
- TLS 1.2 should be supported
- Support only TLS 1.0 and above
- Prefer stronger TLS 1.2 viphers _first_
- AES (128/256) with GCM mode is the current preferred mechanism
- Certificate must be at least 2048 bits RSA + SHA2
- Use ECC (Elliptical curve crypto) certificate if possible
- Update software to the latest TLS and ciphers
- Disable SSL compression with TLS 1.0
- Enable _Http Strict Transport Security_ (HSTS)
- Review these best practices often and update.

## SNI Server Name Indication

Allow one IP to host multiple SSL sites.

The client specifies the domain name befiore SSL starts.

## Certificate pinning

Firefox and Chrome are currently hardcoding the TLS pinning into the browser with the only exception being the self-signed CA root.

## Password storage

- Passwords should __never__ be stored in cleartext in a database.
- Passwords are never meant to be recoverable.
- Cryptpgraphic hashes are the proper way of storing passwords.

### Password hashing

- MD5 is tool old
- Use a SHA family algorithm
- Add _salt_ generated with a crypto random genetor
	- At least 8 bytes
- Use multiple iterations
	- The iteration should take up a minimum of 0.25 second on the server that's running the application
- Use _existing_ and tested mechanisms to perform the crypto functions
	- bcrypt is getting old
	- Argon2 is the defacto industry standard and is recommended
	- PDKDF2 is under attack and probably vulnerable
	- see also `libsodium`

Pepper: a system wide random string not unique to each user and stored outside of the DB.

https://www.owasp.org/index.php/Hashing_Java

### See also:

- https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet
- https://www.owasp.org/index.php/Forgot_Password_Cheat_Sheet

## Recommended Crypto Techno

- Hashing algorithm
	- SHA-256, SHA-512, SHA-3, RIPEMD-160
- Symmetric algorithm
	- AES, Blowfish, Twofish, Serpent
- Asymmetric algorithm
	- RSA, ECDSA

# Input Validation

Never trust your inputs!

- Buffer overflow
	- validate input length
- OS command injection
	- At minimum, block semi-colon, backtick and pipe characters
	- Do not use OS comands in web app.
	- Never let GET or POST parameters go to the comand line.


# Resources

- https://martinfowler.com/articles/web-security-basics.html
