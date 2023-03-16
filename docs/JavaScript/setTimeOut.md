# SetTimeOut

- To print i after i seconds

```js
function x() {
  for (var i = 1; i <= 5; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }
  console.log("Understanding Closures in JavaScript");
}
```

In every iteration i is being referred to same memory location

```
Output
Understanding Closures in JavaScript
6
6
6
6
6
```

- let and const are block scoped. so for each value of j, j will be stored in separate space.

```js
function y() {
  for (let j = 1; j <= 5; j++) {
    setTimeout(function () {
      console.log(j);
    }, j * 1000);
  }
  console.log("Understanding Closures in JavaScript");
}
```

Output

```
Understanding Closures in JavaScript
1 (After 1 sec)
2 (After 2 sec)
3 (After 3 sec)
4 (After 4 sec)
5 (After 5 sec)
```

- Using the concept of closure

```js
function z() {
  for (var k = 1; k <= 5; k++) {
    function closurefun(k) {
      setTimeout(function () {
        console.log(k);
      }, k * 1000);
    }
    closurefun(k);
  }
  console.log("Understanding Closures in JavaScript");
}
```

Output

```
Understanding Closures in JavaScript
1 (After 1 sec)
2 (After 2 sec)
3 (After 3 sec)
4 (After 4 sec)
5 (After 5 sec)
```
