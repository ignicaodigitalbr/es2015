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