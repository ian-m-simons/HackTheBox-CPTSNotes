defined in RFC 8615 typically found in /.well-known/ centralizes critical metadata, including config files and info related to its services, protocols, etc IANA maintains a registry of .well-known URIs and what their purpose is. some notable examples are below

| URI Suffix                   | Description                                                                                          | Status      | Reference                                                                                |
| ---------------------------- | ---------------------------------------------------------------------------------------------------- | ----------- | ---------------------------------------------------------------------------------------- |
| security.txt                 | Contains contact information for security researchers to report vulnerabilities                      | Permanent   | RFC 9116                                                                                 |
| /.well-known/change-password | Provides a standard URL for directing users to a password change page                                | Provisional | https://w3c.github.io/webbappsec-change-password-url/#the-change-password-well-known-uri |
| openid-configuration         | Defines configuration details for OpenID connect, an identity layer on top of the OAuth 2.0 protocol | Permanent   | http://openid.net/specs/openid-connect-discovery-1_0.html                                |
| assetlinks.json              | Used for verifying ownership of digital assets (ie apps) associated with a domain                    | Permanent   | https://github.com/google/digitalassetlinks/blob/master/well-known/specifications.md     |
| mta-sts.txt                  | Specifies the policy for SMTP MTA Strict Transport Security (MTA-STS) to enhance email security      | Permanent   | RFC 8461                                                                                 |
### Web Recon and .well-known
There can be a ton of useful information found here. in particular `openid-configuration` this page returns a JSON document containing metadata about the privedr's endpoints, supported authentication methods, token issuance, and more. Valuable information to find includes:
1. `Endpoint Discovery`: 
	- `Authorization Endpoint`: Identifying the URL for user authorization requests.
	- `Token Endpoint`: Finding the URL where tokens are issued.
	- `Userinfo Endpoint`: Locating the endpoint that provides user information.
2. `JWKS URI`: The `jwks_uri` reveals the `JSON Web Key Set` (`JWKS`), detailing the cryptographic keys used by the server
3. `Supported Scopes and Response Types`: Understanding which scopes and response types are supported helps in mapping out the functionality and limitations of the OpenID connect implementiation
4. `Algorithm Details`: Information about supported signing algorithms can be crucial for understanding the security measures in place .