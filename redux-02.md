<center/>REDUX 02
===
---
## Redux: la fonction Reducer

l'UI est plus predictible lorsque qu'elle est decrit comme fonction pure du `state` de l'application. cette notion a été introduite par des framework et librairies comme React.

Redux complete cette approche, avec l'idée complementaire, que les modifications effectué dans le `state` sois décrite via une fonction pure, qui prend le `state` precedent (*previous `state`*), l'`action` lancé (dispatché), et retourne le `state` suivant (*next `state`*) de l'application.

Dans chaque app codé avec redux, il y a une __fonction__ particulière, qui prend le `state` de l'application, et l'`action` lancé, et retourne le `state` suivant de l'application, il est important que cette fonction ne modifie pas le ``state`` qu'elle prend en charge, elle doit etre pure, elle doit donc retourner un nouvel objet.

Et cette __fonction__ particulière s'applique egalement dans les grosse applications, cependant, retourner entierement un nouvel objet (qui peut etre consequent) ne rend pas l'application lente, car Redux ne modifie que les référence qui change dans l'objet, c'est ce qui permet a redux d'être si rapide.

__Pour resumé__, pour operer des changements dans le `state`, vous devez écrire une fonction prend le `state` de l'application, l'`action` qui est dispatché,  et retourne le `state` suivant de l'application, cette __fonction__ ne modifie pas le `state` et doit donc être pure,

<center/> Cette fonction est appelé un Reducer
----

## Redux : écrire un compteur reducer avec test

Voici un exemple avec un reducer pour l'exemple du compteur,

un reducer prend en paramètre un `state` et une `action`, et retourne le `state` suivant.

	counter = (state = 0, action) => {
	   switch (action.type) {
		   case INCREMENT:
			   return state + 1;
		   case REMOVED:
			   return state - 1;
		   default: return state;
	   }
	}

	expect (
		counter (0, { type: 'INCREMENT'})
	).toEqual(1)

	// test incrementation

	expect (
		counter (1, { type: 'INCREMENT'})
	).toEqual(2)

	expect (
		counter (2, { type: 'DECREMENT'})
	).toEqual(1)

	expect (
		counter (1, { type: 'DECREMENT'})
	).toEqual(0)

	// test décrementation

	expect (
		counter (1, { type: 'SOMETHING_ELSE'})
	).toEqual(1)

	// Fausse action doit retourner le state actuel

	expect (
		counter (undefined, {})
	).toEqual(0)

	// pas de state doit retourner le state initial

	console.log('test passed')

expect est une librairie qui permet de faire des test, elle prend
un parametre une fonction et permet de verifier que le retour est conforme a ce que l'on attend.

quelques règle de base concernant les reducers:

- Si le state n'est pas defini, le reducer doit renvoyé l'etat initial du `state`, qui sera dans notre fonction mise a zero `state = 0`.

- Si l'action n'est pas defini, le reducer renvoi le `state` actuel.

## Redux : Methode du Store: getState(), dispatch() et suscribe()

	import { createStore} from 'Redux'

	counter = (state = 0, action) => {
	   switch (action.type) {
		   case INCREMENT:
			   return state + 1;
		   case REMOVED:
			   return state - 1;
		   default: return state;
	   }
	}

	const store = createStore(counter)

Le store lie les trois principe de Redux :

- Il contient le `state` de l'application

- nous permet de `dispatch` des actions


lorsque l'on crée le Store, on lui notifie le reducer qui va modifier notre state selon les actions.

ici `createStore(counter)`

Le store comporte 3 Methodes importante :

- getState()

		store.getState() recupère le state actuel du store

- dispatch()

		store.dispatch({type: 'INCREMENT'}) va retourner le state + 1

- subscribe()

		store.subscribe(() => {
			document.body.innerText = store.getState();
		}); permet d'appeler un callBack apres chaque action

	ici on va afficher le compteur apres chaque appel de l'action,
	cependant on verra que le compteur ne s'initialisera pas a zero,
	voici une syntaxe propre qui permettra un affichage correct du compteur.

		const render = () => {
			document.body.innerText = store.getState();
		}

		store.subscribe(render);
		render(); // render initial qui permet d'afficher le compteur a zero
		(car aucune action n'a été faite)
