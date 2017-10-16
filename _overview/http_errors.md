---
title: Erreurs HTTP
position: 3
right_code: |

  ~~~ json
  {"error":{"code":403,"message":"Forbidden"}}
  ~~~
  {: title="Error schema" }
---

Il y a plusieurs sortes d'erreurs possibles.

1. Envoyer un JSON invalid provoquera une réponse `400 Bad Request`
2. Envoyer une requête non-identifiée ou avec un token invalide provoquera une réponse `401 Unauthorized`
3. Envoyer une requête à un endpoint nécessitant des droits supérieurs provoquera une réponse `403 Forbidden`
4. Envoyer une requête à une ressource inexistante provoquera une réponse `404 Not found`
5. Envoyer une requête des champs invalides provoquera une réponse `422 Unprocessable Entity`

L'erreur 422 n'est **pas supportée dans la version** actuelle. Renvoie *400 Bad Request* en lieu et place.
{: .warning }
