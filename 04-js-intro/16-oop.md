# Object Oriented Programming

- [Introduction to Objects](#introduction-to-objects)
- [Object Properties](#object-properties)
- [Deleting properties from an object](#deleting-properties-from-an-object)
- [Object Methods](#object-methods)
- [The Prototype](#the-prototype)
- [Introduction to Classes](#introduction-to-classes)
- [Constructor Method](#constructor-method)
- [Static Methods](#static-methods)


## Introduction to Objects

- **object** is any value that's not of a primitive type
- objects are **always passed by reference**
  - arrays and functions are also objects under the hood
- objects can be defined in different ways
  - **object literal** syntax: `const car = { };`
  - `new Object()` and `Object.create()` syntax
- we can also initialize an object using the `new` keyword before a function constructor with a capital letter
  - then initialize the arguments we receive as parameters, to setup the initial state of the object

```js
function Car(brand, model) {
  this.brand = brand;
  this.model = model;
}

// initializing new object
const myCar = new Car('Ferrari', '812 GTS');
myCar.brand; //'Ferrari'
myCar.model; //'812 GTS'
```


## Object Properties

- objects have **properties**, which are composed by a property associated with a value
- properties value can be of any type, e.g., array, function or object
  - objects can have nested objects as properties
- properties can be any string, use quotes for invalid names that includes spaces, hypens or any special character
- multiple properties are separated by comma
- 2 different ways to access properties value: **dot notation** and **bracket notation** which is the only way to access invalid property names
  - accessing, adding or updating properties have the same notation
- accessing an unexisting property, will returned `undefined`

  ```js
  const car = {
    brand: {
      name: 'Ferrari'
    },
    'the brand': {
      name: 'Honda'
    },
    color: 'white'
  };

  // access: dot notation and bracket notation
  car.brand.name; // 'Ferrari'
  car['the brand']['name']; // 'Honda'

  car.doors; // undefined

  // adding/updating property
  car.model = '812 GTS';
  car.model; // 812 GTS
  ```


## Deleting properties from an object

- `delete` operator is used to delete a property/method from an object

  ```js
  // dot notation
  delete car.brand;

  // bracket notation
  delete car['brand'];
  ```


## Object Methods

- **methods** are functions assigned to an object property
- invoke with the parentheses at the end
- inside a method defined using a `function() {}` syntax we have access to the object instance by referencing `this`
  - we have access to the properties by using `this.properyName` syntax
- arrow functions doesn't have access to `this`
  - because **arrow functions are not bound to the object**
  - it's the reason why regular functions are often used as object methods

  ```js
  const car = {
    brand: 'Ferrari',
    model: '812 GTS',
    start: function() {
      console.log(`Started
        ${this.brand} ${this.model}`);
    },
    drive: destination => {
      console.log(`Drive going to ${destination}`);
    }
  };

  car.start();
  car.drive('Paris');
  ```


## The Prototype

- every JS object has a `prototype` property, which points to a different object called **object prototype**
- object prototype is used to inherit properties and methods
- `Object` is the prototype when creating an object
- `Array` is the prototype when initializing array
- `Object.getPrototypeOf()` and `Object.prototype.isPrototypeOf()` methods are used to check and verify prototype
- `Object.prototype` is the base prototype of all the objects
  - there is no prototype for `Object.prototype`, it's `null`
- **prototype chain** is prototype inside a prototype
  - object can extends Array and any object instantiated using it, will have Array and Object in its prototype chain and inherit properties and methods from all the ancestors

```js
const obj = {};
const arr = [];

Object.getPrototypeOf(obj) === Object.prototype; // true
Object.prototype.isPrototypeOf(obj); // true

Object.getPrototypeOf(arr) === Array.prototype; // true
Array.prototype.isPrototypeOf(arr); // true

Object.getPrototypeOf(Array.prototype) === Object.prototype; // true
Object.getPrototypeOf(Object.prototype); // null
Object.getPrototypeOf(Object.prototype) === Object.prototype; // false
```


## Introduction to Classes

- classes defines a common pattern for multiple objects
- **Convention**: Use PascalCase for classes
- from this class, we can initialize an object with `new` keyword followed by class name
  - `student` is an _instance_ of the `Person` class
- classes can hold properties and methods
- setting and accessing properties/methods are the same with objects

  ```js
  class Person {
    greet() {
      return 'Hi, how are you?';
    }
  }

  const student = new Person();
  student.greet(); // 'Hi, how are you?'

  // setting/accessing property
  student.name = 'John';
  student.name; // 'John'
  ```


## Constructor Method

- `constructor()` is used to initialize the class properties when creating a new object instance
- we can instantiate a new object from the class, passing a string, and when we call greet, we;ll get a personalized message
  - when the object is initialized, the constructor method is called, with any parameters passed

  ```js
  class Person {
    constructor(name) {
      this.name = name;
    }

    greet() {
      return 'Hello, I am ' + this.name + '.';
    }
  }

  const student = new Person('John')
  student.greet() // 'Hello, I am John.'
  ```


## Static Methods

- normally methods are defined on the object instance, not on the class
- we can define a method as static to allow it to be executed on the class instead

  ```js
  class Person {
    static genericGreeting() {
      return 'Hello';
    }
  }

  Person.genericGreeting() // Hello
  ```