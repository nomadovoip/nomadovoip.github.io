## Overview
**Home Location Register** or HLR for short, is a database of all the mobile phones on this planet connected to their particular mobile network. `HLR Lookup` allow you to find out important information about a number. such as original network, current network, roaming status, number validation, current status, etc.

## API Endpoint

?>**POST** `https://api.nomado.eu/hlr`

## Authentication
You can choose one of the authentication methods referenced [here](/authentication.md).

## Body object
The JSON object representing the numbers to lookup. Should be included in request body.

| options | description | required | default value |
|---|---|:---:|---|
|numbers|`array<string>` Array of E164 formatted mobile numbers | Yes |  |


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
Body
```json
{
  "numbers": ["32412345678","32423456789"]
}
```


## Response example
```json
{
    "code": 200,
    "data": {
        "3245678901": { ... },
        "3245678902": { ... },
        "valid_numbers": 2
    },
    "cost": 0.05
}
```
