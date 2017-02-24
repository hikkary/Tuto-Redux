<center/>REDUX 01
===
---
## Redux: l'unique arbre immutable

Premier principe de Redux :

Que ce sois pour une application simple ou complexe, vous allez representer tout le state de votre application dans un objet javascript.

Toute les mutations du state dans redux sont explicite, il est donc possible de voir facilement ces changements.

la complexité du state est fonction de l'application, avec une todo list par exemple, notre objet javascript pourra contenir multitude d'objet ou d'array, permettant une manipulation totale de la donnée utilisateurs.

## Redux : changements de states via les Actions

Second principe de redux :

l'arbre des states est immutable, chaque changements se fait via les actions (on dit dispatch une action), une action est un objet javascript decrivant le changement.

Tout comme le state est le representation minimal des data de votre App, l'action est la representation minimal des changement operé sur les donneés.

la structure de l'objet contenant l'action vous incombe, la seul chose requise est que l'objet ai une clé type

 	{
		type:"INCREMENT"
	 }

cette clé ne peut être non defini.

Petit exemple, dans le cas d'un compteur, les seules actions nescessaires seront de type "INCREMENT" et "DECREMENT", a part le type, on ne passera aucune autre donnée car ce n'est pas nescessaires pour manipuler la donnée.

Dans le cas d'application plus complexe, on pourra ajouter des clé permettant la manipulation de la donnée.

Pour resumé toute manipulation de donnée se fait via des actions plus ou moins complexe.

## Redux : Fonction Pure et impure

Difference entre Fonction pure et inpmure :

Les fonctions pure retourne des valeurs uniquements basés sur les valeurs passer en paramètres, si j'envoie les mêmes arguments a une fonction pure, je suis sur que le resultat sera le même.

Et les fonctions pure ne modifie pas les valeurs qu'elle prend en paramètre.

### <center/> __Le Resultat est prévisible ET ne modifie pas les valeurs envoyé__

Les fonctions impure quand a elle peuvent faire appel a une tierce partie(base de donnée ou autre), avoir un effet non voulu sur le DOM, elle peut egalement ecraser la donnée envoyé en paramètre.


La distinction doit etre clair car certaines des fonctions que vous ecrirez pour redux doivent être pure
