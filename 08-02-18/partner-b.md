# Partner B

## Playing Favorites

* What's your favorite algorithm?

NB: The only correct answer to this question is ```bubble sort```!

## Function Declaration VS Function Expression

* What is the difference between a function declaration and a function expression in JavaScript & why does it matter?

### Answer
Function declarations begin with the ‘function’ keyword and must be named. We can pass values in the form of arguments and also return values. If a value is not returned, then the function will return undefined.
```JavaScript
// Declaration
function helloWorld() {
  return "hello world";
}
// Expression
var helloWorld = function() {
  return "hello world";
}
```
Although function declarations and function expressions are similar and often interchangeable, there is an important distinction:

Function Declarations are hoisted or pulled to the top of the function making them available regardless of position. So, we can call a function and then declare it further down and still access the function.
This may seem confusing since javascript typically interprets code line by line, from top to bottom. Despite this, **function and also variable declarations are hoisted by the javascript interpreter while function and variables expressions are not.**

## BST to Linked List

Given the root node of a binary search tree, return an in-order doubly-linked circular linked list.

```
input:
      3
    /   \
  1       5
 / \     / \
0   2   4   6

output:

... 6 <=> 0 <=>1 <=> 2 <=> 3 <=> 4 <=> 5 <=> 6 <=> 0 ...

or...

 0 <=> 1 <=> 2
 ^             ^
 |             3
 v             v
 6 <=> 5 <=> 4
```

### Solution

```ruby
ruby
class Node
    attr_accessor :left, :right, :val
    def initialize(val)
        @val = val
        @left, @right = nil, nil
    end

    def print
        str = "#{val} -> "
        current = self.right
        while current != self && current != nil
            str += "#{current.val} -> "
            current = current.right
        end

        if current == nil
            str += "nil"
        else
            str += "#{current.val} -> "
        end
        puts str
    end
end

def bst_to_cll(node)
    if !node.left && !node.left
        node.left = node
        node.right = node
        return node
    end
    p node.val
    right = node.right
    left = node.left

    if left
        lowest_left = bst_to_cll(left)

        node.left = lowest_left.left
        lowest_left.left.right = node

        node.right = lowest_left
        lowest_left.left = node
    end


    if right
        lowest_right = bst_to_cll(right)

        max = lowest_right.left
        lowest_left = node.right



        max.right = lowest_left
        lowest_left.left = max

        node.right = lowest_right
        lowest_right.left = node

        return lowest_left
    end

    return node.right
end
```
