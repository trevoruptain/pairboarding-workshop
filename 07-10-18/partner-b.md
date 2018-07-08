# Partner B

## Played Yourself

Tell me about a time when you missed an obvious solution to a problem. 

## Almost Sorted

Timestamped data may not always make it into the database in the perfect order. This is caused by server loads, network routes, etc. Your job is to take in a very long sequence of numbers in real-time and efficiently print them out in the correct order. Each number is, at most, `k` away from its final sorted position. Target time complexity is `O(nlogk)` and target space is `O(k)`.

### Questions for your partner?

* What is the naive solution? Time complexity?
* How can we rephrase the defining property of the input stream that might give us insight into how to build our output?
* What is the best data structure to use for this problem, and why is it a heap?

## Solution

* If the stream ends, we could store it and sort it: `O(nlogn)`. If the stream is truly unending, this would not work.
* We can rephrase the property as: "the correct output element will always be found within k steps from the index we are trying to populate".
* This implies that we could store the most recent `k` element and find the minimum: `O(nk)`
* Since we know we want the minimum from this stored set, that implies MinHeap and we can achieve `O(nlogk)`

```ruby
require_relative 'heap'

def almost_sorted(arr, k)
  heap = BinaryMinHeap.new
  # If k = 2, the first output element must be
  # within the first 3 numbers, so we build a heap of 3
  (k + 1).times do
    heap.push(arr.shift)
  end

  # Accounts for when the array runs out but we still have
  # numbers in our heap
  while heap.count > 0
    print heap.extract
    heap.push(arr.shift) if arr[0]
  end
end

arr = [3, -1, 2, 6, 4, 5, 8]
almost_sorted(arr, 2)
```
