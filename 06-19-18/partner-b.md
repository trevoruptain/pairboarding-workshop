# Partner B

## Behavioral Questions (5 minutes)

- What is your greatest weakness as a software engineer? What are you doing to overcome that weakness?
- Tell me about a difficult decision you've made in the last year.

# Technical Questions

## Symmetric Tree ([Leetcode Link](https://leetcode.com/problems/symmetric-tree/description/))

Given a binary tree, check whether it is a mirror of itself.

For example, this binary tree is symmetric:

```
     1
   /   \
  2     2
 / \   / \
3   4 4   3
```

But the following is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

### Solution:
```ruby
def is_symmetric(root)
  return true if root.nil? || (root.left.nil? && root.right.nil?)
  check_siblings(root.left, root.right)
end

def check_siblings(left, right)
  return true if left.nil? && right.nil?
  return false if left.nil? ^ right.nil?
  return left.val == right.val &&
    check_siblings(left.left, right.right) &&
    check_siblings(left.right, right.left)
end
```

## Judge Route Circle ([LeetCode Link](https://leetcode.com/problems/judge-route-circle/solution/))

Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to the original place.

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are R (Right), L (Left), U (Up) and D (down). The output should be true or false representing whether the robot makes a circle.

**Example 1:**
```
Input: "UD"
Output: true
```

**Example 2:**
```
Input: "LL"
Output: false
```

### Solution:
```ruby
def judge_circle(moves)
    x = y = 0
    moves.chars.each do |move|
      if move == 'U'
        y -= 1
      elsif move == 'D'
        y += 1
      elsif move == 'L'
        x -= 1
      elsif move == 'R'
        x += 1
      end
    end

  return (x == 0 && y == 0)
end
```