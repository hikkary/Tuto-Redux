<center/>REDUX 03
===
---
## Redux: Mettre en place le store a partir de zéro

Pour bien comprendre le fonctionnement du store, nous allons l'implementer nous même.

```javascript
const createStore = (reducer) => {
	let state;

	// variable qui va stocker notre state

	let listener = [];

	// tableau permettant de stocker les listeners

	const getState = () => state;

	const dispatch = (action) =>{
		state = reducer(state, action)

		// on met a jour le state grace au reducer au state actuel et l'action envoyé

		listeners.forEach(listener => listener());

		// on notifie le changement aux listeners
	};

	const subscribe = (listener) => {
		listeners.push(listener);

		return() => {
			listeners = listeners.filter(l => l !== listener)
		}

		// permet d'enlever les listener quand on en a plus l'utilité
	};

	dispatch({});

	// by the time is return, we want it to have the initial state populated,
	// we are going to dispatch a dummy action
	// just to get the reducer to return the initial value

	return {getState, dispatch, suscribe};
}
```
Voir pour des explications plus precise de listeners.

## Redux: Exemple de compteur sous React

Sous react on ne peux plus utiliser la methode render utilisé precedemment :

```javascript
const render = () => {
	document.body.innerText = store.getState();
}```

il faut utilisé l'outil `ReactDOM.render` inclus

```javascript
const Counter = ({
	value,
	onIncrement,
	onDecrement
	}) => (
			<div>
			<h1>{value}</h1>
			<button onClick={onIncrement}>+</button>
			<button onClick={onDecrement}>-</button>
			</div>
		);

// on cree un composant Counter qui va prendre en parametre 	
// les actions `INCREMENT` et `DECREMENT` ainsi que le state actuel

const render = () => {
	ReactDOM.render(
		<Counter
			value={store.getState()}
			onIncrement={() =>
				store.dispatch({
					type: 'INCREMENT'
					})
			onDecrement={() =>
				store.dispatch({
					type: 'DECREMENT'
					})
			}
			/>,
			document.getElementById('root')
		)
}

// On utilise ici le composant créer plus haut, on lui passe en parametre l'etat actuel du state, ainsi que les deux actions
// que nous lions plus haut au button '+' et '-'

store.subscribe(render);

// Met a jour le Render dès le dispatch d'une action

render();

// render initial```

## Redux: Evité les mutations de tableau avec `concat()`,`slice()` et `...spread`

Pour ne pas effectuer de mutations dans le code, il faut eviter les methode `push()` et `splice()`,

et privilegier les methodes tel que `concat()` et `slice()`

Si on utilise l'ES6 on peux utiliser le spread operator pour retourner une nouvelle reference de l'objet.

`deepFreeze` permet de voir que la variable n'a pas été muté, couplé a expect cela permet d'effectuer des test
