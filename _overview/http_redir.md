---
title: Redirections HTTP
position: 4
---

L'API peut utiliser des redirections HTTP. Le client doit faire en sorte que ces redirections soient prises en charge. Les redirections portent une entête `Location` qui contient l'URL de la resource vers laquelle le client doit renvoyer la requête.

| Code | Description                      |
|------|----------------------------------|
| 301  | Redirection permanente           |
| 302  | Redirection temporaire           |
