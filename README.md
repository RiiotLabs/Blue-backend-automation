# Automation-Api
## Version: 0.1 - 2022-06
## Base URl : https://api.riiotlabs.com/automation
 
For all the request to this API you'll have to use you blue connect credentials and basic authentication header.


Node JS Example : 

const buff = new Buffer.from(\"user@name.com:password\");

const auth = 'Basic ' + buff.toString('base64');

const headersForRequest = {
  Authorization : auth
}



 
When you configure a webhook, The data send to your server will be using the exact same format as [LastMeasurement](#LastMeasurement)
 
### /blue/{blueKey}/configureWebhook

#### POST
##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| blueKey | path | The Key of your blue connect. | Yes | string |
| configureWebhook | body | The webhook configuration. | Yes | [configureWebhook](#configureWebhook) |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | 200 response |
| 400 | 400 response |
| 500 | 500 response |
 
### /blue/{blueKey}/lastMeasurement

#### GET
##### Parameters
## This path will deliver the information once every 72 minutes, as this is the Blue Connect measurement frequency. If you configured your webhooks, every measurement will tigger the reponse.

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| blueKey | path | The Key of your blue connect. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | 200 response | [LastMeasurement](#LastMeasurement) |
| 400 | 400 response |  |
| 500 | 500 response |  |
 
### Models


#### LastMeasurement

| Name | Type | Description | 
| ---- | ---- | ----------- | 
| temperature_celsius | number | Your pool temperature in °C. | 
| temperature_fahrenheit | number | Your pool temperature in °F. | 
| ph | number | You pool pH. | 
| salinity_g_per_l | number | The salinity of your pool in grams per liter (or ppm). |
| orp_mV | number | The orp measurement of your pool. | 
| timestamp | string | The UTC date when the measurement was taken. |
| blueKey | string | The Blue Connect key linked to the measurement. | 
| status | [ string ] | A not ordered list of status for you pool, possible values are "BLUE_ASLEEP", "PH_LOW", "PH_OK", "PH_HIGH", "ORP_LOW", "ORP_OK", "ORP_HIGH", "SALINITY_HIGH", "SALINITY_OK", "SALINITY_LOW", "SP_OK", "SP_NOT_OK", "TEMPERATURE_LOW", "TEMPERATURE_HIGH", "TEMPERATURE_OK", "TEMPERATURE_IDEAL", "FCL_LOW", "FCL_OK", "FCL_HIGH", "FBR_LOW", "FBR_OK", "FBR_HIGH", "TA_LOW", "TA_OK", "TA_HIGH", "TA_OLD", "CYA_LOW", "CYA_OK", "CYA_HIGH", "CYA_OLD", "TH_LOW", "TH_OK", "TH_HIGH", "TH_OLD" | 

#### configureWebhook

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| headers | object | A list of headers that we will send to your server, to manage a certain level of security. all headers are fixed and must be string values. | No |
| active | boolean | To enable/disable the sending without removing the whole configuration. | Yes |
| url | string | The webhook URL from your own server. | Yes |
