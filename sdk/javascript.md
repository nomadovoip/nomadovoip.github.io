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

!> If you do not have a nomado account, please [signup](https://my.nomado.eu/join.) and get **free 10€ credit** to continue.

Below is a quick example for initializing the library and sending a SMS.

```javascript
const nomadoClient = require('nomado');

const USERNAME = 'username';
const PASSWORD = 'password';

const nomado = new nomadoClient({USERNAME, PASSWORD});

const smsOptions = {
  to: ['3245678901'],
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

##### sms.send()
Send a SMS to one or multiple numbers.

```javascript
nomado.sms.send({
  to: ['3245678901','3245678902'], // e164 formatted numberr in array
  message: 'My first sms from nomado!', 
  unicode: false // Boolean: unicode. See options for all possibilities
});
```
Response:
```javascript
// expected response
{
  code: 200,
  data: {
    callerID: 'NOMADO',
    text: 'My first sms from nomado!',
    unicode: 0,
    '3245678901': { ... },
    '3245678902': { ... }
  },
  cost: 0.16,
  total_sms: 2,
}
```

!> TIP : If you are sending SMS that contains non-gsm characters, set `unicode: true`

---
#### OTP
OTP stands for One time password / pin. Setting up OTP from scratch is cumbersome and require some sleeve rolling tasks such as generating random pin, storing it for verification (including setting up database), send the token via sms, writing endpoints for verifying later, etc. 

this function let you skip all that problems and use our `OTP as service` for free (normal sms charge applies)

---

##### otp.send()
Generating OTP code and sending via sms to your users is as easy as below:

```javascript
nomado.otp.send({
  to: '3245678901', // e164 formatted number (required)
  ...               // Look at all possible parameters and their default values below
})
```

###### Possible parameters
| options | description | required | default value |
|---|---|:---:|---|
|to|`E164`formatted mobile number | Yes |  |
|template| `string`. MUST contain `{{CODE}}` literal in it| No | {{CODE} |
|type| `string` : Type of OTP required. Possible values: `ALPHA`, `NUMERIC` and `ALPHANUMERIC`| No | ALPHANUMERIC |
|length|`Integer` : length of the OTP required. `Max 20`| No | 4 |
|expiry| `time in seconds`. After that, the OTP will expire autoamtically.| No | 7200 |

---

##### otp.verify()
OTP is useless if you cannot verify, isn't it? Lets see how easy it is to verify the OTP. **no local storage require!**

```javascript
nomado.otp.verify({
  number: '3245678901', // E164 formatted mobile number used,
  token: '456789' // OTP generated in previous call. You do not need to store it locally.
})
```

Response:
```javascript
// expected response
{
  code: 200,
  data: {
    verify: true
  }
}
```

!> OTP as the name suggest, Once verified or expired, will be destroyed.

---

### HLR

**Home Location Register** or HLR for short, is a database of all the mobile phones on this planet connected to their particular mobile network. `HLR Lookup` allow you to find out important information about a number. such as original network, current network, roaming status, number validation, current status, etc.

---

##### hlr.fetch()

Make a query 

```javascript
nomado.hlr.fetch({
  numbers: ['3245678901','3245678902'], // e164 formatted numbers
});
```

Response:
```javascript
{
  code: 200,
  data: {
    '3245678901': { ... },
    '3245678902': { ... },
    valid_numbers: 2
  },
  cost: 0.05,
}
```
---

##### hlr.validate()
Not as roburst as a hlr lookup, `hlr.validate` provides basic information regarding a phone number such as if its a valid phone number, a landline or mobile, country it belongs, etc. This lookup does not cost you anything.

```javascript
nomado.hlr.validate({
  number: '3245678901', // e164 formatted number
});
```

Response:
```javascript
{
    "Status": "Valid",
    "Region": "GB",
    "CountryCode": 44,
    "Type": "Mobile"
}
```