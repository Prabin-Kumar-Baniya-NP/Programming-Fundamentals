# Bind and Call

- The bind function creates a copy of a function with a new value to the this present inside the calling function.
- Call is a function that you use to change the value of this inside a function and execute it with the arguments provided.

```js
let car = {
  name: "Maruti Suzuki",
  price: 1234567,
  getInfo: function () {
    console.log(`${this.name} - ${this.price}`);
  },
};

let bike = {
  name: "Hero Honda",
  price: 2346243,
};

let bikeInfo = car.getInfo.bind(bike); // bind returns function reference
bikeInfo();

car.getInfo.call(bike);
```
