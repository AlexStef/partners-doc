---
title: Schema
position: 1
right_code: |

  ~~~ bash
  curl -i https://api.creads-partners.com/v1/
  ~~~
  {: title="Curl" }
  ~~~ json
  {
    "name": "Creads Partners API",
    "version": "1.0.0"
  }
  ~~~
  {: title="Response" }
---

Tous les accès à API se font sur couche HTTPS, sur le domaine `api.creads-partners.com`. Toutes les données sont envoyées et reçues en *JSON*.

Les champs vides sont inclus en tant que valeur `null` plutôt que d'être omis.
{: .info }


Toutes les dates sont renvoyées au format **ISO 8601**:
`YYYY-MM-DDTHH:MM:SS+0000`
{: .info }

#### Représentation partielle ####

Quand vous récupérez une liste de ressources, la réponse contient une sous-sélection d'attributs de cette ressource.

**Exemple**: Quand vous récupérer la liste des catégories de produits `https://api.creads-partners.com/v1/categories`, vous obtenez une représentation partielle de chaque categorie.

~~~ json
{
    "total_count": 7,
    "items": [
        {
            "gid": "55e80f50da498",
            "created_at": "2015-09-03T09:13:52+0000",
            "modified_at": "2015-09-03T09:13:52+0000",
            "href": "/categories/55e80f50da498",
            "is_removable": true,
            "title": "Exécution graphique"
        },
        {
            "gid": "55e80f50da568",
            "created_at": "2015-09-03T09:13:52+0000",
            "modified_at": "2015-09-03T09:13:52+0000",
            "href": "/categories/55e80f50da568",
            "is_removable": false,
            "title": "Logo & Identité"
        }
    ]
}
~~~
{: title="Response" }

#### Représentation complète ####

Quand vous récupérez une ressource individuelle, la réponse renvoyée contient généralement tous les attributs pour cette ressource. C'est la vue "complète" de la ressource. (Notez que vos droits d'accès sur l'API peuvent influencer la présence de certains champs.)

**Exemple**: Quand vous récupérez une catégorie de produits `https://api.creads-partners.com/v1/categories/{gid}`, sa représentation contient tous les champs.

~~~ json
{
    "gid": "55e80f50da498",
    "created_at": "2015-09-03T09:13:52+0000",
    "modified_at": "2015-09-03T09:13:52+0000",
    "href": "/categories/55e80f50da498",
    "is_removable": true,
    "title": "Exécution graphique",
    "description": "Détourage photo, retouches photo, adaptation de fichiers..."
}
~~~
{: title="Response" }

#### Représentation de référence ####

Quand vous récupérez une ressource à laquelle est associée à une autre ressource, cette autre ressource apparait en sous-élement représenté partiellement. Cette représentation est une "représentation de référence" contenant les éléments essentiels pour identifier la resource associée.

**Exemple**: Quand vous récupérer un projet `https://api.creads-partners.com/v1/projects/{gid}`, sa représentation contient une référence owner vous permettant de retrouver l'utilisateur qui à créé le project.

~~~ json
{
    "gid": "55e80f5163e3a",
    "owner": {
        "gid": "55e80f4b9f4c9",
        "href": "/users/55e80f4b9f4c9"
    }
}
~~~
{: title="Response" }

