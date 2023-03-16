# Block Scoping

- let and const are block scoped
```js
{
    var a = 1;
    let b = 2;
    const c = 3;
    console.log(a); // 1
    console.log(b); // 2
    console.log(c); // 3
}
console.log(a); // 1
console.log(b); // reference error
console.log(c); // reference error 
```