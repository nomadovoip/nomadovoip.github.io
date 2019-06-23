## Overview
Once the SMS containing the OTP has been sent, this endpoint allows you to verify the token submitted by the user.

## API Endpoint

?>**POST** `https://api.nomado.eu/2fa/verify`

## Authentication
You can choose one of the authentication methods referenced [here](/authentication.md).

## Body object
The JSON object representing the OTP to verify. Should be included in request body.

| options | description | required | default value |
|---|---|:---:|---|
|number|`string` E164 formatted mobile number | Yes |  |
|token| `string` The OTP to verify| Yes | |

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
  "number": "32412345678",
  "token": "1234"
}
```


## Response example
```json
{
    "code": 200,
    "message": "OK",
    "verify": true
}
```
