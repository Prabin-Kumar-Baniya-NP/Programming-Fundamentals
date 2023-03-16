# Destructuring Data in JavaScript

```js
var user = ["Prabin", 19, "admin"];
var [username, userAge, userRole] = user; // Destructuring Data in Array

console.log(`
    Userame is ${username}
    User Age is ${userAge}
    User role us ${userRole}
`);
```

Output:

```
Userame is Prabin
User Age is 19
User role us admin
```

```js
var Prabin = {
  myName: "Prabin",
  myAge: 19,
  myRole: "admin",
};

const { myName, myAge, myRole } = Prabin;
console.log(`
    Userame is ${myName}
    User Age is ${myAge}
    User role us ${myRole}
`);
```

Output:

```
Userame is Prabin
User Age is 19
User role us admin
```
