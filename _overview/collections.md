---
title: Les collections de ressource
position: 8
---

Les collections de resource représentent un ensemble d'items d'une certaine ressource accompagné d'un compte. Il s'agit des réponses aux requêtes GET sur les listes de resources (ex: `GET /projects`) ou de collections imbriquées dans une autre ressources.

Une collection est une resource qui contient deux attributs:


|total_count| Ce compte contient le nombre d'élements total correspondant à la requête faites (sans prendre en compte la pagination)|
|items      | un tableau d'éléments (ressources) du même type|


#### Recherche dans une collection ####

Certaines ressources sont *searchable* ce qui signifie que vous pouvez filtrer le résultat d'une requête sur la collection de cette resource.

Par exemple, si vous voulez avoir tous les produits existants, vous pouvez faire

~~~ bash
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/products
~~~
{: title="Curl"}


Ce qui vous retournera une liste complète.

Si en revanche vous souhaitez obtenir seulement les produits d'une catégorie dont le gid est `$CATEGORY_GID`, vous pouvez filtrer cette requête via une query.


~~~ bash
curl -H "Authorization: Bearer $TOKEN" https://api.creads-partners.com/v1/products?query=["category.gid", "==", "$CATEGORY_GID"]
~~~
{: title="Curl"}


Le paramètre d'url **query** est un tableau JSON. Il s'agit d'un assemblage d'expressions et d'opérateurs logiques.

Une expression se compose de trois éléments: un champ, un opérateur, et une valeur.

~~~ json
[ "$FIELD", "$OPERATOR", "$VALUE"]
~~~
{: title="query"}

Les champs et opérateurs utilisables sont définies dans la documentation des resources.
{: .info}

#### Opérateurs conditionnels ####

* `==` : Egalité

Exemple: Produit dont le GID est 123456789

``` json
["gid", "==", "123456789"]
```

* `!=` : Inegalité

Exemple: Produit dont le GID n'est pas 123456789

``` json
["gid", "!=", "123456789"]
```

* `<` : Inférieur (strict)

Exemple: Projets crééés après le 21 Octobre 2015 (strictement)

``` json
["created_at", ">", "2015-08-21T01:00:00+0000"]
```

Note: la date doit être au format ISO 8601

* `>` : Supérieur (strict)
* `<=` : Inférieur ou égal
* `>=` : Supérieur ou égal
* `in` : Resources dont la valeur de *field* appartient au tableau *value*. La *value* pour cet opérateur doit-êtr eun tableau de valeurs scalaires.
* `!in` : Resources dont la valeur de *field* n'appartient pas au tableau *value*. La *value* pour cet opérateur doit-être un tableau de valeurs scalaires.
* `~=` : Opérateur **LIKE** qui permet de controler qu'un champ contient une expression. Le champ doit être **likable** pour effecteur ce genre de condition

Exemple: Produits dont le titre contient le mot 'projet'

``` json
["title", "~=", "projet"]
```

* `intersect` : Intersection. La *value* pour cet opérateur doit-être elle-même une expression, elle permet de ne filter que les résultats qui répondent au membre droite de cette condition

Exemple: Produits contenant l'organisation dont le gid est 123456879

``` json
["gid", "in", ["organizations.gid", "==", "123456789"]]
```

* `exclude` : Exclusion. Comme le précédent, permet d'obtenir une liste de resource n'étant pas comprise dans le résultat d'une autre condition.

Exemple: Produits ne contenant pas l'organisation dont le gid est 123456879

``` json
["gid", "!in", ["organizations.gid", "==", "123456789"]]
```

#### Opérateurs logiques ####

Vous pouvez également assembler plusieurs expressions dans la même `query` de manière logique. Par défaut, apposer les expressions en liste réalisera des **ET logiques** entre chacune:

Imaginons cette query sur `/products`

``` json
[["title", "~=", "projet"],["gid", "==", "123456789"],["category.gid", ">=", "12456789"]]
```

Cette requête signifie :

> Tous les produits dont le titre contient "projet" **et** dont le gid est 123456789 **et** donc la category a un gid supérieur à 123456789

Si vous souhaitez la version explicite de cette logique, il faut appliqer un `AND` a la liste d'expressions:

``` json
["AND", [ ["title", "~=", "projet"], ["gid", "==", "123456789"], ["category.gid", ">=", "12456789"] ]]
```

De la même manière, le **OU logique** est possible.:

``` json
["OR", [ ["title", "~=", "projet"],,["gid", "==", "123456789"], ["category.gid", ">=", "12456789"] ]]
```

En d'autres termes:

``` json
["$OPERATOR", [ $EXPRESSION_LIST ]]
```

Pour **prioriser** un opérateur logique, il faut *imbriquer* une query en tant qu'expression :

``` json
["AND", [["title", "~=", "projet"], ["OR", [["category.gid", ">=", "12456789"], ["gid", "==", "123456789"]]] ] ]
```

se traduit:

> Produits dont le titre contient "projet" **ET** ( gid égale 123456789 **OU** category a un gid supérieur à 123546789 )


#### Tri d'une collection ####


Vous pouvez ordonner et trier les réponses d'une requête en utilisant les paramètres de requête `orderBy` et `sort`.

* `orderBy` permet de trier selon le champ d'une ressource (à condition que ce champ soit *orderable*, c.f. References)
* `sort` vous permet de choisir l'ordre de tri ascendant (`asc`) ou descendant (`desc`). Par défaut, cette valeur est à `asc`

Pour obtenir les projets triés par date de modification (les plus récents en premier):

```
/projects?orderBy=modified_at&sort=desc
```

#### Pagination d'une collection

Il est possible d'utiliser la pagination (et la cumuler avec le tri et les `query`) pour n'afficher qu'une partie des résultats. Les paramètres de requêtes `offset` et `limit` vous permettent cette opération.

* `offset` définit l'index de l'élément à partir duquel afficher la collection de réponse
* `limit` définit le nombre d'éléments maximum à afficher

Par exemple, pour obtenir la deuxieme page de la liste de projet, à raison de 10 éléments par page:

```
/projects?offset=10&limit=10
```
