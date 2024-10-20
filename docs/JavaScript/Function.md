# Functions

## Function Statement OR Function Declaration

```js
function add(a, b) {
  return parseInt(a) + b;
}
console.log(add(1, 2)); // 3
console.log(add(1, "2")); // 12
```

## Function Expression

When we create a function and assign it to a variable

```js
var minus = function (a, b) {
  return parseInt(a) - parseInt(b);
};
console.log(minus(3, 2));
```

<b>Difference between Function Statement and function expression is hoisting.</b>

## Named Function Expression

```js
var multiply = function mult(a, b) {
  return parseInt(a) * parseInt(b);
};

multiply(2, 3); // 6
// mult(2,3) --> Gives error => mult is not defined
```

### Difference between parameters and arguments

- Parameter - a, b in previous function
- Arguments - 2, 3 in previous function

## Anonymous Functions - Functions without name

```js
let displayMessage = function () {
  console.log("Hi I am a anonymous function");
};
displayMessage();
```

## Anonymous function as an argument

```js
setTimeout(function () {
  console.log("I am being displayed after 2 seconds");
}, 2000);
```

### First Class Function / First Class Citizens

- The ability to use function as a value and pass that function to another function as an arguments as well as return function from the function is called first class function

```js
function calc(fn) {
  return function () {
    console.log("Adding");
  }; // function is returned
}
var calculation1 = calc(add); // function is passed as an arguments and
```

## Arrow Function

```js
var divide = (a, b) => {
  return a / b;
}; // Arrow Function
console.log(divide(4, 2));

console.log(count_many(1, 9, 5, 7)); // You passed 4 parameters and the parameters are 1,9,5,7
function count_many(...para) {
  // Rest Parameters
  return `You passed ${arguments.length} parameters and the parameters are ${para}`;
}

console.log(count_many_again); // undefined
var count_many_again = function () {
  return `Expecting undefined`;
};
```

## Self Executing Anonymous Function - OR - IIFE (Immediately Invoked Function Expression)

```js
(function () {
  console.log("Hi, We are still learning JavaScript");
})();
```

## Callback Functions

- Callbacks are functions passed into another functions as an argument

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
function isEven(item) {
  if (item % 2 == 0) return item;
}
arr_even = arr.filter(isEven);
console.log(arr_even);
```

### Pure and Impure Functions

```js
// Pure function
function add(x, y) {
  return x + y;
}

// Impure function
let counter = 0;
function incrementCounter() {
  counter++;
  return counter;
}

```