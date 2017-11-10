# Errors

<aside class="notice">A API da TRUSTHUB pode retornar seguintes erros genéricos: </aside>

Error Code | Meaning
---------- | -------
401 | Unauthorized --  Requires HTTP authentication
401 | Unauthorized --  Ip not permited
404 | Not Found -- The specified request could not be found.
405 | Method Not Allowed -- You tried to access a resource with an invalid method.
406 | Not Acceptable -- Limit pagination not acceptable.
406 | Not Acceptable -- Compression Type not acceptable.
406 | Not Acceptable -- You requested a format that isn't json.
429 | Too Many Requests -- You're requesting too many !
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
