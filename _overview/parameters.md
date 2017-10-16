---
title: Paramètres
position: 2
right_code: |

  ~~~ bash
  curl -i https://api.creads-partners.com/v1/users?orderBy=created_at
  ~~~
  {: title="Curl" }
---

Plusieurs méthodes de l'API supportent des paramètres optionnels. Pour les requêtes GET, ormis les paramètres obligatoires présents dans le segment d'URL, les paramètres optionnels doivent être passés comme paramètre d'URL HTTP (query string parameter).

**Exemple**: On récupère la liste des utlisateurs, triés pas date de création.

Pour les requêtes POST, PUT et DELETE, mes paramètres ne sont pas inclus dans l'URL mais encodés en JSON dans le body de la requête dont l'entête `Content-Type` doit être initialisé à la valeur `application/json`.
~~~ bash
curl -i -X POST -d '{"firstname":"John"}' https://api.creads-partners.com/v1/users/55e80f4af117f
~~~
{: title="Curl" }
