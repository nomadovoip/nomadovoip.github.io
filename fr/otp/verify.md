## Général
L’OTP est inutile si vous ne pouvez pas le vérifier, n'est-ce pas? Voyons à quel point il est facile de vérifier l'OTP. pas de stockage local requis!

## Point de terminaison de l'API

?>**POST** `https://api.nomado.eu/2fa/verify`

## Authentification
Vous pouvez choisir l'une des méthodes d'authentification référencées [ici](/fr/authentication.md).

## L’objet du corps
L'objet JSON représentant l’OTP à envoyer devrait être inclus dans le corps de la demande.

| options | description | requis | valeur par défaut |
|---|---|:---:|---|
|number|`string` E164 formatted mobile number | Oui |  |
|token| `string` The OTP to verify| Oui | |

## Réponse

| code du status | description |
|:---:|---|
|200|`success` Request sent successfully |
|400|`bad request` Incorrect or missing parameters |
|401|`unauthorized` Invalid credentials or incorrect authentication method |

!> L’OTP, comme son nom l’indique, une fois vérifié ou expiré, sera détruit.

___

## Exemple de requête
En-têtes
```
Content-type: application/json
Authorization: BASIC base64encodedCredentials
```
Corps
```json
{
  "number": "32412345678",
  "token": "1234"
}
```


## Exemple de réponse
```json
{
    "code": 200,
    "message": "OK",
    "verify": true
}
```
