## Find the Median from a Data Stream

The median is the middle number in an ordered array of integers. If the length of the array is even, there is no middle value, so the median is the average of the two middle numbers.

```ruby
median([1, 2, 3, 4, 5]) => 3
median([1, 2, 3, 4]) => (2 + 3) / 2 => 2.5
```

You are designing a data structure that accepts an incoming data stream of integers. Write an API for your data structure which supports the following operations:

* ```add()``` accepts an integer from the stream and adds it to your data structure
* ```find_median()``` returns the median of all elements which have been added from the stream so far

### Example

```ruby
add(8)
find_median() => 8
add(16)
find_median() => 12
add(4)
find_median() => 8
```

### Requirements:

* ```O(log n)``` time complexity for insertion
* ```O(1)``` lookup for the median value
* ```O(n)``` maximum space to store the dataset

### Hints:

* You could store incoming elements in an array, sort it after each insertion, and index into the middle of the array to find the median. However, this exceeds our time limit.
* You could use insertion sort to maintain a sorted list. However, insertion would take ```O(nlog n)``` time, which also exceeds our limit.
* If only there were a data structure with ```log n``` insertion which allowed us to look up its maximum or minimum value in constant time...

## Solution

We can make two inferences from the prompt for this problem:

* If we could maintain direct access to median elements at all times, then finding the median would take a constant amount of time.
* If we could find a reasonably fast way of adding numbers to our containers, additional penalties incurred could be lessened.

As you may have guessed based on the prompt, we will need to use heaps to solve this problem! The naive approaches mentioned in the hints sort the entire dataset. The key insight here is that we don't need to sort our entire dataset. Instead, we only need a way to access the median elements in constant time.

We can solve this problem using two heaps:

* A max heap to store the smaller half of our dataset
* A min heap to store the larger half of our dataset

As long as our two heaps are balanced (meaning their lengths differ by at most one), we can find the median by examining the top most elements of our heaps. If ```(MaxHeap.length - MinHeap.length).abs == 1```, our median is simply the top element of the longer heap. If ```(MaxHeap.length == MinHeap.length)```, the median is the average of the top values of both heaps.

We can simplify things for ourselves by only allowing ```MaxHeap``` to be the larger heap. This means that, if we have inserted ```n``` elements, only the following conditions are possible:

* ```MinHeap.length == (n / 2)``` and ```MaxHeap.length == (n / 2)```
* ```MinHeap.length == (n / 2)``` and ```MaxHeap.length == (n / 2) + 1```

Now it is trivial to determine which method we should use to compute the median by comparing the length of the two heaps.

The only part of this problem which remains is the insertion set. We insert an integer ```k``` into our data structure by following these steps:

* Insert ```k``` into ```MaxHeap```.
* Since ```MaxHeap``` just received a new element, we remove the largest element from ```MaxHeap``` and insert it into ```MinHeap```.
* Now, we check to see if ```MinHeap.length``` > ```MaxHeap.length```. If it is, our heaps are imbalanced. We therefore remove the smallest element from ```MinHeap``` and insert it into ```MaxHeap```.

Let's take a look at an example:

```ruby
insert(41)
MaxHeap: [41] # MaxHeap stores the largest value at the top (index 0)
MinHeap: [] # MinHeap stores the smallest value at the top (index 0)
Median: 41
=======================
insert(35)
MaxHeap: [35]
MinHeap: [41]
Median: 38
=======================
insert(62)
MaxHeap: [41, 35]
MinHeap: [62]
Median: 41
=======================
insert(4)
MaxHeap: [35, 4]
MinHeap: [41, 62]
Median: 38
=======================
insert(97)
MaxHeap: [41, 35, 4]
MinHeap: [62, 97]
Median: 41
=======================
insert(108)
MaxHeap: [41, 35, 4]
MinHeap: [62, 97, 108]
Median: 51.5
```

## Solution

```ruby
require_relative 'max_heap'
require_relative 'min_heap'

class MedianFinder
  def initialize
    @low = MaxHeap.new
    @high = MinHeap.new
  end

  def add(n)
    @low.push(n)
    @high.push(@low.extract)

    if @high.count > @low.count
      @low.push(@high.extract)
    end
  end

  def find_median
    if @low.count > @high.count
      @low.peek
    else
      (@low.peek + @high.peek) / 2
    end
  end
end
```

## Credit

* The prompt and solution are adapted from [this problem](https://leetcode.com/problems/find-median-from-data-stream/description/) from Leetcode.
