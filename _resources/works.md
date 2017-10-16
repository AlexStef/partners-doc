---
title: Work
position: 6
---

Dans le cas d'un projet multi, une ressource `Work` (travail) représente une création envoyée par un créatif pour un projet.

**En tant que qu'utilisateur simple, seuls les travaux des projets que vous avez créé ou auxquels vous avez été invité sont accessibles.**
{: .info }

**En tant qu'utilisateur *manager*, seuls les travaux des projets des organisations desquelles vous êtes *manager* sont accessibles.**
{: .info }

Il contient soit une image (`image`), soit dans le cas des concours de rédaction un contenu texte (`content`). Il est rattaché à un créatif (`Worker`) et peut avoir un autre `Work` parent. Les *enfants* d'un `work` sont des images (déclinaisons) que le créatif a souhaité grouper sous la même création.

Par exemple, pour obtenir les créations principales (parentes) d'un projet:

~~~ sh
curl -H "Authorization: Bearer $TOKEN" 'https://api.creads-partners.com/v1/works?query=\[\["project.gid","==","55c0d927cad5c"\],\["parent","==",null\]\]'
~~~

Réponse :
~~~ json
{
    "total_count": 4,
    "items": [
        {
          "gid": "559bf0527764e",
          "created_at": "2014-09-08T22:47:31-07:00",
          "won_at": null,
          "description" : "Quisque ac ligula faucibus, pretium orci ac, porta velit. Cras ante enim, lacinia a commodo ut, iaculis et sem. Sed faucibus leo id justo imperdiet sollicitudin. Nunc tempor et risus vitae pulvinar. Quisque sed lacinia erat, vitae efficitur turpis. Fusce vel mollis tortor. Vivamus fermentum lacus in ultricies euismod.",
          "image": "https://cre.ads/43348e3ea6-1.jpg",
          "worker": {
            "gid": "559bf0683e9a5"
          },
          "project": {
            "gid": "559bf06dc73e8",
            "title": "lorem ipsum dolor"
          }
        },
        ...
    ]
}
~~~

Pour terminer un projet et recevoir des fichiers sources lorsque vous êtes satisfait d'une création, il faut sélectionner un vainqueur.
Mettre à jour le projet en lui indiquant la création gagnante:

~~~
curl -i -H "Authorization: Bearer $TOKEN" -d '{
    "winner": {
        "gid": "559bf0527764e"
    }
}' -X PUT https://api-preprod.creads-partners.com/v1/projects/559bf06dc73e8
~~~

Le projet est alors terminé. Lorsque des **fichiers sources** arriveront, ils apparaitront dans la resource `project` en tant que `source_files`:

~~~ json
{
    "source_files": [
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
    ...
}
~~~
