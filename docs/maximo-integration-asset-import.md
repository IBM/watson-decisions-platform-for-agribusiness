## IBM Weather Operations Center integration for Maximo Spatial Assets </h1> 

IBM Weather Operations Center integrates with the IBM Maximo solutions suite to simplify GeoSpatial monitoring of client Maximo assets for additional insight. Release 1.0 empowers users to import Maximo Asset Locations in order to expand their exploration of weather and other geospatial data layers. In order to perform the import operation, you would require the URL of the Maximo instance, Maximo API credentials and Weather Operations Center user credentials issued to you at the time of provisioning. 

<b>Action</b>: Ask your IBM representative to provide a IBM Weather Operations Center `API_KEY` for your users. 

## Generate JWT token to access IBM Weather Operations Center Service APIs
  
<b>Substitute `<API_KEY>` in the following request and call it in a command-line window (PC) or a terminal (MAC) </b>: 

 `curl --request POST --url https://auth-b2b-twc.wsitrader.com/Auth/GetBearerForClient --header 'Content-Type: application/json' --header 'cache-control: no-cache' --data '{"apiKey":"<API_KEY>", "clientId":"ibm-agro-api"}'`

<b>Response</b>: 

  `{"access_token":"<JWT_TOKEN>","expires_in":xxx,"token_type":"Bearer","scope":"xxxxxxx"}`
 
<b>Action</b>:

  Copy the value corresponding to `<JWT_TOKEN>` from the repsonse above to use in the Import API call below.
 
## Import new assets using e2e mode


### Import assets

<b>Substitute `<JWT_TOKEN>`, `<ASSET_COLLECTION_NAME>`, `<MAXIMO_AUTH>` and `<MAXIMO_URL>` in the following request and call it in a command-line window (PC) or a terminal (MAC) </b>: 

`curl -X POST -H 'Authorization: Bearer <JWT_TOKEN>' --data '{"displayName": "<ASSET_COLLECTION_NAME>", "maxauth":"<MAXIMO_AUTH>", "serviceUrl": "http://<MAXIMO_URL>/maximo/oslc/", "limit": 200}' 'https://foundation.agtech.ibm.com/v2/assetimport/source?mode=e2e' -i`


<b>Response</b>:


`{
  "code": "202",
  "message": "Number of assets imported [200]",
  "timestamp": "2020-Dec-10 12:50:46",
  "id": "<UNIQUE_ID>",
  "targetResponse": "Block added"


}`


### Status of the Import job


<b>Substitute `<UNIQUE_ID>` from the response above and your `<JWT_TOKEN>` in the following request and call it in a command-line window (PC) or a terminal (MAC) </b>: 


`curl -X GET "https://foundation.agtech.ibm.com/v2/assetimport/status/<UNIQUE_ID>" -H "accept: application/json" -H "Authorization: Bearer <JWT_TOKEN>"`


Response:

`
{
  "status": "LOADED",
  "message": "LOADED successfully",
  "last_modified": "2020-Dec-10 12:50:46"
}`


## Verify assets have been loaded into Weather Operations Center



 1. Login to Weather Operations Center with your username and password by launching http://weatheroperationscenter.ibm.com - and navigate to Dashboard Visualization -> Interactive Map:
 
![alt text](https://github.com/IBM/Weather-Operations-Center/blob/master/docs/resources/woc-maximo01.png?raw=true)

 2. Click on Map Layers and Overlays:
  
 ![alt text](https://github.com/IBM/Weather-Operations-Center/blob/master/docs/resources/woc-maximo02.png?raw=true)
 
 3. Select your asset collection (named <Asset Collection Name> in Import step above):
  
 ![alt text](https://github.com/IBM/Weather-Operations-Center/blob/master/docs/resources/woc-maximo03.png?raw=true)
  
 4. Select a Maximo asset on the interactive map to view details:
  
 ![alt text](https://github.com/IBM/Weather-Operations-Center/blob/master/docs/resources/woc-maximo04.png?raw=true)
  
 5. Turn on out-of-the-box weather layers to assess relevant attributes impacting the asset:
  
 ![alt text](https://github.com/IBM/Weather-Operations-Center/blob/master/docs/resources/woc-maximo05.png?raw=true)
  
 6. If work order creation/modification is needed based on the assessment in step 5, go to your Maximo UI and search for the Location/Asset by the name (copied over from step 4 above):
  
 ![alt text](https://github.com/IBM/Weather-Operations-Center/blob/master/docs/resources/woc-maximo06.png?raw=true)
  
 7. View 'Work Details' and adjust as necessary:
  
 ![alt text](https://github.com/IBM/Weather-Operations-Center/blob/master/docs/resources/woc-maximo07.png?raw=true)
  
  
 
