# this

- For all regular function calls this points to window object.
- If its an object, then this points to that object.

```js
console.log(this); // points to window object
var user = {
  name: "Prabin Kumar",
  languages: ["C", "Java", "Python", "JavaScript"],
  get_user_info: function () {
    console.log("Information", this); // this points to user object
    function sayHello() {
      console.log("Hello", this); // this points to window object
    }
    sayHello();
  },
};
user.get_user_info();
function sayHello() {
  console.log("Hello", this); // this points to window object
}
sayHello();
```
