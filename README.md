# Code Snippets to ES2015 Presentation

## Arrow Functions

### Return
```javascript
const sum = x => x + 1;
const awesomeSum = (x, y) => x + y;
const complex = (x, y) => x > y ? x : y;

const complexOperation = (x, y) => {
  if (x > y) {
    return x * y;
  }

  return x + y;
}

// ES5
var avengers = [
  { name: 'Iron Man', damage: 500 },
  { name: 'Thor', damage: 300 },
  { name: 'Hulk', damage: 400 },
  { name: 'Captain America', damage: 250 },
  { name: 'Black Widow', damage: 350 },
  { name: 'Hawkeye', damage: 320 }
];

var powerfulFilter = function(avenger) {
  return avenger.damage > 300;
};
var damageCollection = function(avenger) {
  return avenger.damage;
};
var calcDamage = function(sum, damage) {
  sum + damage;
};

var totalDamage = avengers
  .filter(powerfulFilter)
  .map(damageCollection)
  .reduce(calcDamage);

console.log(totalDamage);

// ES2015
const avengers = [
  { name: 'Iron Man', damage: 500 },
  { name: 'Thor', damage: 300 },
  { name: 'Hulk', damage: 400 },
  { name: 'Captain America', damage: 250 },
  { name: 'Black Widow', damage: 350 },
  { name: 'Hawkeye', damage: 320 }
];

const powerfulFilter = avenger => avenger.damage > 300;
const damageCollection = avenger => avenger.damage;
const calcDamage = (sum, damage) => sum + damage;

const totalDamage = avengers
  .filter(powerfulFilter)
  .map(damageCollection)
  .reduce(calcDamage);

console.log(totalDamage);
```

### This
```javascript
// ES5
function Count() {
  this.time = 0;

  setInterval(function () {
    this.sum(); // Uncaught TypeError: this.sum is not a function
    console.log(this.time);
  }, 1000);
}

Count.prototype.sum = function () {
  this.time++;
};

var c = new Count();

//ES2015
function Count() {
  this.time = 0;

  setInterval(() => {
    this.sum(); // No error :)
    console.log(this.time);
  }, 1000);
}

Count.prototype.sum = function () {
  this.time++;
};

var c = new Count();
```

### Constructor
```javascript
var Hero = (name) => `Hero: ${name}`;

new Hero('Iron Man'); // Uncaught TypeError: Hero is not a constructor
```

### Anonymus
```javascript
var Hello = World(foo) => foo; // Uncaught SyntaxError: Unexpected token (
```

## Classes

```javascript
// ES5
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log('Hi. I\'m ' + this.name);
};

Person.sayBye = function () {
  console.log('Bye');
};

var p = new Person('Vitor');

p.sayHello();
Person.sayBye();

// ES2015
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log('Hi. I\'m ' + this.name);
  }

  static sayBye() {
    console.log('Bye');
  }
}

const p = new Person('Vitor');

p.sayHello();
Person.sayBye();

console.log(typeof Person) // function;
console.log(typeof Person.prototype.sayHello) // function;
```

### Extends
```javascript
// ES5
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log('Hello! I\'m ' + this.name);
};

function Hero(name, alias) {
  Person.call(this, name);

  this.alias = alias;
}

Hero.prototype = new Person(null);

Hero.prototype.whoIs = function () {
  console.log(this.name + ' is ' + this.alias);
};

var tony = new Hero('Tony Stark', 'Iron Man');
tony.whoIs(); // Tony Stark is Iron Man

// ES2015
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log(`Hello! I'm ${name}`);
  }
}

class Hero extends Person {
  constructor(name, alias) {
    super(name);

    this.alias = alias;
  }

  whoIs() {
    console.log(`${this.name} is ${this.alias}`);
  }
}

const tony = new Hero('Tony Stark', 'Iron Man');
tony.whoIs(); // Tony Stark is Iron Man
```

## Template Strings

```javascript
console.log(`Hello IGD!!`); // Hello IGD!!
console.log(`Hello
IGD!!`);
// Hello
// IGD!!

// ES5
var product = 'Klickpages';
console.log(product + ' is awesome!'); // Klickpages is awesome!

// ES2015
const product = 'Klickpages';
console.log(`${product} is awesome!`); // Klickpages is awesome!
```

## let and const

### let
```javascript
// ES5
console.log(foo); // undefined
if (true) {
  var foo = true;
  console.log(foo); // true
}
console.log(foo); // true

// ES2015
console.log(foo); // Uncaught ReferenceError: foo is not defined
if (true) {
  let foo = true;
  console.log(foo);
}

if (true) {
  let bar = true;
  console.log(bar); // true
}
console.log(bar); // Uncaught ReferenceError: foo is not defined
```

### const
```javascript
const FOO = true;
console.log(FOO); // true

FOO = false // Uncaught TypeError: Assignment to constant variable.

const FOO = true; // Uncaught SyntaxError: Identifier 'FOO' has already been declared

const BAR; // Uncaught SyntaxError: Missing initializer in const declaration
```

## Modules

```javascript
// math.js
const math = {
  sum: x => x + 1,
  awesomeSum: (x, y) => x + y
};

export default math;

// main.js
import math from 'math';

console.log(math.sum(3)) // 4
console.log(math.awesomeSum(3, 3)) // 5
```

## Promises
```javascript
const timer = (name) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`${name} is awesome!`);
    }, 1000);
  });
};

timer('Klickpages')
  .then(data => console.log(data), error => console.error(error));
```