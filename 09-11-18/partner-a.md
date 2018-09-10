# Partner A

## Back on Track!
* Tell me about a time when one of your projects got off­ track (a deadline was at risk or you were stuck because of a big obstacle).
* What did you do to get it back on track?

## Inner HTML VS. Append Child
* What is the best way to create a DOM element? Set innherHTML or use createElement?

### Answer
When you set the `innerHTML` property, the browser removes all the current children of the elements. Parses the string and assigns the parsed string to the element as children.

For example, if you want to add a list item to an unorderedList. You can get the element and set the `innerHTML` of the element like so:

```JavaScript
var ul = document.getElementById('myList');

el.innerHTML = '<li>Only one item</li>';
```              

**Extra Credit:** `innerHTML` could be slow while parsing a string. The browser has to deal with the string and if you have invalid html.

`appendChild` on the other hand, creates a new Element. Since you are creating it, the browser doesn't have to parse string and there is no invalid html. You can pass the child to the parent and child will be appended to the parent.

```JavaScript
var li = document.createElement("li");
var text = document.createTextNode('Only one Item');

li.appendChild(text);
ul.appendChild(li);
```

**Extra Credit:** If you pass a reference to be appended as child rather than creating a new element. The reference you are passing will be removed from the current parent and will be added to the new parent you are appending to.  Although you would be writing couple more lines of JavaScript, it makes browsers life easier and your page faster.
