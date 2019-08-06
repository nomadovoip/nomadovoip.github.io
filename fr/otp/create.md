## Général
OTP signifie mot de passe / pin unique ou à usage unique. Configurer un OTP à partir de zéro est fastidieux et nécessite beaucoup de tâches manuelles telles que : générer un code pin aléatoire, le stocker pour vérification (y compris la configuration de la base de données), envoyer le jeton par SMS, écrire des points de terminaison pour une vérification ultérieure, etc. 
Cette fonction vous permet de passer outre tous ces problèmes et utiliser notre service OTP sans générer des frais de développement (mis à part les coûts de sms normaux)

Ce point de terminaison vous permet d’implémenter facilement l’authentification à deux facteurs en envoyant un SMS avec OTP..

## Point de terminaison de l'API

?>**POST** `https://api.nomado.eu/2fa/create`

## Authentification
Vous pouvez choisir l'une des méthodes d'authentification référencées [ici](/fr/authentication.md).

## L’objet du corps
L'objet JSON représentant l’OTP à envoyer devrait être inclus dans le corps de la demande.


| options | description | requis | valeur par défaut |
|---|---|:---:|---|
|to|`string` E164 formatted mobile number | Oui |  |
|template| `string` MUST contain `{{CODE}}` literal in it, which will be replaced by the generated OTP| Non | {{CODE} |
|type| `string` Type of OTP required. Possible values: `ALPHA`, `NUMERIC` and `ALPHANUMERIC`| Non | ALPHANUMERIC |
|length|`Integer`  length of the OTP required. `Max 20`| Non | 4 |
|expiry| `Integer` time in seconds after which the OTP will expire automatically.| Non | 7200 |

## Réponse

| code du status | description |
|:---:|---|
|200|`success` Request sent successfully |
|400|`bad request` Incorrect or missing parameters |
|401|`unauthorized` Invalid credentials or incorrect authentication method |

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
  "to": "32412345678",
  "template": "Your verification code is {{CODE}}",
  "type": "NUMERIC",
  "length": 4,
  "expiry": 7200
}
```


## Exemple de réponse
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
