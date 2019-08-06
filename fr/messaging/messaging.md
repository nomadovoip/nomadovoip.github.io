## Général
Ce point de terminaison vous permet d’envoyer un ou plusieurs sms à la fois dans n’importe quel pays.

## Point de terminaison de l'API

?>**POST** `https://api.nomado.eu/sms/send`

## Authentification
Vous pouvez choisir l'une des méthodes d'authentification référencées [ici](/authentication.md).

## Objet message
L'objet JSON représentant le SMS à envoyer devrait être inclus dans le corps de la demande.

| clé | description | requis | valeur par défaut |
|---|---|---|---|
|vers|`array<string>` Array of`E164`formatted mobile numbers | Oui |  |
|message|`string` Your SMS message| Oui | |
|unicode|`boolean` Indicates whether your message contains non-gsm characters | Non | false |

!> Les messages SMS sont limités à 160 caractères (70 si unicode est utilisé). Si la taille dépasse cette limite, les messages seront fractionnés et facturés séparément.

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
  "to": ["32412345678","32423456789"],
  "message": "Hello world",
  "unicode": false
}
```


## Exemple de réponse

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
