---
title: Comment
position: 8
---

Il est possible de commenter des resources. Par exemple, pour échanger avec le créatif sur un `Work`, il suffit de poster un commentaire portant le `uri` du commentaire.

~~~ bash
curl -i -H "Authorization: Bearer $TOKEN" -d '{
  "message": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras scelerisque viverra sodales. Vestibulum quis fringilla nisi. Donec congue neque ac consequat vestibulum. Praesent sed urna maximus ante ornare vestibulum. In in vulputate sapien. Ut elementum bibendum mi sit amet congue. Aliquam suscipit turpis vitae dapibus efficitur. Nullam quis lacinia ligula. Nam at lectus sem.",
  "uri": "/works/559bef4a9b600"
}' -X POST https://api-preprod.creads-partners.com/v1/comments
~~~

Et pour récuperer les autres commentaires de la même ressource


~~~ sh
curl -H "Authorization: Bearer $TOKEN" 'https://api.creads-partners.com/v1/comments?query=\["uri","==","/works/559bef4a9b600"\]'
~~~


