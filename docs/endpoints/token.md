---
layout: docs-default
---

#Token Endpoint

The token endpoint can be used to programmatically request or refresh tokens (resource owner password credential flow, authorization code flow, client credentials flow and custom grant types).

### Supported Parameters

See [spec](http://openid.net/specs/openid-connect-core-1_0.html#TokenRequest).

- `grant_type` (required)
    - `authorization_code`, `client_credentials`, `password`, `refresh_token` or custom
- `scope` (required for all grant types besides refresh_token and code)
- `redirect_uri` (required for code grant type)
- `authorization_code` (required for code grant)
- `username` (required for password grant type)
- `password` (required for password grant_type)
- `acr_values` (allowed for password grant type to pass additional information to user service)
    - there are values with special meaning:
        - `idp:name_of_idp` bypasses the login/home realm screen and forwards the user directly to the selected identity provider (if allowed per client configuration)
        - `tenant:name_of_tenant` can be used to pass extra information to the user service
- `refresh_token` (required for refresh token grant)
- `client_id` (either in the post body, or as a basic authentication header)
- `client_secret` (either in the post body, or as a basic authentication header)

### Authentication
All requests to the token endpoint must be authenticated - either pass client id and secret via Basic Authentication
or add `client_id` and `client_secret` fields to the POST body.

### Example
(Form-encoding removed and line breaks added for readability)

```
POST /connect/token
Authorization: Basic abcxyz

grant_type=authorization_code&
authorization_code=hdh922&
redirect_uri=https://myapp.com/callback
```