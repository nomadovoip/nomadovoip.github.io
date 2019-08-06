# Autentificación

Todos los puntos finales de la API REST de nomado están protegidos con tres métodos de autentificación: Credenciales de usuario, JSON Web Tokens y Claves API (API Keys).

> Recomendamos el uso de JSON Web Tokens y Claves API.

---
### Credenciales de usuario

La autentificación basada en credenciales de usuario es la más fácil de todas para probar y explorar la API REST de nomado. Las credenciales de usuario deben proporcionarse con cada solicitud en el encabezado `Authorization`, codificadas en base64, y separadas por :.

Ejemplo:
Si su `username (nombre de usuario)` es myemail@myserver.com y su `password (contraseña)` es 123456, su valor en base64 (username:password) será: `bXllbWFpbEBteXNlcnZlci5jb206MTIzNDU2`


> ```curl
> curl -X POST \
> https://api.nomado.eu \
> -H 'Authorization: BASIC bXllbWFpbEBteXNlcnZlci5jb206MTIzNDU2' 
> //Base64 encoding for myemail@myserver.com:123456
> ```


!> Para los otros métodos, estamos trabajando en ello.