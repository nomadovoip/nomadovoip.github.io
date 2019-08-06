# El SDK para Javascript

[Github](https://github.com/nomadovoip/nomado-node) | [npm](https://www.npmjs.com/package/nomado)

La forma recomendada y más fácil (léase: más inteligente) de utilizar la API REST de nomado en su aplicación nodejs es a través de nuestro sdk (kit de desarrollo de software).


---

## Instalación

```javascript
npm install nomado
```

---

## Inicio rápido

!> Si no dispone de una cuenta nomado, por favor, [regístrese](https://my.nomado.eu) y obtenga 10€ de crédito gratis para continuar.

A continuación se muestra un ejemplo rápido para inicializar la biblioteca y enviar un SMS.


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
### Respuestas
Cada llamada devolverá una promesa (promise) que será resuelta (o rechazada) con un objeto nomadoResponse que envuelve el código de respuesta de la API y los datos.

```javascript
// Result object:
{
  code: 200, //OK!
  reason: "", //in case of error
  data: {}
}
```

---
### Autentificación
Primero, inicialice la biblioteca con sus credenciales de nomado.

```javascript 
const nomado = new nomadoClient({USERNAME, PASSWORD});
```

Ahora ya puede empezar a enviar solicitudes a la API.

## Funciones

La clase nomadoClient proporciona las interfaces públicas para acceder a la API de nomado

* `SMS`
* `OTP`
* `HLR`
* `Calls`
* `Account`
---

### SMS

##### sms.send()
Envía un SMS a uno o varios números.

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
Generar un código OTP y enviarlo vía sms a sus usuarios es tan fácil como se muestra a continuación:

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

Realizar una solicitud

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
