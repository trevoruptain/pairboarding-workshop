# Partner B

## Playing Nice

Do you do your best work alone or in a group?  Does the type of work matter?

## Longest Increasing Subsequence

Given an array of integers, find the length of the longest increasing subsequence.

### Example: 

```
[1,5,2,6,10,4,20] => 5, [1,2,6,10,20]
```

### Solution

At each index, the solution is the longest preceding solution that terminates in a number less than the number we are considering (plus the current number).

If we accumulate the optimal solutions for every index, we can then choose among them.

```ruby
def longest_sub(arr)

  # Create an array of length arr.size to store the longest
  # subsequence which terminates at each index
  longest = Array.new(arr.size) { Array.new }

  # Base case
  longest[0] << arr[0]

  # Starting at 1 iterate through the longest sequences up
  # to that point
  (1...arr.size).each do |i|
    (0...i).each do |j|

      # As we iterate up to i, if arr[i] is less than arr[j]
      # and if what we have stored as the candidate for
      # longest[i] is shorter than what we could make by
      # selecting a new sequence, then we store that as
      # the longest[i] (must dup it)
      if arr[j] < arr[i] && longest[i].size < longest[j].size + 1
        longest[i] = longest[j].dup
      end
    end

    # Once we have determined the longest qualifying sequence
    # up to i, we append arr[i] onto it; thus we store the
    # longest increasing subsequence that terminates at i
    longest[i] << arr[i]
  end

  # Selecting the longest one and returning its length
  longest.max_by(&:length).length
end
```
