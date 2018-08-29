# Partner B

## Longest Substring Without Duplication

Write a function that takes in a string and that returns its longest substring without duplicate characters.  Assume that there will only be one longest substring without duplication.

```
Sample Input: "clementisacap"
Sample Output: "mentisac"
```

### Answer
We can solve this problem efficiently by traversing the string and storing the last position at which we see each character in a hash table which we'll call `lastSeen`.  We'll also keep track of the `longest` string we've seen so far.  As we traverse the string we'll keep track of a variable called `startIdx` which will represent the most recent index from which we can start a substring with no duplicate characters, ending at the current index.  If we come across a character that we've already seen then we'll update our `startIdx` to be the maximum of the current `startIdx` and the position of the element the last time we saw it + 1.  Updating the `startIdx` in this way will make sure that we don't end up moving the `startIdx` backward when we encounter a duplicate character late in the string.  If the current string from the `startIdx` to the current position + 1 is greater than the length of the `longest` string we've seen so far, we'll update `longest` to the current string.
