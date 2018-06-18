# Behavorial Questions

1. What’s your favorite algorithm?

2. Tell me about a time you made a hard decision to sacrifice short term gain for a longer term goal.


# Technical Questions


## Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

```ruby
# Definition for singly-linked list.
# class ListNode
#     attr_accessor :val, :next
#     def initialize(val)
#         @val = val
#         @next = nil
#     end
# end

# @param {ListNode} l1
# @param {ListNode} l2
# @return {ListNode}
def merge_two_lists(l1, l2)
    
    dummy = ListNode.new(0)
    l3 = dummy
    
    while(!l1.nil? && !l2.nil?)
        if l1.val <= l2.val
            l3.next = l1
            l1 = l1.next
        else 
            l3.next = l2
            l2 = l2.next
        end
        
        l3 = l3.next
    end
    
    if(l1.nil?)
        l3.next = l2
    end
    
    if(l2.nil?)
        l3.next = l1
    end
    
    dummy.next
    
    
end
```


## Convert Sorted Array to Binary Search Tree

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:

Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

        0
       / \
     -3   9
     /   /
    -10  5



## solution

```ruby
# Definition for a binary tree node.
# class TreeNode
#     attr_accessor :val, :left, :right
#     def initialize(val)
#         @val = val
#         @left, @right = nil, nil
#     end
# end

# @param {Integer[]} nums
# @return {TreeNode}
def sorted_array_to_bst(nums)
   
    return nil if nums.nil? || nums.empty?
    
    mid = nums.length / 2
    n = TreeNode.new(nums[mid])
    n.left = sorted_array_to_bst(nums[0...mid])
    n.right = sorted_array_to_bst(nums[mid + 1..-1])
    n
    
end
```