### Variables
- `let` - local inside `{}` block
- `var` - local inside a function or global

### TDZ
```js
{ // enter new scope, TDZ starts
    let log = function () {
        console.log(message); // messagedeclared later
    };

    // calling log() here would cause a ReferenceError

    let message= 'Hello'; // TDZ ends
    log(); // called outside TDZ
}
```

### Constants
```js
// declaration
const TEST = 'hi';

// constant objects are immutable, but properties are changeable
const person = { age: 20 };
person.age = 30; // OK
person = {age: 30} // Error
```

### Arrow function
```js
// passing callback
setTimeout(() => console.log(i), 1000);
```

### Function params
```js
// default values
function test(a=1, b=2) {
    return a + b;
}

// required params
function req(x = (() => { throw new Error('this is a required argument') })()){
  return x * 2;
}

// variable list of params
function test(a,b,...args) {
   console.log(args) // array of all params except first two
}
```

### Spreading
```js
let a = [1,2];
let b = [...a, 3,4, ...a]; // [1,2,3,4,1,2]

```

### Object properties
```js
// Automatic properties from variables
let name = 'Computer', status = 'On';
let machine = { name, status};
console.log(machine) // { name: 'Computer', status: 'On' }

// Computed properies names
let obj = {[name]: 'Dell'}
console.log(obj); // {Computer: 'Dell'}
```

### Object methods
```js
let server = {
    name,
    restart() { // short syntax to define object methods
        console.log("The" + this.name + " is restarting...");
    }
};
```

### `for...of` loop
```js
// array itearting
for (let a of [1,2,3]) console.log(a);

// object destructing
const ratings = [
    {user: 'John',score: 3},
    {user: 'Jane',score: 4}
];

let sum = 0;
for (const {score} of ratings) { // "score" property of each object will go to "score variable"
    sum += score;
}
```

### Templates
```js
let a = 2;
let tpl = `hi ${a}` // hi 2
```

### Destructure
```js
let [a,b] = [1,2];
console.log(a) // 1

// object properties
let person = { firstName: 'John', lastName: 'Doe' };
let { firstName: fname, lastName: lname } = person;
console.log(fname) // John
```

### Importing modules
```js
import {some_var, some_func} from './module.js';
import * as cal from './cal.js'; // cal.var1, cal.func1 and so on ...
import './extension.js'; // e.g. for prototype definitions
```

### Classes
```js
class Person {
    constructor(name) {
        this.name = name;
    }
    getName() {
        return this.name;
    }
}

let p1 = new Person('Denys')
console.log(p1.getName()) // Denys
```
