---
title: Timezones
position: 7
---

Certaines requêtes renvoient des dates ou nécessitent d'en envoyer. **Toutes les dates renvoyées par l'API sont exprimées en temps universelle (UTC) au format ISO 8601**.

Par exemple :

`2015-08-04T15:24:21+0000`
{: .info}

Lorsque vous souhaitez soummetre une date générée sur un autre fuseau horaire qu'UTC, vous devez prendre soin de spécifier la timezone employée. L'exemple présent sur le fuseau Europe/Paris en heure d'été sera :

`2015-08-04T17:24:21+0200`
{: .info}
