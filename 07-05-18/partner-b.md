# Partner B 

## Playing Favorites

* What's your favorite algorithm?

NB: The only correct answer to this question is ```bubble sort```!

## Losing Your Marbles

* You have 20 jars full of marbles. You also have a scale. Each marble weighs 1 gram, except for the marbles in 1 jar, which each weigh 1.1 grams. Using your scale only once, how can you identify the jar with the heavy marbles?

### Answer

Label the jars successively - Jar 1, Jar 2, etc. Remove n marbles from each jar. i.e. remove 1 marble from Jar 1 and 15 marbles from Jar 15. Weigh all of the marbles you've removed on the scale. You know that if all of the marbles you removed each weighed 1 gram, the total weight would be 210 grams (using n(n + 1) / 2). However, there will be additional weight from the heavy marbles. Divide the extra weight by 0.1 to determine the number of the heavy jar!

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


root = Node.new(3)

root.right = Node.new(5)
root.right.right = Node.new(6)
root.right.left = Node.new(4)

root.left = Node.new(1)
root.left.left = Node.new(0)
root.left.right = Node.new(2)

root.print

smallest = bst_to_cll(root)

smallest.print
```
