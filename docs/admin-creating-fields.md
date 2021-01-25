# Admins: how to create fields for a user

The following assumes subfield geometries (eg as kml files) have been already uploaded to an IBM COS bucket called eg agrotech-prod-agrocustomername-onboarding.

1. Get a valid auth token: [Generate an API Authorization JWT](./api-tokens.md)
2. Create a JSON payload similar to this in a file called eg field.json:

```json
{
  "name": "Field Name",
  "subFields": [
    {
      "name": "Subfield-Name",
      "geo": {
        "type": "kml",
          "url": "s3:///agrotech-prod-agrocustomername-onboarding/subfield-file-name.kml"
      }
    }
    ]
 }
 ```
3. Run the following field API:

* `curl -X POST -H 'Accept: application/json' -H 'Content-Type: application/json' -H  "X-Profile-Id: <PROFILE-ID>" -H 'Authorization: Bearer <ADMIN JWT>' -d @field.json -i 'https://foundation.agtech.ibm.com/v2/field'`
* This assumes that you have been provided with an admin API key to be able generate an admin token and also with the PROFILE-ID that correspondes to the customer userid.
