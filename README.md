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

