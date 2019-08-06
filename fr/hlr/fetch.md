## Général
**Home Location Register** ou HLR, est une base de données de tous les téléphones mobiles de cette planète connectés à leur réseau mobile particulier. `HLR Lookup`  vous permet de trouver des informations importantes sur un numéro. tels que le réseau d'origine, le réseau actuel, l'état d'itinérance, la validation du numéro, l'état actuel, etc.

## Point de terminaison de l’API

?>**POST** `https://api.nomado.eu/hlr`

## Authentification
Vous pouvez choisir l'une des méthodes d'authentification référencées [ici](/fr/authentication.md).

## L’objet du corps
L'objet JSON représentant le numéro à vérifier devrait être inclus dans le corps de la demande. 


| options | description | requis | valeur par défaut |
|---|---|:---:|---|
|numbers|`array<string>` tableau des numéros mobiles formatés E164 | Yes |  |


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
  "numbers": ["32412345678","32423456789"]
}
```


## Exemple de réponse
```json
{
    "code": 200,
    "data": {
        "3245678901": { ... },
        "3245678902": { ... },
        "valid_numbers": 2
    },
    "cost": 0.05
}
```
