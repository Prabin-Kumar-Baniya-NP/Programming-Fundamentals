# Variables, Data Types, Operators

## Variables

```js
var first_name = "Prabin"; // String
var middle_name = "Kumar"; // String
var age = 19; // Number
const gender = "Male";
var lives_in_nepal = true; // Boolean
console.log("Is " + first_name + " " + middle_name + " lives in" + " Nepal ?");
console.log(lives_in_nepal);
console.log(`
    Data Type of first name is ${typeof first_name}
    Data Type of middle name is ${typeof middle_name}
    Data type of age is ${typeof age}
    Data type of gender is ${typeof gender}
    Data type of lives in Nepal is ${typeof lives_in_nepal} 
`);
```

```js
var random; // undefined
var i_am_not_num = first_name / 2; // NaN
console.log(random); // undefined
console.log("Data type of random variable is " + typeof random);
console.log(i_am_not_num);
console.log("Data type of i_am_not_num variable is " + typeof i_am_not_num);
```

## Arithmetic Operators

```js
var operation1 = 6 + 2 - 5; // Addition, Substraction
var operation2 = 2 * 5; // Multiplication
var operation3 = 2 / 5; // Division
var operation4 = 2 ** 5; // Exponential
console.log(`
    ${operation1}
    ${operation2}
    ${operation3}
    ${operation4}
`);
```

## Bitwise Operators

```js
var operation5 = 10 & 2; // Bitwise And
var operation6 = 10 | 2; // Bitwise OR
var operation7 = ~operation6; // Bitwise NOT
var operation8 = 10 ^ 2; // Bitwise XOR
var operation9 = 10 << 2; // Bitwise Left Shift
var operation10 = 10 >> 2; // Bitwise Right Shift
```

## Logical Operators

```js
var operation11 = true || true; // Logical OR
var operation12 = true && false; // Logical AND
var operation13 = !operation12; // Logical NOT
```

## Relational Operators

```js
var operation14 = 10 < 5; // Less than
var operation15 = 10 > 9; // Greater than
var operation16 = 10 <= 5; // Less or Equal to
var operation17 = 11 >= 11; // Greater than or Equal to
```

## Conditional (Ternary) Operator

```js
var operation18 = 10 > 5 ? true : false;
var operation19 = age > 18 ? "Can Vote" : "Can't Vote";
console.log(operation19);
```
