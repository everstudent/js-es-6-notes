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
// short syntax
let add = (x, y) => x + y;
add(1,2) // 3

// longer syntax
let add = (x, y) => {return x + y; };
add(1,2) // 3

// passing callback
setTimeout(() => console.log(i), 1000);
```

Don't use arrow function when you want to refer to `this.*` inside a function context.

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
class Person extends People { // inherit "People" class
    constructor(name) {
        super(name) // call parent constructor
        this.name = name;
    }
    getName() {
        return this.name;
    }
    static callMeStatically(x) { // static method
        return 2;
    }
}

let p1 = new Person('Denys')
console.log(p1.getName()) // Denys
```

### Iterator
```js
class Sequence {
    constructor( start = 0, end = Infinity, interval = 1 ) {
        this.start = start;
        this.end = end;
        this.interval = interval;
    }
    [Symbol.iterator]() { // this method should return iterator protocol object with "next()" function that returns an object: {value: , done: }
        let counter = 0;
        let nextIndex = this.start;
        return  {
            next: () => {
                if ( nextIndex <= this.end ) {
                    let result = { value: nextIndex,  done: false }
                    nextIndex += this.interval;
                    counter++;
                    return result;
                }
                return { value: counter, done: true };
            }
        }
    }
};
```

### Function generator
```js
function* generate(n = 100) {
    for ( let i = 0; i < n; i++ ) {
        yield i;
    }
}

let gen = generate(10);
console.log(gen.next()); // { value: 0, done: false }
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
```

### Promises
Promise - is a result object of async operation
```js
function getUsers() {
  return new Promise((resolve, reject) => { // revolve is called when ok, reject is called when not ok
    setTimeout(() => {
      resolve([
        { username: 'john', email: 'john@test.com' },
        { username: 'jane', email: 'jane@test.com' },
      ]);
    }, 1000);
  });
}

const promise = getUsers();

promise.then((users) => { // then accepts resolve/reject callbacks
  console.log(users);
});

promise.catch(...... // only error callback
promise.finally(.... // either error or success (any) callback


// resolve all promises callback
Promise.all([p1, p2, p3]).then((results) => { // p1, p2, p3 - promises, "results" - array of returned values in promises
    console.log('ok');
});


// handle first resolved/rejected promise
Promise.race([p1, p2]) // p1, p2 - promises
    .then(value => console.log(`Resolved: ${value}`))
    .catch(reason => console.log(`Rejected: ${reason}`));
```

### Maps
```js
let users = new Map(); // key-value structure
users.set('den', {name: 'Denys'});
users.set('zhenya', {name: 'Yevheniia'});
console.log(users.size); // 2
```

### Sets
Stores a collection of unique values:
```js
let row = new Set(['den', 'zhenya']);
```

### Arrays
```js
// create arrays from values
console.log( Array.of(1,2,'a') ); // [ 1, 2, 'a' ]

// create array from iterable object
Array.from( Iterable ); // => [...]

// mapping
console.log(Array.from( [1, 2, 3], x => x * x )); // [ 1, 4, 9 ]

// find first value by callback
console.log( [1, 2, 3, 4, 5].find(x => x > 3) ); // 4
console.log( [1, 2, 3, 4, 5].findIndex(x => x > 3) ); // 3
```

### Cloning and merging
```js
let clone = Object.assign({}, obj); // "obj" cloned into "clone"
let merged = Object.assign({}, obj1, obj2); // "obj1" and "obj2" merged into "merged"
```

### String search
```js
console.log( 'hi den'.startsWith('hi') );   // true 
console.log( 'hi den'.endsWith('den') );    // true
console.log( 'hi den'.includes('de') );     // true
console.log( 'hi den'.includes('aaa') );    // false
```

### Proxies
```js
const user = {
    firstName: 'John',
    lastName: 'Doe',
    email: 'john.doe@example.com',
}

const handler = {
    get(target, property) {
        return target[property] + '!';
    }
}

let proxyUser = new Proxy(user, handler);

console.log( proxyUser.email ); // john.doe@example.com!
```

### Reflections
```js
Reflect.apply(functionName, thisArg, args); // call "functionName" with "this" pointing to "thisArg" and "args" arguments list
```
