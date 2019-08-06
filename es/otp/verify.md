## Descripción general
El OTP es inútil si no se puede verificar, ¿no? Veamos lo fácil que es verificar el OTP. ¡No requiere almacenamiento local!

## Punto final de la API

?>**POST** `https://api.nomado.eu/2fa/verify`

## Autentificación
Puede elegir uno de los métodos de autentificación a los que se hace referencia [aquí](/es/authentication).

## Objeto body
Es el objeto JSON que representa el OTP para verificar. Debe incluirse en el cuerpo de la solicitud.

| opciones | descripción | requerido | valor por defecto |
|---|---|:---:|---|
|number|`string` E164 formatted mobile number | Oui |  |
|token| `string` The OTP to verify| Oui | |

## Respuesta

| código de estado | descripción |
|:---:|---|
|200|`success` Request sent successfully |
|400|`bad request` Incorrect or missing parameters |
|401|`unauthorized` Invalid credentials or incorrect authentication method |

!> El OTP como su nombre sugiere, una vez verificado o caducado, será destruido.

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
  "number": "32412345678",
  "token": "1234"
}
```


## Ejemplo de respuesta
```json
{
    "code": 200,
    "message": "OK",
    "verify": true
}
```
