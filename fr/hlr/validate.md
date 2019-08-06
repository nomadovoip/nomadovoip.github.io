## Général
Pas aussi robuste qu'une recherche hlr, ce point de terminaison vous permet de récupérer des informations de base concernant un numéro de téléphone, par exemple s'il s'agit d'un numéro de téléphone valide, d'un téléphone fixe ou mobile, du pays auquel il appartient, etc. Cette recherche ne vous coûte rien.


## Point de terminaison de l’API

?>**POST** `https://api.nomado.eu/hlr/validate`

## Authentification
Vous pouvez choisir l'une des méthodes d'authentification référencées [ici](/fr/authentication.md).

## Requête URL
Il vous suffit d’ajouter le numéro au point de terminaison, comme `https://api.nomado.eu/hlr/validate/[NUMBER]` où `[NUMBER]` serait remplacé par le numéro de mobile formaté E164


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

Query URL
`https://api.nomado.eu/hlr/validate/32456789012`


## Exemple de réponse
```json
{
    "Status": "Valid",
    "Region": "BE",
    "CountryCode": 32,
    "Type": "Mobile"
}
```
