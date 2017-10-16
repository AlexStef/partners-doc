---
title: Project Message
position: 5
---

Dans le cas d'un projet solo, le contact avec le créatif s'effectue sous forme conversationnelle.

Le créatif postera ses questions et ses propositions qui apparaitront comme des messages. Le client peut répondre sous la même forme.

Ces messages acceptent des pièces jointes (`attached_files`).

Vous pouvez obtenir la liste des messages existants dans un projet :

~~~ bash
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/projects/55c0d927cad5c/messages
~~~

Réponse :
~~~ json
{
    "total_count": 1,
    "items": [
        {
          "gid": "559befeeab59f",
          "href": "/project-message/559befeeab59f",
          "created_at": "2014-09-08T22:47:31-07:00",
          "modified_at": "2014-09-08T22:47:31-07:00",
          "accepted_at": null,
          "rejected_at": null,
          "message": "Lorem ipsum dolor sit amet",
          "project": {
            "gid": "559befeeab59a"
          },
          "mine": false,
          "worker": {
            "gid": "559befeeab59b"
          },
          "user": null,
          "type": "simple",
          "attached_files": [
            {
              "url": "https://cre.ads/43348e3ea6-1.zip"
            },
            {
              "url": "https://cre.ads/43348e3ea6-2.zip",
            }
          ]
        },
        ...
    ]
}
~~~

Les utilisateurs ayant accès au projet peuvent poster des messages sur ce même endpoint.

~~~
curl -i -H "Authorization: Bearer $TOKEN" -d '{
    "message": "Veuillez me faire une proposition"
}' -X POST https://api-preprod.creads-partners.com/v1/projects/559bf06dc73e8/messages
~~~

Lorsque le créatif postera un message livraison (`type` à `delivery`), il faudra répondre à ce message par une acceptation (mesage de type `accept`, qui finira le projet) ou un refus (type `reject`) pour continuer a discuter.
