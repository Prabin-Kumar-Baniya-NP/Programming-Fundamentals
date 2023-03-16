# Conditionals

## If statement

```js
var age = 19;
var gender = null;
if (age >= 18) {
  console.log("You can Vote");
} else {
  console.log("You can't Vote");
}

if (gender == "Male") {
  console.log("Go Left");
} else if (gender == "Female") {
  console.log("Go Right");
} else {
  console.log("Go Straight");
}
```

## Switch Statement

```js
var role = "Staff";
switch (role) {
  case "Student":
    console.log("You can directly go to classroom");
    break;
  case "Teacher":
    console.log("You can go to meeting room");
    break;
  case "Principle":
    console.log("You can go to your office");
    break;
  default:
    console.log("You are not allowed to enter here");
    break;
}
```
