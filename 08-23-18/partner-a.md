# Partner A

## Who likes you
* Tell me about a time you were able to successfully deal with another person even when that individual
may not have personally liked you (or vice versa).

## Trivia
* Consider the two functions below. Will they both return the same thing? Why or why not?

```JavaScript
function foo1()
{
  return {
      bar: "hello"
  };
}

function foo2()
{
  return
  {
      bar: "hello"
  };
}
```

### Answer
Not only is this surprising, but what makes this particularly gnarly is that `foo2()` returns undefined without any error being thrown.

The reason for this has to do with the fact that semicolons are technically optional in JavaScript (although omitting them is generally really bad form). As a result, when the line containing the `return` statement (with nothing else on the line) is encountered in `foo2()`, a semicolon is automatically inserted immediately after the return statement.

No error is thrown since the remainder of the code is perfectly valid, even though it doesn’t ever get invoked or do anything (it is simply an unused code block that defines a property `bar` which is equal to the string `"hello"`).

This behavior also argues for following the convention of placing an opening curly brace at the end of a line in JavaScript, rather than on the beginning of a new line. As shown here, this becomes more than just a stylistic preference in JavaScript.

## Find the in-order successor for a given key in a BST
* Given a BST, find the in-order successor of a given key in it.  If the given key doesn't appear in the BST, then return the next greater key (if any) present in the BST.

An in-order successor of a node in a BST is the next node in the in-order traversal of it.  Consider the below BST:

```
      15
    /    \
  10      20
 /  \     / \
8   12  16   25

- The in-order successor of 8 is 10
- The in-order successor of 12 is 15
- The in-order successor of 25 doesn't exist
```
