---
title: Project
position: 4
---


Une ressource `Project` représente une commande d'un produit qu'un utilisateur peut effectuer.

**En tant que qu'utilisateur simple, seuls les projets que vous avez créés ou auxquels vous êtes invités à collaborer sont accessibles.**
{: .info }

**En tant qu'utilisateur *manager*, seuls les projets créés dans les organisations desquelles vous êtes *manager* sont accessibles.**
{: .info }


### Obtenir la liste des projets

~~~ bash
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/projects
~~~

Réponse :
~~~ json
{
    "total_count": 4,
    "items": [
        {
            "gid": "55c0d927cad5c",
            "created_at": "2015-08-04T15:24:23+0000",
            "modified_at": "2015-08-04T15:24:23+0000",
            "href": "/projects/55c0d927cad5c",
            "started_at": "2015-08-04T15:24:23+0000",
            "finished_at": null,
            "status": "in_progress",
            "title": "Malesuada",
            "description": "Caesaris observante",
            "options": {
                "due": 1,
                "mode": "solo",
                "skill": "conception"
            },
            "quantity": 1,
            "owner": {
                "gid": "55f2a84f150a2",
                "href": "/users/55f2a84f150a2"
            },
            "organization":         {
                "gid": "55f2ab761d0bd",
                "href": "/organizations/55f2ab761d0bd",
                "name": "WayneCorp",
                "hostname": null
            },
            "product": {
                "gid": "55a6842ac3f6b",
                "href": "/products/55a6842ac3f6b"
            },
            "brief_files": [],
            "source_files": [],
            "receipt_file": null,
            "price": {
                "amount": 1470,
                "currency": "EUR"
            },
            "vat": {
                "amount": 0,
                "ratio": 0,
                "currency": "EUR"
            },
            "winner": null
        },
        ...
    ]
}
~~~

### Chercher des projets

Le paramètre d'URL `query` appliqué au *endpoint* précédement évoqué permet d'effectuer une recherche dans les projets. Pour savoir comment utiliser ce paramètre d'URL veuillez vous référer à [Recherche dans une collection](#overviewcollections).

Les champs sur lesquels on peut effectuer une recherche sont les suivants :

 * `organization.id` : les projets d'une organisation donnée.
 * `owner.gid` : les projets créés par un utilisateur donnée.
 * `status` : les projets dans un état donné.
 * `created_at` : les projets créés par rapport à une date donnée.


Par exemple, pour rechercher les projets créés dans l'organization *WayneCorp* depuis le début de l'année :
~~~ sh
curl -H "Authorization: Bearer $TOKEN" 'https://api.creads-partners.com/v1/projects?query=\[\["organization.gid","==","55f2ab761d0bd"\],\["created_at",">=","2015-01-01T00:00:00Z"\]\]'
~~~

### Obtenir un projet (par son GID)

~~~ sh
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/project/55c0d927cad5c
~~~

Réponse :
~~~ json
{
    "gid": "55c0d927cad5c",
    "created_at": "2015-08-04T15:24:23+0000",
    "modified_at": "2015-08-04T15:24:23+0000",
    "href": "/projects/55c0d927cad5c",
    "started_at": "2015-08-04T15:24:23+0000",
    "finished_at": null,
    "status": "in_progress",
    "title": "Malesuada",
    "description": "Caesaris observante",
    "options": {
        "due": 1,
        "mode": "solo",
        "skill": "conception"
    },
    "quantity": 1,
    "owner": {
        "gid": "55f2a84f150a2",
        "href": "/users/55f2a84f150a2"
    },
    "organization":         {
        "gid": "55f2ab761d0bd",
        "href": "/organizations/55f2ab761d0bd",
        "name": "WayneCorp",
        "hostname": null
    },
    "product": {
        "gid": "55a6842ac3f6b",
        "href": "/products/55a6842ac3f6b"
    },
    "brief_files": [],
    "source_files": [],
    "receipt_file": null,
    "price": {
        "amount": 1470,
        "currency": "EUR"
    },
    "vat": {
        "amount": 0,
        "ratio": 0,
        "currency": "EUR"
    },
    "winner": null
}
~~~

### Créer un projet

Un projet est une commande d'un produit dans une configuration donnée.

#### Obtenir les options du produit

Avant de créer un projet, on doit d'abord connaitre les options disponibles pour le produit du projet (mode, délai, métier...) et s'il peut être cumulé.
Cette récupération peut être faite une fois pour toute car l'on suppose qu'un produit ne perdra pas ou ne changera pas de caractéristique.

Obtention du produit "Logo" :
~~~
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/products/55a6842ac3f6b
~~~

Réponse :
~~~ json
{
    "gid": "55a6842ac3f6b",
    "created_at": "2015-08-04T15:24:23+0000",
    "modified_at": "2015-09-11T12:22:06+0000",
    "href": "/products/55a6842ac3f6b",
    "category": {
        "gid": "55c0d9279d5a6",
        "href": "/categories/55c0d9279d5a6",
        "title": "Logo & Identité"
    },
    "title": "Logo",
    "available_options": {
        "due": {
            "type": "integer",
            "default": 5,
            "required": true,
            "enum": [
                1,
                2,
                5,
                10
            ]
        },
        "mode": {
            "type": "string",
            "default": "solo",
            "required": true,
            "enum": [
                "solo",
                "multi"
            ]
        },
        "skill": {
            "type": "string",
            "default": "conception",
            "required": true,
            "enum": [
                "conception",
                "execution"
            ]
        }
    },
    "additional_meta": {
        "solo_mode_meta": {
            "description": "- Sollicitation d'un designer professionnel pour votre projet.\n- Recevez 3 propositions de logo.\n- 3 aller/retours sur celle de votre choix et recevez les fichiers sources.",
            "brief_template": "Décrivez votre besoin, le contexte du projet, les livrables attendus..."
        },
        "multi_mode_meta": {
            "description": "- Sollicitation de 3 designers professionnels pour votre projet.\n- Recevez 9 propositions de logo.\n- 3 aller/retours sur celle de votre choix et recevez les fichiers sources.",
            "brief_template": "Décrivez votre besoin, le contexte du projet, les livrables attendus..."
        }
    },
    "is_enabled": true,
    "is_cumulative": false,
    "interface": "default",
    "organizations": [
        {
            "gid": "55f2ab761d0bd",
            "href": "/organizations/55f2ab761d0bd",
            "name": "WayneCorp",
            "hostname": null
        }
    ]
}
~~~

Le champ `available_options` indique au format [JSON Schema](http://json-schema.org/) les différentes options disponibles à la création du projet:

* `available_options.due` est le délai de rendu souhaité exprimé en jours. Observez la valeur `available_options.due.enum` pour savoir quels sont les délais possibles pour le produit.
* `available_options.mode` est le mode de travail souhaité. Observez la valeur `available_options.mode.enum` pour savoir quels sont les modes possibles pour le produit.
* `available_options.skill` est l'expertise métier souhaitée (Direction artistique, exécution, ...). Observez la valeur `available_options.skill.enum` pour savoir quels sont les modes possibles pour le produit.

Le champ `is_cumulative` est un booléen indiquant s'il est à `true` que le produit peut être commandé en quantité.

Le champ `additional_meta` contient des meta-données non-essentielles :
* `additional_meta.solo_mode_meta`: description détaillée du mode solo
* `additional_meta.multi_mode_meta`: description détaillée du mode multi

#### Calculer le prix d'un projet

La création d'un projet nécessite la vérification et l'approbation du prix de ce projet
Pour ce faire, le prix correct du projet doit être calculé puis soumis à la création du projet (`POST /projects`).

Par exemple, calcul du prix pour une commande en 2 jours d'un *Logo* en mode *solo* en *Direction artistique* :
~~~
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/prices/for?product.gid=55a6842ac3f6b&organization.gid=55f2ab761d0bd&options.due=2&options.mode=solo&options.skill=conception
~~~

Réponse :
~~~
{
    "gid": "55f307e922d88",
    "created_at": "2015-09-11T16:57:13+0000",
    "modified_at": "2015-09-11T16:57:13+0000",
    "href": "/prices/55f307e922d88",
    "organization": null,
    "product": {
        "gid": "55a6842ac3f6b",
        "href": "/products/55a6842ac3f6b"
    },
    "options": {
        "mode": "solo",
        "due": 2,
        "skill": "conception"
    },
    "amount": 735,
    "currency": "EUR"
}
~~~

#### Créer le projet

Un projet peut être créé en état de brouillon (`state: draft`) pour pouvoir être modifié avant lancement définitif de la commande, ou définitivement lancé (`state: published`).

Les options du projet doivent être précisées (voir *Obtenir les options du produit*).
{: .info }

Le prix calculé au préalable doit être soumis à titre d'approbation (voir *Calculer le prix d'un projet*).
{: .info }

Par exemple, création d'une commande en 2 jours d'un *Logo* en mode *solo* et *Direction artistique* avec validation du prix à 990.0€ :
~~~
curl -i -H "Authorization: Bearer $TOKEN" -d '{
    "title": "titre du projet",
    "description": "Description précise de la commande (brief)",
    "product": {"gid": "55a6842ac3f6b"},
    "organization": {"gid": "55f2ab761d0bd"},
    "options": {"due":2, "mode": "solo", "skill": "conception"},
    "price": {"amount": 735.0},
    "status": "in_progress"
}' -X POST https://api-preprod.creads-partners.com/v1/projects
~~~


Second exemple, création d'une commande en 2 jours de 3 *Logos* en mode *multi* et *Execution* avec validation du prix à 1800.0€ à l'état de brouillon :
~~~
curl -H "Authorization: Bearer $TOKEN" -d '{
    "title": "titre du projet 2",
    "description": "Description précise de la commande (brief)",
    "product": {"gid": "55a6842ac3f6b"},
    "organization": {"gid": "55f2ab761d0bd"},
    "options": {"due":2, "mode": "multi", "skill": "execution"},
    "price": {"amount": 1800.0},
    "state": "draft",
    "quantity": 3
}' -X POST https://api.creads-partners.com/v1/projects
~~~

Réponse :
~~~
HTTP/1.1 201 Created
Cache-Control: no-cache
Content-Type: application/json
Date: Fri, 18 Sep 2015 16:29:25 GMT
Location: /v1/projects/55fc3be3a69db
Server: nginx/1.6.2
Content-Length: 0
Connection: keep-alive
~~~

En complément, le project accepte un tableau de fichiers de brief qui peuvent accompagner la commande pour guider les créatifs.

~~~ json
"brief_files": [
    {
        "url": "https://cre.ads/43348e3ea6-1.zip",
    },
    {
        "url": "https://cre.ads/43348e3ea6-2.zip",
    },
    {
        "url": "https://cre.ads/43348e3ea6-3.zip"
    }
],
~~~

### Modifier un projet

**En tant que qu'utilisateur, seuls les les projets que vous avez créé sont modifiables.**
{: .info }


## Works/Messages

* Dans le cadre des projets **solo** (avec un seul créatif), les projets sont gérés en mode **Project Box**. Des messages (resource `Project Message`) seront ajoutés au projet lorsque le créatif fera des propositions.
* Dans le cadre des projets **multi** (avec plusieurs créatifs), des créations (resource `Works`) seront ajoutés au projet lorsque des créatifs feront des propositions.
