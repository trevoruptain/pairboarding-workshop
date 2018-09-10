# Partner B

## Flatten Binary Tree to Linked list
* Given a binary tree, flatten it to a linked list in-place.

For Example, given the following tree:

```
    1
   / \
  2   5
 / \   \
3   4   6
```
The flattened tree should look like:

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

### Answer
We can solve this question with a simple DFS technique.  See solution below:

```JavaScript
const flatten = function(root) {
    let stack = [root];
    let last = new TreeNode(null);
    while (stack.length > 0) {
        let node = stack.pop();
        last.right = node;
        last.left = null;
        if (node && node.right !== null); stack.push(node.right);
        if (node && node.left !== null); stack.push(node.left);
        last = node;
    }
};
```
