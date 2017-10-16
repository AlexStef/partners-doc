---
title: Scopes
position: 5
right_code: |
  ~~~ bash
  curl -u CLIENT_ID:CLIENT_SECRET "https://api.creads-partners.com/oauth2/token" -d 'grant_type=client_credentials' -d 'scope=files'
  ~~~
  {: title="Curl"}
  ~~~ json
  {
      "access_token": "MWFjYjgxZGRmMTRjMDA0MDUyYmNmODA5ZDRlNzFjYTc1NTZlYzc0ODMwYTc2OTE3NzIzYzY4ZDc0OGE4YWRhYg",
      "expires_in": 3600,
      "token_type": "bearer",
      "scope": "files"
  }
  ~~~
  {: title="Response"}
---

L'API Partners permet de demander un `access_token` pour un `scope` particulier lors de l'authentification. Par défaut, cette valeur est définie à `base`.

### Scopes existants

* **base**: Permet d'obtenir et modifier des resources et des fichiers (soumis aux règles de sécurité de l'utilisateur)
* **files**: Ne permet que d'obtenir des images ou des fichiers sur les endpoints prévus à cet effet.
* **upload_files**: Permet d'uploader des fichiers.

> Un token avec le scope `base` ne devrait **jamais** être exposé à un client. L'obtention de ce token par un tiers constitue une faille de sécurité

### Donner accès aux images à des utilisateurs anonymes

Si une application (grant type `client_credentials`) a besoin d'afficher une image à ses utilisateurs qui ne sont pas eux mêmes authentifiés sur Partners, les scopes permettent d'exposer un token non critique pour effectuer cet affichage.


Obtenir un access token pour les fichiers:

```
curl -u CLIENT_ID:CLIENT_SECRET "https://api.creads-partners.com/oauth2/token" -d 'grant_type=client_credentials' -d 'scope=files'
```

> remplacer `CLIENT_ID` par votre *Client ID*
> remplacer `CLIENT_SECRET` par votre *Client Secret*
> Remarquer *scope=files*

Réponse:
```
{
    "access_token": "MWFjYjgxZGRmMTRjMDA0MDUyYmNmODA5ZDRlNzFjYTc1NTZlYzc0ODMwYTc2OTE3NzIzYzY4ZDc0OGE4YWRhYg",
    "expires_in": 3600,
    "token_type": "bearer",
    "scope": "files"
}
```

Ce token peut maintenant être joint à l'url d'une image :

```
<img src="https://api.creads-partners.com/v1/img/whateverImage.png?access_token=ACCESS_TOKEN">
```

> remplacer `ACCESS_TOKEN` par la valeur de ce champ dans la réponse obtenue précédemment

