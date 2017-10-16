---
title: Product
position: 3
---

Une ressource `Product` (produit) représente un produit qu'un utilisateur de votre organisation peut commander.

**Seuls les produits activés dans les organisations desquelles vous êtes membre ou *manager* sont accessibles.**

### Obtenir la liste des produits

Pour une organisation donnée, vous pouvez obtenir la liste des produits possibles à commander

~~~ sh
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/orgs/55f2ab761d0bd/products
~~~

Réponse :
~~~ json
{
    "total_count": 14,
    "items": [
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
            "interface": "default"
        },
        ...
    ]
}
~~~

### Chercher des produits

Le paramètre d'URL `query` appliqué au *endpoint* précédement évoqué permet d'effectuer une recherche dans les produits. Pour savoir comment utiliser ce paramètre d'URL veuillez vous référer à [Recherche dans une collection](#overviewcollections).

Les champs sur lesquels on peut effectuer une recherche sont les suivants :

 * `category.id` : les produits d'une catégorie donnée
 * `organizations.gid` : les produits activés dans une organisation donnée

Par exemple, pour rechercher la produits de la catégorie *Logo & Identité* :
~~~ sh
curl -H "Authorization: Bearer $TOKEN" 'https://api.creads-partners.com/v1/products?query=\["category.gid","==","55c0d9279d5a6"\]'
~~~

### Obtenir un produit (par son GID)

~~~ sh
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
