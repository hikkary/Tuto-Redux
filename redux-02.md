<center/>REDUX 02
===
---
## Redux: la fonction Reducer

l'UI est plus predictible lorsque qu'elle est decrit comme fonction pure du `state` de l'application. cette notion a été introduite par des framework et librairies comme React.

Redux complete cette approche, avec l'idée complementaire, que les modifications effectué dans le `state` sois décrite via une fonction pure, qui prend le `state` precedent (*previous `state`*), l'`action` lancé (dispatché), et retourne le `state` suivant (*next `state`*) de l'application.

Dans chaque app codé avec redux, il y a une __fonction__ particulière, qui prend le `state` de l'application, et l'`action` lancé, et retourne le `state` suivant de l'application, il est important que cette fonction ne modifie pas le ``state`` qu'elle prend en charge, elle doit etre pure, elle doit donc retourner un nouvel objet.

Et cette __fonction__ particulière s'applique egalement dans les grosse applications, cependant, retourner entierement un nouvel objet (qui peut etre consequent) ne rend pas l'application lente, car Redux ne modifie que les référence qui change dans l'objet, c'est ce qui permet a redux d'être si rapide.

__Pour resumé__, pour operer des changements dans le `state`, vous devez écrire une fonction prend le `state` de l'application, l'`action` qui est dispatché,  et retourne le `state` suivant de l'application, cette __fonction__ ne modifie pas le `state` et doit donc être pure,

<center/> Cette `action` est appelé un Reducer
----
