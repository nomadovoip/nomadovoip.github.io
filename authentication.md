# Authentication

All nomado REST API endpoints are protected with three authentication methods : User credentials, JSON Web Tokens and API Keys. 

> We recommend to use JSON Web Tokens and API Keys.
---
### User credentials

User credential based authentication is the easiest of all to test and explore nomado REST API. User credentials should be provided with each request in `Authorization` header base64 encoded and separated by `:`. 

Example:
If your `username` is myemail@myserver.com and your `password` is 123456, your base64(username:password) value would be: `bXllbWFpbEBteXNlcnZlci5jb206MTIzNDU2` 

> ```curl
> curl -X POST \
> https://api.nomado.eu \
> -H 'Authorization: BASIC bXllbWFpbEBteXNlcnZlci5jb206MTIzNDU2' 
> //Base64 encoding for myemail@myserver.com:123456
> ```
