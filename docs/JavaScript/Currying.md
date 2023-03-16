# Currying

- Currying is a technique in functional programming
- It is a transformation of the function of multiple arguments into several functions of a single argument in sequence.
- Example: f(a,b,c) => f(a)(b)(c)

```js
function volume(length) {
  return function (breadth) {
    return function (height) {
      return length * breadth * height;
    };
  };
}
console.log(volume(2)(3)(4));
```
