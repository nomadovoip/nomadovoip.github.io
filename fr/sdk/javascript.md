# Javascript SDK

[Github](https://github.com/nomadovoip/nomado-node) | [npm](https://www.npmjs.com/package/nomado)

Le moyen le plus simple et le plus recommandé (lire: le plus intelligent) d'utiliser l'API REST de nomado dans votre application nodejs consiste à utiliser notre sdk.


---

## Installation

```javascript
npm install nomado
```

---

## Démarrage rapide

!> Si vous n’avez pas encore de compte nomado, [créez-en un ici](https://my.nomado.eu/join) et recevez jusqu’à 10€ de crédit pour continuer et tester.

Voici un exemple rapide pour initialiser la librairie et envoyer un SMS.

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
### Réponses
Chaque appel renverra une promesse qui sera résolue (ou rejetée) avec un objet nomadoResponse encapsulant le code de réponse de l'API et les données.

```javascript
// Result object:
{
  code: 200, //OK!
  reason: "", //in case of error
  data: {}
}
```

---
### Authentification
Commencez par initialiser la librairie avec vos identifiants nomado.

```javascript 
const nomado = new nomadoClient({USERNAME, PASSWORD});
```

Vous pouvez maintenant commencer à envoyer des demandes à l'API.

## Fonctions

La classe nomadoClient fournit les interfaces publiques pour accéder à l'API nomado

* `SMS`
* `OTP`
* `HLR`
* `Calls`
* `Account`
---

### SMS

##### sms.send()
Envoyer un SMS vers un ou plusieurs numéros.

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
Générer un code OTP (code PIN à usiage unique) et envoyer des SMS à vos utilisateurs est aussi simple que ci-dessous:

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

Effectuer une requête

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
