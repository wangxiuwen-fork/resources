# WS-Security

An effort to standardize authentication, authorization, encryption and digital signature for web services.

SOAP based :-(  WS-Security is an extension to SOAP messages.

## WS-Security authentication

```
<UsernameToken>
	<Username>MyName</Username>
	<Password Type="PasswordDigest">...</Password>
	<Nonce>A984tFWIU3948Hiuer==</Nonce>
	<Created>2016-12-29T04:33:22Z</Created>
</UsernameToken>
```

`<Nonce>` and `<Created>` timestamp are there to mitigate replay risk.
