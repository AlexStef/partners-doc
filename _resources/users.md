---
title: User
position: 2
---

Une ressource `User` (utilisateur) représente un utilsateur de l'application.

Un utilisateur peut être désigné *manager* de l'organisation par un utilisateur *admin*.
Un manager a alors le droit de :
 * voir les bons de commande de tous les collaborateurs de l'organisation
 * inviter de nouveaux utilisateurs à utiliser l'outil (collaborateur)
 * configurer une limite de dépense pour chaque collaborateur

**Seuls votre compte utilisateur et les utilisateurs des organisations desquelles vous êtes *manager* sont accessibles.**

### Obtenir la liste des utilisateurs

~~~ sh
curl -i -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/users
~~~

Réponse :
~~~ json
{
    "total_count": 22,
    "items": [
        {
            "gid": "55f2a84f150a2",
            "created_at": "2015-09-11T10:09:19+0000",
            "modified_at": "2015-09-11T10:09:19+0000",
            "href": "/users/55f2a84f150a2",
            "firstname": "Doe",
            "lastname": "John",
            "email": "j.doe@creads.org",
            "locale": "FR",
            "phone": null,
            "mobile_phone": null,
            "member_of": [
                {
                    "gid": "55f2ac24163ed",
                    "monthly_budget": null,
                    "is_manager": false,
                    "monthly_spent": {
                        "amount": 0,
                        "currency": "EUR"
                    },
                    "organization": {
                        "gid": "55f2ab761d0bd",
                        "href": "/organizations/55f2ab761d0bd",
                        "name": "WayneCorp",
                        "hostname": null
                    }
                }
            ],
            "roles": [
                "user"
            ],
            "pending_email": null
        }
        ...
    ]
}
~~~

### Chercher des utilisateurs

Le paramètre d'URL `query` appliqué au *endpoint* précédement évoqué permet d'effectuer une recherche dans les organisations. Pour savoir comment utiliser ce paramètre d'URL veuillez vous référer à [Recherche dans une collection](#overviewcollections).

Les champs sur lequel on peut effectuer une recherche sont les suivants :

 * `created_at` : les utilisateurs en fontion de leur date de création
 * `modified_at` : les utilisateurs en fontion de leur date de dernière modification
 * `member_of.organization.gid` : les utilisateurs membres d'une organisation donnée

Par exemple, pour rechercher un utilisateur créé après minuit du 11/09/2015 (en temps universel) :
~~~ sh
curl -H "Authorization: Bearer $TOKEN" 'https://api.creads-partners.com/v1/users?query=\["created_at",">","2015-09-11T00:00:00Z"\]'
~~~

### Obtenir un utilisateur (par son GID)

~~~ sh
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/users/55f2a84f150a2
~~~

Réponse :
~~~ json
{
    "gid": "55f2a84f150a2",
    "created_at": "2015-09-11T10:09:19+0000",
    "modified_at": "2015-09-11T10:09:19+0000",
    "href": "/users/55f2a84f150a2",
    "firstname": "Doe",
    "lastname": "John",
    "email": "j.doe@creads.org",
    "locale": "FR",
    "phone": null,
    "mobile_phone": null,
    "member_of": [
        {
            "gid": "55f2ac24163ed",
            "monthly_budget": null,
            "is_manager": false,
            "monthly_spent": {
                "amount": 0,
                "currency": "EUR"
            },
            "organization": {
                "gid": "55f2ab761d0bd",
                "href": "/organizations/55f2ab761d0bd",
                "name": "WayneCorp",
                "hostname": null
            }
        }
    ],
    "roles": [
        "user"
    ],
    "pending_email": null
}
~~~
