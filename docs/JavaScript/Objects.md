# Objects

## Defining Objects Using Object Literals

```js
let circle = {
  radius: 4,
  location: {
    x: 1,
    y: 2,
  },
  draw: function () {
    console.log("Drawing Circle Using JavaScript");
  },
};
circle.draw();
```

## Creating Objects Using Factory Function

```js
function createCircle(radius) {
  return {
    radius,
    draw: function () {
      console.log("Drawing Circle Using JavaScript");
    },
  };
}

const circle1 = createCircle(5);
circle1.draw();
```

## Creating Objects Using Constructor Function

```js
function Rectangle(length, breadth) {
  this.length = length;
  this.breadth = breadth;
  this.area = function () {
    console.log(this.length * this.breadth);
  };
}
const rect1 = new Rectangle(2, 3);
rect1.area();

// Creating objects using Object Constructor
let cycle = new Object();
cycle.Model = "XYZ";
cycle["Price"] = 453264;
cycle.getInfo = function () {
  return `Model is ${this.Model} and Price is ${this.Price}`;
};

console.log(cycle.getInfo());

var Car = function (name, color, price) {
  this.name = name;
  this.color = color;
  this.price = price;
  this.check_price = function () {
    if (this.price >= 2000000) {
      return "Expensive Car";
    } else {
      return "Cheap Car";
    }
  };
};

var maruti = new Car("suzuki", "white", "1500000");
var ferrari = new Car("F120", "red", "9900000");
console.log(maruti.name);
console.log(ferrari.check_price());
```

## Object Operations

```js
// Enumerating Properties of the Objects

for (let key in circle) {
  if (typeof circle[key] != "function") console.log(key, circle[key]);
}

// To get the keys of objects
const keys = Object.keys(circle);

// To check property or methods of an object
if ("radius" in circle) console.log("yes");
```

## Classes

```js
class Grandfather {
  constructor() {
    this.money = 1000;
  }
  showbalance() {
    console.log(this.money);
  }
}

class Father extends Grandfather {
  constructor() {
    super();
    this.money = this.money + 500;
  }
}
class Daughter extends Father {
  constructor() {
    super();
    this.money = this.money + 200;
  }
}

class Son extends Father {
  constructor() {
    super();
    this.money = this.money + 100;
  }
}

let GF = new Grandfather();
let F = new Father();
let D = new Daughter();
let S = new Son();
GF.showbalance();
F.showbalance();
D.showbalance();
S.showbalance();
```

## Prototype in JavaScript

```js
var House = function (floor, room) {
  // Instance Member
  this.floor = floor;
  this.room = room;
  this.check_house = function () {
    if (this.floor >= 3) {
      return "House is Big";
    } else {
      return "House is Small";
    }
  };
};

var Ram_house = new House(2, 6);
var Shyam_house = new House(3, 10);

// Prototype Member
House.prototype.min_price = 1000000;

console.log(Ram_house);
console.log(Shyam_house.room);
console.log(Shyam_house.check_house());
console.log(Ram_house.min_price); // Accessing Prototype Member

// Iterating over Instance Members and Prototype Members

console.log(Object.keys(Ram_house)); // Returns only instance members

for (var keys in Ram_house) {
  console.log(keys); // Returns Instance and Prototype members
}
```

## Understanding Prototype Object

```js
var obj = {};
```

- In above statement, Object is Constructor.
- Object will inherit all the properties of Object.prototype and Object.protype is the prototype object of object obj.
- Whereas prototype object of Object.prototype is null.
- obj => Object.Prototype =>NULL

### Verifying the concept through code

```js
console.log(Object.prototype); // Returns the properties and methods of Object.prototype.
console.log(Object.getPrototypeOf(obj)); // Returns the properties and methods of Object.prototype.
console.log(Object.getPrototypeOf(Object.prototype)); // Returns null
```

```js
var arr = [];
```

- In above statement, Array is constructor.
- Array will inherit all the properties of Array.prototype So, Array.prototype is prototype object of object arr.
- Array.prototype is also inheriting the properties of Object.prototype. So, Object.prototype is the prototype object of object Array.prototype.
- Whereas prototype object of Object.prototype is null.
- arr => Array.prototype => Object.Prototype => NULL

## Verifying the concept through code

```js
console.log(Array.prototype); // Returns the properties of Array.protoype
console.log(Object.getPrototypeOf(arr)); // Returns the properties of Array. Prototype
console.log(Object.getPrototypeOf(Array.prototype)); // Returns the properties of Object.prototype
console.log(Object.getPrototypeOf(Object.prototype)); // Returns null
```

```js
var str = new String();
```

- In above statement, String is constructor.
- String will inherit all the properties of String.prototype So, String.prototype is prototype object of object str.
- Whereas Object,prototype is the prototype object of String.prototype and prototypr object of Object.protype is null.
- str => String.prototype => Object.Prototype => NULL

### Verifying the concepts through code

```js
console.log(String.prototype); // Returns the properties of String.protoype
console.log(Object.getPrototypeOf(str)); // Returns the properties of String. Prototype
console.log(Object.getPrototypeOf(String.prototype)); // Returns the properties of Object.prototype
console.log(Object.getPrototypeOf(Object.prototype)); // Returns null
```

## Use of **proto**

```js
console.log(obj.__proto__ == Object.prototype); // Returns true
console.log(arr.__proto__ == Array.prototype); // Returns true
console.log(str.__proto__ == String.prototype); // Returns true

House.prototype.max_price = 10000000;
House.__proto__.avg_price = 5000000;
```

- Conclusion of **proto** is when we create any object, **proto** property is created which points to its Prototype Object.

## Understanding How JavaScript Engine Searches for a variable

```js
var Smartphone = function (ram, price) {
  this.ram = ram;
  this.price = price;
};
var Realme = new Smartphone(8, 12000);
Realme.__proto__.price = 24000;
console.log(Realme.price); // Returns 12000 (not 24000)  but if not found price in Realme object it will return 24000
```

## Constructor Inheritance and Prototype Inheritance

```js
// Creating two Constructor
var First = function () {
  this.a = 10;
};

var Second = function () {
  First.call(this); // It will inherit all the instance properties of First class
  this.b = 20;
};

// Adding a Prototype member in First Class
First.prototype.x = 111;

// Prototype Inheritance --inheriting Prototype Object I
Second.prototype = Object.create(First.prototype);
Second.prototype.constructor = Second; // Reset the constructor

// Creating Two Objects
var obj1 = new First();
var obj2 = new Second();

// Accessing the instance members of each objects
console.log(obj1.a);
console.log(obj2.b);

// Accessing the inherited instance properties of First class to Second class
console.log(obj2.a); // Returns 10

// Accessing the inherited prototype member
console.log(obj2.x);
```

## Understanding Prototype Inheritance by Example-1

```js
// Creating one Super class and two sub classes

// Super class
var Father = function (name) {
  this.name = name;
};

Father.prototype.bank_balance = "10 Lakhs";
Father.prototype.get_bank_balance = function () {
  return this.bank_balance;
};

// Creating two sub classes
var Daughter = function (name) {
  this.name = name;
};

var Son = function (name) {
  this.name = name;
};
// Prototype Inheritance
Daughter.prototype = Object.create(Father.prototype);
Daughter.prototype.constructor = Daughter;

Son.prototype = Object.create(Father.prototype);
Son.prototype.constructor = Son;

// Creating Objects
var Ram = new Father("Ram");
var Hari = new Son("Hari");
var Gita = new Daughter("Gita");

console.log(Ram.name);
console.log(Ram.get_bank_balance()); // 10 Lakhs
console.log(Hari.get_bank_balance()); // 10 Lakhs
console.log(Gita.get_bank_balance()); // 10 Lakhs
```

## Understanding Prototype Inheritance by Example-2

```js
// Prototype Inheritance by using function to avoid repetative codes while inheriting super class to sub class
// Creating one Super class and two sub classes

var Grand_father = function (name_gf) {
  this.name = name;
};

Grand_father.prototype.bank_balance = "20 Lakhs";
Grand_father.prototype.get_bank_balance = function () {
  return this.bank_balance;
};

var Grand_son = function (name) {
  this.name = name;
};

var Grand_daughter = function (name) {
  this.name = name;
};

// Creating a function to apply Prototype Inheritance
function Inheritance(child, parent) {
  child.prototype = Object.create(parent.prototype);
  child.prototype.constructor = child;
}

// Using the above function to inherit the prototype object
Inheritance(Grand_son, Grand_father);
Inheritance(Grand_daughter, Grand_father);

// Creating Objects

var Champaklal = new Grand_father("Champaklal");
var Tapu = new Grand_son("Tapu");
var Sonu = new Grand_daughter("Sonu");

console.log(Tapu.get_bank_balance()); // 20 Lakhs
console.log(Sonu.get_bank_balance()); // 20 Lakhs
```

## Method Overriding

```js
var Class1 = function one() {
  this.a = 10;
};

var Class2 = function two() {
  this.b = 20;
};
Inheritance(Class2, Class1);

Class1.prototype.show = function () {
  return "Super class";
};

var obj_one = new Class1();
var obj_two = new Class2();
console.log(obj_one.a);
console.log(obj_two.show()); // Super Class

Class2.prototype.show = function () {
  return "Sub Class";
};

console.log(obj_two.show()); // Sub Class
```

## Multi-Level Inheritance

- JavaScript does not support multiple inheritance.

```js
var Top = function () {
  this.p = 10;
};

var Middle = function () {
  Top.call(this);
  this.q = 20;
};

var Bottom = function () {
  Top.call(this);
  Middle.call(this);
  this.r = 30;
};

Inheritance(Middle, Top); // (Child, Parent)
Inheritance(Bottom, Middle); // (Child, Parent)

Top.prototype.fun1 = function () {
  return "Top";
};

Middle.prototype.fun2 = function () {
  return "Middle";
};

Bottom.prototype.fun3 = function () {
  return "Bottom";
};

var level1 = new Top();
var level2 = new Middle();
var level3 = new Bottom();

// Accessing own properties
console.log(level1.p);
console.log(level2.q);
console.log(level3.r);
// Accessing other class properties
console.log(level2.p);
console.log(level3.p);
console.log(level3.q);
// Accessing own prototype members
console.log(level1.fun1());
console.log(level2.fun2());
console.log(level3.fun3());
// Accessing other prototype members
console.log(level2.fun1());
console.log(level3.fun1());
console.log(level3.fun2());
```
