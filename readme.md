# ES6 La base

## Comment exécuter du code ES6 ?

Toutes les features ES6 (ou ES2015) ne sont pas encore bien supportée à ce jour.
Il faut donc utiliser un compiler, comme Babel.

```
git clone // TODO: ajouter le repo
cd // repo
npm install babel-cli -g
npm install
babel-node index.js
```

## const & let

Es6 apporte une nouvelle manière de déclarer ses variables :

```js
const myConstant = 'CONSTANT';
let myVariable = 'variable';
```

à la différence de  `var` ces variables sont block-scopées et non function-scopées.

les constantes, définies par `const` ne peuvent pas être ré-assignées.
Privilégier l'utilisation de const. Réassigner des variables amène souvent
des bug dans le code.

## String templating
On peut maintenant interpoller des variables à l'intérieur d'une string en la définissant avec des back-ticks.

```js
const person = 'Moray';
const salutation = `Wesh ${person}`; // Wesh Moray
```

## arrow-function

Une nouvelle manière de définir ses functions.

```js
collection.forEach(function(item) {
  return item + 1;
});
```

peut maintenant s'écrire

```js
collection.map((item) => item + 1);
```
Si notre function de callback n'est pas définie par un block
(comme au dessus), la valeur est automatiquement retournée. Si on défini un
block, on peut exécuter plusieurs instructions et on doit utiliser le
token `return`, comme avant. par exemple :

```js
collection.map((item, i) => {
  item.id = i;
  return item;
})
```

#### Les petites différences entre les deux
Une arrow function n'est pas liée à un contexte, comme une function standard. Elle n'a donc pas d'objet `this`. C'est cool, parce que c'était quand même assez emmerdant qu'un contexte soit créé pour un callback par exemple. On a donc plus besoin de le gérer manuellement.
```js
(function() {
  this.coucou = 'blablabla';

  // plus besoin de ça :
  doSomething(function() { console.log(this.coucou) /* 'blablabla'  */ }.bind(this));

  // ou de ça :
  var self = this;
  doSomething(function() { console.log(self.coucou) /* 'blablabla' */ });

  // on peut faire ça
  doSomething(() => console.log(this.coucou));

})();
```

## Default values
On peut maintenant définir des valeurs par défault dans les paramètres d'une function.

```js
function renderList(items = []) {
  items.forEach((item) => renderItem(item));
}
renderList(); // pas de throw, la valeur par défault est utilisée.
```

## Object shortcut

Es6, ça facilite la vie. maintenant à la place d'écrire ça :
```js
var firstname = 'Gabriel';
var lastname = 'Vergnaud';
var user = {firstname: firstname, lastname: lastname};
```
on peut tout simplement écrire ça :
```js
const user = { firstname, lastname };
```
C'est chouette.

## Destructuring
Le destructuring, c'est le fait de pouvoir sortir des variables d'une
data-structure pour les rendre disponible dans notre scope.
Exemple :
```js
const person = {
  firstname: 'Moustache',
  lastname: 'Devbaques'
};

const { firstname, lastname } = person;
console.log(firstname); // 'Moustache'
console.log(lastname); // 'Devbaques'
```
#### Pourquoi c'est de la balle ?
On peut les utiliser le destructuring pour récupérer les paramètres d'une function :

```js
let fullname = ({firstname, lastname}) => `${firstname} ${lastname}`

fullname(person); // 'Moustache Devbaques'
```
C'est chouette parce que ça rend le passage de paramètre expressif, tout en permettant de ne pas se prendre la tête avec l'ordre des paramètre, puisqu'on les stock sous forme d'object.

Notez à quel points ça se mari bien avec l'Object Shortcut :
```js
let myFunction({param1, param2, param3}) => { // destructuring
  // do something
};

const
  param1 = 'COUCOU',
  param2 = 'Hey',
  param3 = 'Wasup';

myFunction({param1, param2, param3}); // object shortcut
```

```js
let myFunction() => {
  return {param1, param2, param3}; // object Shortcut
};

const { param1, param2, param3 } = myFunction(); // destructuring
```

## Spread Syntax

La spread syntax permet de "verser" les valeurs d'un array ou d'un object dans
un autre. Par exemple :

```js
const arr1 = [1, 2, 3];
const arr2 = [3, 4, 5];
const spreadArr = [...arr1, ...arr2];
console.log(spreadArr); // [1, 2, 3, 3, 4, 5];
```

```js
const obj1 = {one: 1, two: 2, three: 3};
const obj2 = {three: 'three', four: 4, five: 5};
const spreadObj = {...obj1, ...obj2};
console.log(spreadObj); // {one: 1, two: 2, three: 'three', four: 4, five: 5};
```
#### c'est pas tout
on peut aussi récupérer les arguments d'une function grâce à la spread syntax :

```js
let myFunc = (...args) => {
  console.log(args); // [ 'lol', ':)' ]
  args.forEach(arg => console.log(arg))
}

myFunc('lol', ':)');
```

On peut récupérer le reste des arguments comme ceci :

```js
let myFunc = (arg1, ...rest) => {
  console.log(rest); // [ ':)', '😜' ]
}

myFunc('lol', ':)', '😜');
```

Ou bien injecter un tableau d'arguments dans une function :

```js
let myFunc = (arg1, arg2, arg3) => {
  // ...
}

const argsArray = ['lol', ':)', '😜'];
myFunc(...argsArray);

//  on peut aussi insérer des arguments entres d'autres
myFunc('lol', ...[':)', '😜'], 'blablebli'); // === myFunc('lol', ':)', '😜', 'blablebli')
```

## import & export

## Les class


## Ressources :

- [Tout es6 sous forme de bullet points](https://ponyfoo.com/articles/es6)
- [Le guide du savoir universel de l'ES6](https://ponyfoo.com/articles/tagged/es6-in-depth)
- [Comparaisons ES5 vs ES6](http://es6-features.org/)
- [S'entrainer avec des tests](http://es6katas.org/)
