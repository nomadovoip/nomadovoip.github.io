## Overview
This endpoint allows you to send one or multiple sms at once to any country.

## API Endpoint

?>**POST** `https://api.nomado.eu/sms/send`

## Authentication
You can choose one of the authentication methods referenced [here](/authentication.md).

## Message object
The JSON object representing the SMS to send. Should be included in request body.

| key | description | required | default value |
|---|---|---|---|
|to|Array of`E164`formatted mobile numbers | Yes |  |
|message|`string` Your SMS message| Yes | |
|unicode|`boolean` Indicates whether your message contains non-gsm characters | No | false |

!> SMS messages are limited to 160 characters (70 if using unicode). If the size exceeds the limit, messages will be split and billed separately.

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
  "to": ["32412345678","32423456789"],
  "message": "Hello world",
  "unicode": false
}
```


## Response example
```json
{
    "code": 200,
    "message": "OK",
    "total_sms": 2,
    "valid_numbers": 2,
    "data": {
        "callerID": "NOMADO",
        "text": "Hello world",
        "unicode": 0,
        "32412345678": {
            "code": 200,
            "status": "SENT"
        },
        "32423456789": {
            "code": 200,
            "status": "SENT"
        }
    },
    "cost": 0.20,
    "currency": "EUR"
}
```
