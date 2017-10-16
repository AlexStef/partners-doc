---
title: App Server
position: 2
right_code: |
  ~~~ bash
  curl -u CLIENT_ID:CLIENT_SECRET "https://api.creads-partners.com/oauth2/token" -d 'grant_type=client_credentials'
  ~~~
  {: title="Curl"}
  ~~~ json
  {
      "access_token": "MWFjYjgxZGRmMTRjMDA0MDUyYmNmODA5ZDRlNzFjYTc1NTZlYzc0ODMwYTc2OTE3NzIzYzY4ZDc0OGE4YWRhYg",
      "expires_in": 3600,
      "token_type": "bearer",
      "scope": "base"
  }
  ~~~
  {: title="Response"}
---


**client_credentials** grant type

Ce workflow permet d'authentifier une application qui ne nécessite pas d'authentification de plusieurs utilisateurs Partners différents.

> remplacer `CLIENT_ID` par votre *Client ID*
> remplacer `CLIENT_SECRET` par votre *Client Secret*

