# Javascript SDK

[Github](https://github.com/nomadovoip/nomado-node) | [npm](https://www.npmjs.com/package/nomado)

The easiest and recommended (read: smartest) way to use nomado REST API in your nodejs application is via our sdk.

---

## Installation

```javascript
npm install nomado
```

---

## Quickstart

!> If you do not have a nomado account, please [signup](https://my.nomado.eu/join) and get **free 10€ credit** to continue.

Below is a quick example for initializing the library and sending a SMS.

```javascript
const nomadoClient = require('nomado');

const USERNAME = 'username';
const PASSWORD = 'password';

const nomado = new nomadoClient({USERNAME, PASSWORD});

const smsOptions = {
  to: ['32456789012'],
  message: 'Hello world',
  unicode: false
};

nomado.sms.send(smsOptions)
    .then((response) => {
      console.log(response.code);
      console.log(response.data);
    })
    .catch((error) => {
      console.log(error.code);
      console.log(error.reason);
    });
```
### Responses
Every call will return a promise that will be resolved (or rejected) with a nomadoResponse object wrapping the API response code and the data.

```javascript
// Result object:
{
  code: 200, //OK!
  reason: "", //in case of error
  data: {}
}
```

---
### Authentication
First, initialize the library with your nomado credentials.

```javascript 
const nomado = new nomadoClient({USERNAME, PASSWORD});
```

Now, you can start sending requests to the API.

## Functions

The nomadoClient class provides the public interfaces to access the nomado API

* `SMS`
* `OTP`
* `HLR`
* `Calls`
* `Account`
---

### SMS

##### sms.send()
Send a SMS to one or multiple numbers.

```javascript
nomado.sms.send({
  to: ['3245678901','3245678902'], // e164 formatted numberr in array
  message: 'My first sms from nomado!', 
  unicode: false // Boolean: unicode.
});
```

---
#### OTP

##### otp.send()
Generating OTP code and sending via sms to your users is as easy as below:

```javascript
nomado.otp.send({
      "to": "32412345678",
      "template": "Your verification code is {{CODE}}",
      "type": "NUMERIC",
      "length": 4,
      "expiry": 7200
})
```

---

##### otp.verify()

```javascript
nomado.otp.verify({
  number: '32456789012', // E164 formatted mobile number used,
  token: '456789' // OTP generated in previous call. You do not need to store it locally.
})
```

---

### HLR


##### hlr.fetch()

Make a query 

```javascript
nomado.hlr.fetch({
  numbers: ['32456789012','32456789013'], // e164 formatted numbers
});
```

---

##### hlr.validate()

```javascript
nomado.hlr.validate({
  number: '32456789012', // e164 formatted number
});
```
