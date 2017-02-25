<center/>REDUX 04
===
---
## Redux: Evité la mutations d'objet avec `Object.assign()` et `...spread`

Pour retourner un objet sans le muté il faudrait classiquement recopié toute les clé et valeurs de l'objet, modifier la valeur voulu, puis retourner l'integralité.

Cependant sous ES6 la methode `Object.assign()` permet d'assigner une valeur a une clé ce sans mutations de l'objet

Sous ES7 le spread operator permet egalement de modifier une valeurs de l'objet très simplement

	Voir leurs utilisation sur les internets

## Ecrire un `reducer` pour Todo list (ajout de Todo)

>https://egghead.io/lessons/javascript-redux-writing-a-todo-list-reducer-adding-a-todo


	export default (state = [], action) => {
    switch (action.type) {
        case ADD:
            return [...state, action.payload];
        case REMOVE:
            return state.filter(task => task.id !== action.payload);
        case EDIT:
            return edit(state, action);
        default: return state;
    	}
	}

voir Tuto Todo De Raph pour plus d'info

## Redux: Reducer Composition via tableau

un reducer peux en appeler un autre qui gerera les cas egalement, dans le cas ou je dois map plusieurs todos, je peux utiliser un reducer comme fonction qui gerera les todos individuellement.

Ces dernieres sont stocké dans un tableau.

	https://egghead.io/lessons/javascript-redux-reducer-composition-with-arrays
