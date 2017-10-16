---
title: Authentification
position: 6
---

En dehors du endpoint de base `https://api.creads-partners.com/v1/`, tous les autres endpoints nécessitent d'être authentifié pour être interrogés. Certaines requêtes non-authentifiées peuvent retourner `404 Not Found` au lieu de `403 Forbidden` pour prévenir de fuites de sécurité.

L'authentification se fait grâce à un token OAuth2 (access token). Veuillez lire la section [authentication OAuth2](doc/api/oauth2) pour plus d'information sur les méthodes pour obtenir un access token.

Il y a deux solutions pour authentifier les requêtes à l'aide du token OAuth2:

**Token Oauth2 envoyé en en-têtes:**

~~~ bash
curl -H "Authorization: Bearer OAUTH-TOKEN" https://api.creads-partners.com/v1/me
~~~
{: title="Curl" }

**Token Oauth2 envoyé en paramètre d'URL:**

~~~ bash
curl https://api.creads-partners.com/v1/me?access_token=OAUTH-TOKEN
~~~
{: title="Curl" }

Si l'authentification échoue, la réponse retournée prendra la forme d'une 401 Unauthorized:

~~~ json
{
    "error": "invalid_grant",
    "error_description": "The access token provided is invalid."
}
~~~
{: title="Response" }
