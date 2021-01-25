# Admins: how to upload field data to IBM Object Storage

The following uploads zipped files to an IBM COS bucket called eg agrotech-prod-agrocustomername-onboarding.

1. Get a valid auth token: [Generate an API Authorization JWT](./api-tokens.md)
2. Upload files request:
3. Run the following API:

* `curl -k -X POST  -H 'Accept: application/json' -H 'Content-Type: multipart/form-data' -H  "X-Profile-Id: <PROFILE-ID>" -H 'Authorization: Bearer <ADMIN JWT TOKEN>' -F data=<@FILELOCATION> -i 'https://foundation.agtech.ibm.com/upload'`

Step 2 assumes that you have provided with an admin API key to be able generate an admin token and also with the PROFILE-ID that correspondes to the customer userid.
