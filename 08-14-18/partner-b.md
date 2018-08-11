# Partner B

## Culture Fit
* There are many types of company cultures...what type of culture is important to you?
* What are ways you develop relationships with collaborators/team mates?

## You get a pass
* Does JavaScript pass by value or by reference?

### Answer
* Primitive types (strings, numbers, etc.) are passed by value & objects are passed by reference.  If you change the properties of the passed object, the change will be affected.  However, if you assign a new object to the passed object, the changes will not be reflected.  You can read more about it [here](https://snook.ca/archives/javascript/javascript_pass).

```JavaScript
var num = 10,
    name = "Addy Osmani",
    obj1 = {
      value: "first value"
    },
    obj2 = {
     value: "second value"
    },
    obj3 = obj2;

function change(num, name, obj1, obj2) {
    num = num * 10;
    name = "Paul Irish";
    obj1 = obj2;
    obj2.value = "new value";
}

change(num, name, obj1, obj2);

console.log(num); // 10
console.log(name);// "Addy Osmani"
console.log(obj1.value);//"first value"
console.log(obj2.value);//"new value"
console.log(obj3.value);//"new value"        
```
