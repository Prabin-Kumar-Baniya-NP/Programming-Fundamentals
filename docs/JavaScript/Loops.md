# Loops

```js
var programming_languages = new Array(
  "C",
  "C++",
  "Java",
  "Python",
  "JavaScript"
);

for (let i = 0; i < programming_languages.length; i++) {
  console.log(programming_languages[i]);
}
```

```js
let i = 0;
while (i < programming_languages.length) {
  console.log(programming_languages[i]);
  i++;
}
```

```js
for (;;) {
  if (i == 10) {
    console.log(i);
    break;
  }
  console.log(i);
  i++;
}
```

## For Each

```js
console.log("Using For Each in Array");
programming_languages.forEach((s) => console.log(s));
```

## For of - Use for arrays

```js
console.log("Using for of in Array");
for (const i of programming_languages) {
  console.log(i);
}
```

## For in - Use for objects

````js
console.log("Using for in")
const languages = {
    py: "Python",
    js: "JavaScript",
    cpp: "C++",
}
for(const i in languages){
    console.log(i); // Prints Keys of objects
    console.log(languages[i])  // Prints value for corresponding keys
}
````
