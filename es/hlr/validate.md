## Descripción general
No tan robusto como una búsqueda hlr, este punto final le permite obtener información básica sobre un número de teléfono, como por ejemplo si es un número de teléfono válido, un teléfono fijo o móvil, el país al que pertenece, etc. Esta búsqueda no le cuesta nada.


## Punto final de la API

?>**POST** `https://api.nomado.eu/hlr/validate`

## Autentificación
Puede elegir uno de los métodos de autentificación a los que se hace referencia [aquí](/es/authentication).

## URL para la petición
Sólo tiene que añadir el número a la URL del punto final de la API, como por ejemplo `https://api.nomado.eu/hlr/validate/[NÚMERO]` donde `[NÚMERO]` se reemplazará por el número real de móvil/celular en formato E164.


## Respuesta

| código de estado | descripción |
|:---:|---|
|200|`success` Request sent successfully |
|400|`bad request` Incorrect or missing parameters |
|401|`unauthorized` Invalid credentials or incorrect authentication method |

___

## Ejemplo de solicitud
Cabeceras
```
Content-type: application/json
Authorization: BASIC base64encodedCredentials
```

URL para la petición
`https://api.nomado.eu/hlr/validate/32456789012`


## Ejemplo de respuesta
```json
{
    "Status": "Valid",
    "Region": "BE",
    "CountryCode": 32,
    "Type": "Mobile"
}
```
