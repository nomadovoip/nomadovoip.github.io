## Descripción general
El **Home Location Register** o HLR, es una base de datos de todos los teléfonos móviles de este planeta conectados a su red móvil particular. `HLR Lookup` le permite encontrar información importante sobre un número, como la red original, la red actual, el estado de roaming, la validación de números, el estado actual, etc.

## Punto final de la API

?>**POST** `https://api.nomado.eu/hlr`

## Autentificación
Puede elegir uno de los métodos de autentificación a los que se hace referencia [aquí](/es/authentication).

## Objeto body
El objeto JSON que representa los números a buscar. Debe incluirse en el cuerpo de la solicitud.


| opciones | descripción | requerido | valor por defecto |
|---|---|:---:|---|
|numbers|`array<string>` tableau des numéros mobiles formatés E164 | Si |  |


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
Cuerpo
```json
{
  "numbers": ["32412345678","32423456789"]
}
```


## Ejemplo de respuesta
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
