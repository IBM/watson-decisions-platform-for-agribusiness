# API Auth Tokens

In order to programatically access Weather Operations Center APIs for operations like asset import, registration of custom geospatial queries, etc., users need to generate JWT access tokens using their `apiKey`.

Shell example with curl:

```bash
curl --request POST --url https://auth-b2b-twc.ibm.com/Auth/GetBearerForClient --header 'Content-Type: application/json' --header 'cache-control: no-cache' --data '{"apiKey":"xxxxxxxxxxxxxx", "clientId":"ibm-agro-api"}'
```

Example output:

```{"access_token":"ey ..... 6Mg","expires_in":600,"token_type":"Bearer"}```


Please reach out to your IBM representative for `token provider URL` and `apiKey`.
