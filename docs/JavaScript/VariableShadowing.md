# Variable Shadowing

```js
var a = 1;
let b = 2;
const c = 3;
{
  var a = 4;
  let b = 5;
  const c = 6;
  console.log(a); // 4
  console.log(b); // 5
  console.log(c); // 6
}
console.log(a);
// 4 because var a = 4 is shadowing var a = 1 and both a are same varibable pointing to same memory location
console.log(b); // 2
console.log(c); // 3
```

## illegal Shadowing

```js
var a = 1;
let b = 2;
{
    let a = 3; // right because we can decrease the scope of a
    var b = 4; // wrong because we cannot increase the scope of b
}
```