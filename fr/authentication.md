# Authentification

Tous les points de terminaison de l'API REST de nomado sont protégés par trois méthodes d'authentification: informations d'identification de l'utilisateur, jetons Web JSON et clés d’API (API keys).

> Nous vous recommandons d'utiliser des jetons Web JSON et des clés d'API.

---
### Informations d'identification de l’utilisateur 

L'authentification basée sur les informations d'identification de l'utilisateur est le moyen le plus facile de tester et d'explorer l'API REST nomado. Les informations d'identification de l'utilisateur doivent être fournies avec chaque demande dans l'en-tête Authorization codée en base64 et séparés par `:`.

Exemple:
Si votre `username (identifiant)` est monmail@monserveur.com et votre `password (mot de passe)` est 123456, votre valeur base64 (username:password) sera: `bXllbWFpbEBteXNlcnZlci5jb206MTIzNDU2`


> ```curl
> curl -X POST \
> https://api.nomado.eu \
> -H 'Authorization: BASIC bXllbWFpbEBteXNlcnZlci5jb206MTIzNDU2' 
> //Base64 encoding for myemail@myserver.com:123456
> ```


!> Pour les autres méthodes, nous y travaillons d’arrache pied.