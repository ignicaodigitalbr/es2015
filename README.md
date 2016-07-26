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
```

### This
```javascript
// ES5
function Count() {
  this.time = 0;

  setInterval(function () {
    this.sum(); // Uncaught TypeError: this.sum is not a function
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
    this.sum();
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