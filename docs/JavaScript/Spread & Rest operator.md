# Spread & Rest Operator

- Spread Operator - Use this when you dont know how your arguments are packed
- Rest Operator - Use this when you dont know how many parameters are going to be passed.

```js
function sum(a, b) {
  return a + b;
}

args = [1, 2];
console.log(sum(...args)); //Spread Operator
function multiply(...args) { // Rest Operator
  let sum = 0;
  for (const eachElement of args) {
    sum += eachElement;
  }
  return sum;
}
console.log(multiply(1, 2, 3, 4));

function sumMultiply(a, b, ...args) {
  let result = a + b;
  for (const eachElement of args) {
    result *= eachElement;
  }
  return result;
}
console.log(sumMultiply(2, 3, 4, 5, 6, 7));
```
