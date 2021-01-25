# Geospatial Analytics API

## Authentication

### Overview
Geospatial Analytics API endpoints require an authenticated access token to be provided as an
HTTP Authorization header Bearer realm. For example:

``` text
Authorization: Bearer xxxxxxxx
```

Geospatial Analytics uses the Weather Operations Center authorization server to provide API access.
The Weather Operations Center authorization server implements standard OAuth 2.0 and OpenId Connect 1.0 protocols.

Authorization server endpoints are located at the base Uri:
- https://auth-b2b-twc.ibm.com/

An OpenId Connect discovery document for the authorization server is located at the Uri:
- https://auth-b2b-twc.ibm.com/.well-known/openid-configuration

To make Geospatial Analytics API requests an API key is provided to obtain an access token
which is then used in API requests to confirm authentication and to execute further authorization controls.

Geospatial Analytics API requests are secured by access token validation. The following diagram illustrates the API key usage flow
for just one of the Geospatial Analytics APIs: `/v2/query`. The section [Obtaining an Access Token](#obtaining-an-access-token) further
below provides details.

![Geospatial-API-Authentication-Overview](resources/Geospatial-API-Authentication-Overview.png)

1. Call the authorization server endpoint to obtain an authenticated access token with your API key
2. The JSON response contains a property `access_token` which will be used as the "`Authorization: Bearer xxxxxxxx`" HTTP header value
2.1. The JSON property `refresh_token` value is kept for later use in `#5` below.
3. Requests to the Geospatial Analytics API shall be submitted to the applicable API endpoint with "`Authorization: Bearer xxxxxxxx`"
4. Geospatial Analytics API response payload
5. The access token obtained in `#2` has expired, a request for a new token is made using the `refresh_token` value
6. The JSON response contains properties `access_token` and `refresh_token` as in `#2` above
7. The new access token is used for Geospatial Analytics API requests
8. Geospatial Analytics API response payload; and the process to make API requests and refresh access token continues

### Obtaining an Access Token

An API endpoint is provided that accepts a JSON object and will return a JSON response containing an access token:
- **POST** https://auth-b2b-twc.ibm.com/auth/GetBearerForClient
- **Content-Type:** `application/json`
- **Expected Data:** `{"apiKey":"xxxxxxxx", "clientId":"ibm-pairs"}`

For example:

``` shell
curl --request POST \
     --url https://auth-b2b-twc.ibm.com/auth/GetBearerForClient \
     --header 'Content-Type: application/json' \
     --data '{"apiKey":"xxxxxxxx", "clientId":"ibm-pairs"}'
```

The result of **POST** `/auth/GetBearerForClient` will produce:

``` json
{
 "access_token":"<ACCESS_JWT>",
 "expires_in":3600,
 "token_type":"Bearer",
 "refresh_token":"<REFERSH TOKEN>",
 "scope":"custom.profile email ibm-pairs-api offline_access openid phoenix-api profile"
}
```

Where; the response payload value for property `access_token`, i.e. `<ACCESS_JWT>`, is used in the example below
which submits a Geospatial Analytics API query request.

In this example, the value of the `access_token` property in the response above is used as the value for
the`Authorization` header Bearer realm in a request to the Geospatial Analytics API `/v2/query` endpoint.

``` shell
curl --request POST \
     --url https://pairs.res.ibm.com/v2/query \
     --header 'Content-Type: application/json' \
     --header 'Authorization: Bearer <ACCESS_JWT>' \
     --data '{...omitted for brevity...}'
```

### Refreshing an Access Token

For scenarios where usage of an access token is longer than the default token expiry of 1 hour,
Geospatial Analytics API requests will respond with a *`403` Forbidden* code and an error data payload:

`{"error":"jwt signature verification failed: 'exp' claim expired at Mon, 4 Jan 2021 10:27:37 GMT"}`

When an access token expires, the `refresh_token` property value of `/auth/GetBearerForClient` and
`/connect/token` JSON responses can be used to request a new `access_token` without re-authenticating
with your API key as follows:

``` shell
curl --request POST \
     --url https://auth-b2b-twc.ibm.com/connect/token \
     --header 'Content-Type: application/x-www-form-urlencoded' \
     --data-urlencode "grant_type=refresh_token" \
     --data-urlencode "client_id=ibm-pairs" \
     --data-urlencode "refresh_token=<REFRESH TOKEN>"
```

The result of **POST** `/connect/token` will produce a JSON response payload with a new `access_token` and
`refresh_token` to use in subsequent Geospatial Analytics API and authorization server requests
where applicable..
