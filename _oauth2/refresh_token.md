---
title: Refresh token
position: 4
right_code: |
  ~~~ bash
  curl -u CLIENT_ID:CLIENT_SECRET "https://api.creads-partners.com/oauth2/token?grant_type=password' -d 'grant_type=refresh_token&refresh_token=REFRESH_TOKEN'
  ~~~
  {: title="Curl"}
  ~~~ json
  {
      "access_token": "NWE4MmVmZjgyYjA1NTBkODI5ZDY1ZmFlMGZlZmIyZTE1NDE1MWM2ZmQ0NjEwMjNlYmI0M2MxNDYxOTMyNmFlMQ",
      "expires_in": 3600,
      "token_type": "bearer",
      "scope": "base",
      "refresh_token": "ZWNmZWEwNjU0OTY5ZjUxMThjN2VlM2NkMjI5MDk1OWM3MGE1NTI2OTNmMzUwZWU3M2MzZTc0ZmFiMmVhYTk4Nw"
  }
  ~~~
  {: title="Response"}
---

*refresh_token* grant type

**refresh_token** grant type

Permet de raffraichir un *access token* OAuth2 sans redemander le mot de passe de l'utilisateur.
A l'obtention d'un *access token* et son stockage sur le serveur, on peut également stocker un *refresh token*.
Ce *refresh token* valable pour une plus longue durée permettra d'obtenir un nouvel *access token* pour un utilisateur Partners sans le forcer à resaisir son mot de passe.

> remplacer `CLIENT_ID` par votre *Client ID*
> remplacer `CLIENT_SECRET` par votre *Client Secret*
> remplacer `REFRESH_TOKEN` par le *refresh token* obtenu avec l'*access token*


