<center/>REDUX 05
===
---

## Redux: Reducer Composition via Objets

Pour permettre une gestion plus claire de nos projets, nous aurons souvent besoin de plusieurs reducers, dans le cas de la todo, on a besoin par exemple d'un reducer qui va gerer la creation et modification des todos, mais on peux egalement avoir besoin d'un autre reducer qui va gerer la visibilité des todos.

pour appeler tout ces reducers, nous devrons les combiner, on peux pour cela utiliser une `const` qui va regrouper les differents todo de la manière suivante :

```javascript
const todoApp = (state = {}, action) => {
return {
	todos: todos(
		state.todos,
		action
		),
	visibilityFilter: visibilityFilter(
		state.visibilityFilter,
		action
		)
	};
};

const store = createStore(todoApp)```

on combine donc tout nos reducer dans un objet qui sera envoyé au store.

## Reducer Composition avec `combineReducers()`

la methode vu au chapitre précedent est banale au sein d'une application Redux, c'est pour cela que redux met a disposition la fonction `combineReducers()`

La fonction `combineReducers()` nous evite de taper tout ce code et cree le reducer geant combinant tout les petits reducers pour nous.

voici la syntaxe :

``` javascript
import { combineReducers } from 'Redux'

const todoApp = combineReducers({
todos,
visibilityFilter
})

// Syntaxe ES6
```

le peu de ligne de codes ci dessus permettent la creation du meme reducer combiné que celui du chapitre precedent, nous apprecierons le caractere menu du code.

## Redux: Implementer `combineReducers()` de zero

Pour bien comprendre le fonctionnement de `combineReducers` on va recoder la fonction de zero

```javascript
const combineReducers = (reducers) => {
	return (state = {}, action) => {
		return Object.keys(reducers).reduce(
			(nextState, key) => {
				nextState[key] = reducers[key](
					state[key],
					action
					);

					// ici on set le nextState au state suivant grace au reducer invoqué

					return nextState;
			}

			// on doit retourner un reducer, voila pourquoi le retour prend en parametre le
			// state et l'action.

			{}

			// on initialise un objet vide en tant que prochain nextState
			);
	};
};```



On remarque ici que l'on modifie la donnée envoyé, ce qui, comme nous avons pu le voir, n'est pas une bonne pratique, mais le fait est que c'est le reducer lui meme qui cree l'objet, et non pas un objet que nous lui avons passer en parametre
