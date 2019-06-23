## Overview
This endpoint allows you to implement Two Factor Authentication the easy way, by sending
a SMS with One Time Password (OTP).

## API Endpoint

?>**POST** `https://api.nomado.eu/2fa/create`

## Authentication
You can choose one of the authentication methods referenced [here](/authentication.md).

## Body object
The JSON object representing the OTP to send. Should be included in request body.

| options | description | required | default value |
|---|---|:---:|---|
|to|`string` E164 formatted mobile number | Yes |  |
|template| `string` MUST contain `{{CODE}}` literal in it, which will be replaced by the generated OTP| No | {{CODE} |
|type| `string` Type of OTP required. Possible values: `ALPHA`, `NUMERIC` and `ALPHANUMERIC`| No | ALPHANUMERIC |
|length|`Integer`  length of the OTP required. `Max 20`| No | 4 |
|expiry| `Integer` time in seconds after which the OTP will expire automatically.| No | 7200 |

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
  "to": "32412345678",
  "template": "Your verification code is {{CODE}}",
  "type": "NUMERIC",
  "length": 4,
  "expiry": 7200
}
```


## Response example
```json
{
    "code": 200,
    "message": "OK",
    "data": {
        "32412345678": {
            "code": 200,
            "status": "SENT"
        },
        "text": "Your verification code is 1234",
        "token": "1234",
        "expiry": 7200,
        "total_messages": 1
    }
}
```
