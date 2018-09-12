## Remove Kth Node From End Of Linked List

* Given a linked list, remove the k-th node from the end of list and return its head.
* Could you do this in one pass?

Example:

```
Given linked list: 1->2->3->4->5, and k = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

Note:
Given k will always be valid.

### Answer
To solve this problem we'll use two pointers. The first pointer advances the list by n+1 steps from the beginning, while the second pointer starts from the beginning of the list. Now, both pointers are exactly separated by n nodes apart. We maintain this constant gap by advancing both pointers together until the first pointer arrives past the last node. The second pointer will be pointing at the nth node counting from the last. We relink the next pointer of the node referenced by the second pointer to point to the node's next next node.  The time complexity of this problem is O(n) and the space is O(1).

```JavaScript
const removeNthFromEnd = (head, n) => {
    let dummy = new ListNode(0);
    dummy.next = head;
    let first = dummy;
    let second = dummy;
    // Advances first pointer so that the gap between first and second is n nodes apart
    for (let i = 1; i <= n + 1; i++) {
        first = first.next;
    }
    // Move first to the end, maintaining the gap
    while (first !== null) {
        first = first.next;
        second = second.next;
    }
    second.next = second.next.next;
    return dummy.next;
}
```
