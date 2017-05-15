Best practices to avoid common web security pitfalls.

# CSRF

__CSRF__ Cross--Site Request Forgery exploits the trust that a site has in the user's browser.

In a CSRF attack, the attack leverages the fact that the client is already logged in and anything that the client sends to the server will be regarded by the server as client activity.

Most input forms are vulnerable to this attack if no special defenses are in place.

### CSRF mitigation/defense

- Avoid GET requests
- Use only POST. All forms leading to action must only accetp POST requests.
- Use short sessions. A tmeout reduces the window of opportunity.
- Check the HTTP referrer
	- There is no reason for some sites to link directly to your form actions.
- Use a CAPTCHA
	- Randomizes the response required to submit a form.
	- If implemented correctly, can provides a strong protection against CSRF.
	- But not practical for every form.
- Implement some flow control
	- For every critical form in the site put a boolean state to track whether a user has visited the form page before submission.
	Allow a single path through the application.

#### Anti-CSRF token

In a CSRF attack, the attacker does not see the HTML form being sent from server to client.

Generating a dynamic token for every form mitigiates CSRF:
- the token has to be random
- verifiable by the server
- unguessable
- sent back in a hidden form field

A token constructed with _Hash of the form name_ + _secret keys on the site_ + _sessionID_ does not have to be stored by the server. But can be somewhat CPU intensive because the server has to regenerate the token at every request.

### more CSRF resources

- https://scotthelme.co.uk/csrf-is-dead/

# Cookies

http://stackoverflow.com/questions/27972/how-do-httponly-cookies-work-with-ajax-requests

# SQL Injection

- Due to poor input validation.
- User inputs get passed without checking to the backend SQL database.

### exemple:

`SELECT id FROM table WHERE name='$var'``

$var is `' OR 1=1 --`

The query becomes:

`SELECT id FROM table WHERE name='' OR 1=1 --'`

## SQL Injection Attack Potentials

- Change the meaning of existing SQL queries
- Extract data
- Alter data
- Control the host running the database; jump to other hosts on the network.
	- e.e `xp_cmdshell` in MS SQL.

## SQL Injection attack

- Based on error messages
	- Distinct SQL errors in web app can allow the attacker to know which DB engine is running.
- Blind
	- Based on questions and answers (YES or NO answers from the server)

## SQL Injection mitigation

- Constrain input
	- Very hard to perform consistently
- Reject bad input
	- Reject reserved words like `insert`, `delete`, `--`, `char`, etc.
	- Reject SQL metacharacters
- Filter out all encoding not needed
- Escaping
	- Need to be done according the the database type used
- Use __parametrized queries__, also known as __prepared statements__
	- Easy solution to a complicated problem
- Stored Procedure
- Database Permission and Hardening
- Limit SQL error messages
	- security by obscurity
	- error messages may be OK for debug but in production these message must _never_ go to the user, only to logs.


### Prepared statements

Similar to _stored procedures_, the main difference being that in prepared statements, the SQL statement is constructed at the client side and not on the the database server.

In the Java JDBC implementation of _prepared statements_, the exact details that the DB driver has to perform for validation are not specified. This is the implementer responsibility.

A _prepared statement_ is not as strong as parametrized stored procedure.

### Stored Procedure

Never use dynamic SQL within a stored procedure.

One big advantage:
- access can be granted to the stored procedure and not the table themselve. Only the stored procedure can access the tables. An attacker could not access the tables directly.

Stored Procedure can be vulnerable to SQL injection if badly written. Never concatened a parameter with other parts of SQL strings to create the SQL statement.

### Database Permission and Hardening

The web app should only use low privilege accounts and only have the permission needed for the task. E.g. no write access if the app only read the data.

#### Hardening

- Delete unneeded stored procedures
- Delete default user accounts
- Monitor SQL server outbound connections


# Cross-Site Scripting (XSS)

- Tricks client browser to execute malicious scripting commands and HTML code.
- Caused by insufficient input Validation
- Easy to find, easy to exploit
- Commonly leverage Javascript but will also work with ActiveX, Flash ActionScript or any other scripting language.

## XSS Cause

- Bad input Validation
- User input displayed back in its original form

Potential effects:

- Disclosure of cookies
	- Lead to session hijacking
- Force redirection
	- Helps phishing
- Modify content of the web page
- Change images
- Run custom scripts

### Reflected XSS

The malicious (injected) content does not get stored in the server.

### Stored (Persistent) XSS

The malicious (injected) content gets stored in the server.

### Local XSS (DOM based)

The injected script does not go to the server

Often ignored when testing for server-side XSS

#### Universal XSS attack

`http://site/file.pdf#a=javascript:alert('xss');`

The local PDF viewer gets the full URL from the browser, including the fragment after '#', and then execute the javascript.

## XSS Defense

- Filter out HTML meta-characters (minimum `<>';&\%"`)
- Watch for encoding
	- Explicitly set the encoding, do not let the browser auto-detect.

Be careful, do not blindly filter, it might backfire. The exact characters to filter might be dependent upon the _encoding_ being used.

Do both _input filtering_ __and__ _output encoding_.

XSS happens on the output data. Input filtering cuts down the noise and output encoding get of it at the output.

### Output encoding

Escape or encode all _HTML enbtities_ to be sent to the browser.

Most languages already have this capability in their libs.

#### HTML Attributes

User input or untrusted data must be HTML entity encoded before being put in _simple attribute_ (`id`, `name`, etc.).

User input or untrusted data must __not__ be put into complex in _complex attribute_ such as `style`, `src`, `href` and event handler.

#### Javascript

Avoid putting user input into Javascript source as much as possible.

Untrusted data is only safe inside quoted data value in Javscript.

The untrusted data need to be Javascript escaped before being put in quoted value.

CSS can contain Javascript.

#### URL GET parameter

TODO...

## XSS Resources

- https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet
- https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet
- https://github.com/cure53/H5SC


# Input Validation

# File Upload

# Security Config

# Anti Automation

# Safe Redirection

# HTTP Response Splitting

HTTP Response Splitting allows attackers to inject information into the HTTP response header.

This attack does not target the web application itself.
- Targets are usually _clients_ of the website
- Or infrastructure components (_proxy cache poisoning_)
- Usually used in conjunction with other attacks (_session fixation_, _XSS_, etc.)
- Hard to manually detect and test

Defense:
- Input Validation
- Avoid CR/LF
- Validate redirections

# CORS - Cross Origin Resource Sharing

- https://www.w3.org/TR/cors/

# Headers



# Security

### SRI

https://www.srihash.org/

## Password storage

https://nakedsecurity.sophos.com/2013/11/20/serious-security-how-to-store-your-users-passwords-safely/

# Headers

- __https://securityheaders.io/__
- https://blog.cleantalk.org/exotic-http-headers/

# CSP - Content Security Policy

- https://report-uri.io/

# HTTP Public Key Pinning

- https://report-uri.io/

# AngularJS

http://fr.slideshare.net/carlo.bonamico/angularjs-security-defend-your-single-page-application

# OpenID, SAML, OAuth

## OpenID

- Attemp to provide users with a single sign-on to various sites.
- Same URL used to identify the user against different service providers
- Only HTTP(S) redirects, no Javascript
- Only as good as the weakest permitted provider
- Easy to implement
- Well validated
- Server will have to contact various OpenID providers
- Privacy not explicitely considered
- By default, trust all OpenID providers (black list)
- Not very extensible

## SAML

- Designed with Service-Oriented Architecture (SOA) in mind.
- Can be used with a browser but main focus is web services.
- The consumer has to explicitely trust  the SAML provider.
- Privacy concerns part of the standard
- By default, trust nobody (white list)
- Modular extensible design

## OAuth

- Authorization standard
- The goal is to provide the user of one app access to information stored in another web app, securely and without exposing the user's credentials and letting the user control information is shared between the apps.
- Valet key concept where a subset of the information can be passed on to third-party
- Password change does not alter the app that had been authorized
- CSRF protection not built-in with OAuth

# Resources

- https://github.com/vasanthk/web-security-basics
- http://lcamtuf.coredump.cx/tangled/
- https://mikewest.org/2013/09/frontend-security-frontendconf-2013
- https://html5sec.org/
