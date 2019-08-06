## Descripción general
Este punto final le permite enviar uno o varios sms a la vez a cualquier país.

## Punto final de la API

?>**POST** `https://api.nomado.eu/sms/send`

## Autentificación
Puede elegir uno de los métodos de autentificación a los que se hace referencia [aquí](/es/authentication).

## Objeto Mensaje
El objeto JSON que representa el SMS a enviar. Debe ser incluido en el cuerpo de la solicitud (request).

| clave | descripción | requerido | valor por defecto |
|---|---|---|---|
|to|`array<string>` Array of`E164`formatted mobile numbers | Oui |  |
|message|`string` Your SMS message| Oui | |
|unicode|`boolean` Indicates whether your message contains non-gsm characters | Non | false |

!> Los mensajes SMS tienen un límite de 160 caracteres (70 si se utiliza unicode). Si el tamaño excede el límite, los mensajes se dividirán y se facturarán por separado.

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
  "to": ["32412345678","32423456789"],
  "message": "Hello world",
  "unicode": false
}
```


## Ejemplo de respuesta

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
