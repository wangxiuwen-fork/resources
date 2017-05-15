# Secure Development - Input Validation

__Input Validation is very difficult to perform consistently!__

Input Validation is, by far, the hardest process in protecting web applications.

- No one solution fits all
- Centralize as much as possible
- Validate before processing, as early as possible

# Validation Steps in a web application

1. Client-side Validation
2. Web application firewall
3. Web server filter
4. Validation within the dev framework
5. Customized validation for (each) field

# Rules

- Client side validation is __NOT__ for security reasons.
- Only use user inputs when necessary.
	- Less input = less risk
- Always leverage information that is on the server.
 	- Back and forth hauling of information is unnecessary

# Encoding

Before performning any other validation actions on input data, first:
- decode URLs
- decode HTML entities
in order to make the data into a single uniform encoding scheme.

# Filtering

__Filtering is hard!__

Filtering and catching bad inputs is really tough.

## Filtering SQL

### Strings

How about `SE/**/LECT/**/` ?

### Numbers

Numeric fields don't need a quote to be injected

### Evasion

TODO...

## Filtering against XSS

- Filter out HTML meta-characters (minimum `<>';&\%"`)
- Watch for encoding

Be careful, do not blindly filter, it might backfire.
