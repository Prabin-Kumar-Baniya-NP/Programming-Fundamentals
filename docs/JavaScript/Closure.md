# Closure

- Closure is the combination of function boundled together with its lexical environment.

```js
function a() {
  let x = 1;
  return function b() {
    return x;
  };
}

c = a();
console.log(c()); // 1
```
