# Partner A

## Behavioral Questions

* Give me an example of when you took an unpopular stance in a meeting with peers and your leader and you were the outlier. What was it, why did you feel strongly about it, and what did you do?
* How do you drive adoption for your vision/ideas? How do you know how well your idea or vision has been adopted by other teams or partners? Give a specific example highlighting one of your ideas.

## Find in Ordered Set
Given an array of sorted integers and an integer, write a function that will check to see if that integer exists in the array.

#### Solution 1 (Brute-force)
Iterate over the entire array and compare each element with the given integer.

```JavaScript
const binarySearch = (arr, target) => {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) return true;
  }
  return false;
};
```

- **Time Complexity** - *O*(*n*). *n* represents the number of elements in the input array. In this naive solution, the for loop may have to iterate through the entire array before finding the element that matches the target value.
- **Space Complexity** - *O*(1) constant extra space.


#### Solution 2 (Optimized)
Use a binary search algorithm.

```JavaScript
const binarySearch = (arr, target) => {
  // leftIdx & rightIdx act as "walls" that contain the indices
  // in which the target value exists.
  // initiate the walls to surround the entire array.
  let leftIdx = -1; // the index left of idx 0;
  let rightIdx = arr.length;

  while (leftIdx + 1 < rightIdx) {
    let idxRange = rightIdx - leftIdx;
    let middleIdx = Math.floor(idxRange/2);
    let guessIdx = leftIdx + middleIdx;
    let guessVal = arr[guessIdx];

    if (guessVal === target) return true;

    if (guessVal > target) {
      // target exists on the left half of the idxRange, update the right "wall"
      rightIdx = guessIdx;
    } else {
      // target exists on the right half of the idxRange, update the left "wall"
      leftIdx = guessIdx;
    }
  }
  return false;
};

// // sample test cases
// const arr = [1,2,3,4,5,6];
//
// console.log(binarySearch(arr, 4));
// console.log(binarySearch(arr, 8));
```

- **Time Complexity** - *O*(log<sub>2</sub>*n*). *n* represents the number of elements in the input array. Each time the function runs through the while loop, the number of elements that are considered is halved.
- **Space Complexity** - *O*(1) constant extra space

**Source:** [Interview Cake](https://www.interviewcake.com/question/javascript/find-in-ordered-set)

## Linked List Cycle

Given a linked list, determine if it has a cycle or loop in it.

Bonus: Can you solve it without using extra space?

```JavaScript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
```

#### JavaScript solution using a hash
```JavaScript
const hasCycle = (head) => {
  const hash = {};
  let node = head;

  while (node !== null) {
    if (hash[node.val] === node)  {
      return true;
    } else {
      hash[node.val] = node;
    }
    node = node.next;
  }
  
  return false;
};
```
- Time complexity : **O(n)**. We visit each of the **n** elements in the list at most once. Adding a node to the hash table costs only **O(1)** time.
- Space complexity: **O(n)**. The space depends on the number of elements added to the hash table, which contains at most **n** elements.

#### JavaScript solution using pointers
```JavaScript
const hasCycle = (head) => {
  if (head === null || head.next === null) return false;

  let slowPointer = head;
  let fastPointer = head.next;

  while (slowPointer !== fastPointer) {
    if (fastPointer === null || fastPointer.next === null) {
      return false;
    } else {
      slowPointer = slowPointer.next;
      fastPointer = fastPointer.next.next;
    }
  }
  return true;
};
```

- Time complexity : **O(n)**. Let us denote nn as the total number of nodes in the linked list. To analyze its time complexity, we consider the following two cases separately.
  - List has no cycle:
  The fast pointer reaches the end first and the run time depends on the list's length, which is **O(n)**.
  - List has a cycle:
  The worst case time complexity is **O(N+K)** (where **N** is the number of nodes and **K** is the number of node in the cycle/loop), which is **O(n)**.
- Space complexity : **O(1)**. We only use two nodes (slow and fast) so the space complexity is **O(1)**.

**Source: [Leetcode](https://leetcode.com/problems/linked-list-cycle/solution/)**
