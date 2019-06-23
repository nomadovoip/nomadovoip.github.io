## Overview
This endpoint allows you to send one or multiple sms at once to any country.

## API Endpoint

?>**POST** `https://api.nomado.eu/sms/send`

## Authentication
You can choose one of the authentication methods referenced [here](/authentication.md).

## Message object
The JSON object representing the sms to send. Should be included in request body.

| key | description | required | default value |
|---|---|:---:|---|
|to|Array of`E164`formatted mobile numbers | Yes |  |
|message|`string` Your SMS message| Yes | |
|unicode|`boolean` Indicates whether your message contains non-gsm characters | No | false |

---

!> SMS messages are limited to 160 characters (70 if using unicode). If the size exceeds the limit, messages will be split and billed separately.

## Request example
Headers
```
Content-type: application/json
Authorization: BASIC base64encodedCredentials
```
Body
```json
{
  to: ['32412345678','32423456789'],
  message: 'Hello world',
  unicode: false,
}
```
