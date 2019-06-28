## Overview
Not as robust as a hlr lookup, this endpoint allows you to fetch basic information regarding a phone number such as if its a valid phone number, a landline or mobile, country it belongs, etc. 
This lookup does not cost you anything.

## API Endpoint

?>**POST** `https://api.nomado.eu/hlr/validate`

## Authentication
You can choose one of the authentication methods referenced [here](/authentication.md).

## Query URL
Just append the number to the API endpoint url, such as `https://api.nomado.eu/hlr/validate/[NUMBER]` where 
`[NUMBER]` will be replaced by the actual E164 formatted mobile number.


## Response

| status code | description |
|:---:|---|
|200|`success` Request sent successfully |
|400|`bad request` Incorrect or missing parameters |
|401|`unauthorized` Invalid credentials or incorrect authentication method |

___

## Request example
Headers
```
Content-type: application/json
Authorization: BASIC base64encodedCredentials
```

Query URL
`https://api.nomado.eu/hlr/validate/32456789012`


## Response example
```json
{
    "Status": "Valid",
    "Region": "BE",
    "CountryCode": 32,
    "Type": "Mobile"
}
```
