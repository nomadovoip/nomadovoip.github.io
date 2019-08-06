## Descripción general

OTP es la abreviatura de One time password / pin. La configuración de OTP desde cero es engorrosa y requiere algunas tareas como generar un pin aleatorio, almacenarlo para su verificación (incluyendo configurar la base de datos), enviar el token a través de sms, crear puntos finales para la verificación posterior, etc. Esta función le permite saltarse todos los problemas y utilizar nuestro OTP como servicio de forma gratuita (se aplica el cargo normal por sms).

Este punto final le permite implementar la Autentificación de Doble Factor de la manera fácil, enviando un SMS con OTP.

## Punto final de la API

?>**POST** `https://api.nomado.eu/2fa/create`

## Autentificación
Puede elegir uno de los métodos de autentificación a los que se hace referencia [aquí](/es/authentication).

## Objeto body
Es el objeto JSON que representa el OTP a enviar. Debe incluirse en el cuerpo de la solicitud.


| opciones | descripción | requerido | valor por defecto |
|---|---|:---:|---|
|to|`string` E164 formatted mobile number | Si |  |
|template| `string` MUST contain `{{CODE}}` literal in it, which will be replaced by the generated OTP| Non | {{CODE} |
|type| `string` Type of OTP required. Possible values: `ALPHA`, `NUMERIC` and `ALPHANUMERIC`| No | ALPHANUMERIC |
|length|`Integer`  length of the OTP required. `Max 20`| No | 4 |
|expiry| `Integer` time in seconds after which the OTP will expire automatically.| No | 7200 |

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
  "to": "32412345678",
  "template": "Your verification code is {{CODE}}",
  "type": "NUMERIC",
  "length": 4,
  "expiry": 7200
}
```


## Ejemplo de respuesta
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
