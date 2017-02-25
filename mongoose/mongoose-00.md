<center/>Mongoose Tutorial
================
---------------

### Pre-requis

> Avoir installé MongoDb et NodeJs

### installation

> npm install mongoose

#### Mise en place dans le projet

```javascript
import mongoose from 'mongoose'
mongoose.connect('mongodb://urldemabdd/maBdd')

```

nous avons donc une connexion en attente a la bdd, on veut savoir si la connexion c'est bien passé ou si il y a eu une erreur.

 ```javascript
const db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', () =>{
	// Yala ! on est connecté
})
 ```

Dans mongoose, tout est derivé de schema, un schema est un objet qui va definir la structure de nos elements

Prenons un exemple ou je souhaite referencé des chatons, il me faudra pour cela creer un schema

Par souci de brieveté on assume que tout le code ecrit ci dessous sera dans le call back de `db.once`


 ```javascript
const kittySchema = mongoose.Schema({
	name: String
})
 ```

le schema n'aura donc qu'une proprieté `name`, qui attend un `String`.

l'etape suivante et de transformer le `schema` en `model`

```javascript
	const Kitten = mongoose.model('Kitten', kittySchema);
```

un model est une classe avec laquelle on construit des `documents`, dans ce cas, chaque `document` sera un chatons avec les proprietés declaré dans notre `schema`.

exemple de creation d'un `document`

```javascript
const silence = new Kitten = ({name: 'Silence'});
console.log(silence.name); // 'Silence'
```

Nous pouvons egalement ajouté des fonctionnalité a nos `documents`

Nous allons donc creer une fonctionnalité qui va permettre a nos chatons de miauler

```javascript
	//Note : les methodes doivent être ajouter au schema avant de la compiler avec mongoose.model()

	kittySchema.methods.speak = () => {
		let greeting = this.name
		? 'Meow name is ' + this.name
		: 'i dont have a name';
		console.log(greeting);
	}

	const Kitten = mongoose.model('Kitten', kittySchema);
```

Nos chatons peuvent desormais miauler

```javascript
const fluffy = new Kitten({name: 'fluffy'})
fluffy.speak(); // "Meow name is fluffy"
```

pour sauvegarder un element dans `mongoDB` il faut utiliser la methode `.save()`

```javascript
fluffy.save((err, fluffy) => {
  if (err) return console.error(err);
  fluffy.speak();
});
```
Pour log l'integralité de nos chatons on passe par le model `Kitten` que l'on a créer

```javascript
Kitten.find((err, kittens) => {
  if (err) return console.error(err);
  console.log(kittens);
})
```

on peux egalement filtrer les chatons par nom, Mongoose supporte la syntaxe de recherche mongoDB


```javascript
Kitten.find({ name: /^fluff/ }, callback);
```

Cela permet de chercher tout les documents qui commencent par 'fluff', et renvoi une array contenant tout les chatons trouvé dans les callback
