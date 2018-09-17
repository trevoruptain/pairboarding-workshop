# Partner A

## Dev Cycles
* We are in the middle of a development cycle (or sprint if you use agile) and there is a major change in the functionality of a feature you have been working on.
* How do you respond?
* What questions do you ask?

## Cloning
* How do you clone and object in JS?

### Answer
```javascript
var obj = {a: 1 ,b: 2}
var objclone = Object.assign({},obj);
```

Now the value of objclone is `{a: 1 ,b: 2}` but points to a different object than `obj`.

Note the potential pitfall, though: `Object.clone()` will just do a shallow copy, not a deep copy. This means that nested objects aren’t copied. They still refer to the same nested objects as the original:

```javascript
let obj = {
    a: 1,
    b: 2,
    c: {
        age: 30
    }
};

var objclone = Object.assign({},obj);
console.log('objclone: ', objclone);

obj.c.age = 45;
console.log('After Change - obj: ', obj);           // 45 - This also changes
console.log('After Change - objclone: ', objclone); // 45
```
