---
title: Organization
position: 1
---

Une ressource `Organization` (organisation) représente un partenaire ou une sous-entité d'un partenaire. Elle isole les utilisateurs, produits, projets, travaux et factures par entité.

**Seules les organisations desquelles vous êtes membre ou manager sont accessibles.**

### Obtenir la liste des organisations

~~~ bash
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/organizations
~~~

Réponse :
~~~ json
{
    "total_count": 3,
    "items": [
        {
            "gid": "55f2ab761d0bd",
            "created_at": "2015-09-11T10:22:46+0000",
            "modified_at": "2015-09-11T10:22:46+0000",
            "href": "/organizations/55f2ab761d0bd",
            "name": "WayneCorp",
            "hostname": null,
            "vat": null,
            "billing_address": {
                "division": null,
                "address1": null,
                "address2": null,
                "zipcode": "10007",
                "city": "Gotham City",
                "state": null,
                "country": "US",
                "additional": null,
                "country_name": "États-Unis"
            }
        }
        ...
    ]
}
~~~

### Chercher des organisations

Le paramètre d'URL `query` appliqué au *endpoint* précédement évoqué permet d'effectuer une recherche dans les organisations. Pour savoir comment utiliser ce paramètre d'URL veuillez vous référer à [Recherche dans une collection](#overviewcollections).

Les champs sur lequel on peut effectuer une recherche sont les suivants :

 * `products.gid` : les organisations pour lesquelles un produit donné est activé

Par exemple, pour rechercher des organisations qui ont le produit de gid `55a6842ac3f6b` activé :
~~~ sh
curl -H "Authorization: Bearer $TOKEN" 'https://api.creads-partners.com/v1/organizations?query=\["products.gid","==","55a6842ac3f6b"\]'
~~~

### Obtenir une organisation (par son GID)

~~~ sh
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/organizations/55f2ab761d0bd
~~~

Réponse :
~~~ json
{
    "gid": "55f2ab761d0bd",
    "created_at": "2015-09-11T10:22:46+0000",
    "modified_at": "2015-09-11T10:22:46+0000",
    "href": "/organizations/55f2ab761d0bd",
    "name": "WayneCorp",
    "hostname": null,
    "vat": null,
    "billing_address": {
        "division": null,
        "address1": null,
        "address2": null,
        "zipcode": "10007",
        "city": "Gotham City",
        "state": null,
        "country": "US",
        "additional": null,
        "country_name": "États-Unis"
    }
}
~~~
