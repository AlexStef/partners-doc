---
title: Password
position: 3
right_code: |
  ~~~ bash
  curl -u CLIENT_ID:CLIENT_SECRET "https://api.creads-partners.com/oauth2/token?grant_type=password' -d 'grant_type=password&username=USERNAME&password=PASSWORD'
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

**password** grant type

Ce workflow permet d'authentifier des utilisateurs Partners différents.
Le serveur doit obtenir un *access token* et le stocker en l'associant à un utilisateur (en session par exemple).
L'*access token* devra être associé à toutes les requêtes effectuées par l'utilisateur.

> remplacer `CLIENT_ID` par votre *Client ID*
> remplacer `CLIENT_SECRET` par votre *Client Secret*
> remplacer `USERNAME` par l'email de l'utilisateur à authentifier
> remplacer `PASSWORD` par le mot de passe saisie par l'utilisateur à authentifier

