### `let` vs `var`
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

### arrow function
```js
// passing callback
setTimeout(() => console.log(i), 1000);
```
