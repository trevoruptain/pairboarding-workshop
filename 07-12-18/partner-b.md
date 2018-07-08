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

## Taking Your Chances

A  gangster kidnaps you. He puts two bullets in consecutive order in an empty six-round revolver, spins it, points it at your head and shoots. *click* You’re still alive. He then asks you, “do you want me to spin it again and fire or pull the trigger again right away?” For each option, what is the probability that you’ll be shot?

### Solution

The key hint here is that the bullets were loaded adjacent to each other.

There are 4 ways to arrange the revolver with consecutive bullets so that the first shot is blank. These are the possible scenarios:

* (xBBxxx)
* (xxBBxx)
* (xxxBBx)
* (xxxxBB)

The other two scenarios would have meant you got shot on the first attempt. (BBxxxx) or (BxxxxB)

Now look at the second slot in those 4 possible scenarios above. Your odds of getting shot are 1/4 or 25%. (Only #1 would get you shot)

But if you respin… there are 2 bullets remaining and 6 total slots. 2/6 or 33%.

## Apples and Oranges

There are three boxes, one contains only apples, one contains only oranges, and one contains both apples and oranges. The boxes have been incorrectly labeled such that no label identifies the actual contents of its box. Opening just one box, and without looking in the box, you take out one piece of fruit. By looking at the fruit, how can you immediately label all of the boxes correctly? 

### Solution

So, you know all 3 boxes are incorrectly labeled.

Go to the box labeled “Apples + Oranges.” Since the label is wrong, it must have one or the other.

This is the box to take one piece of fruit from. Whichever comes out is what that box contains. If you took out an apple, the box has only apples. If you took out an orange, vice versa.

Here’s where it gets tricky a bit tricky. But we’re almost done…

Let’s say you grabbed an apple. Move the “Apples” label over to that box. Now it’s correctly labeled.

You know the “Oranges” box is still labeled wrong (because all 3 were labeled wrong to start and you haven’t touched it). And you know it’s not “Apples”.

So it has to be “Apples + Oranges”.

The last box is “Oranges”.

The same process above would work if you had pulled out an orange at the start.

## Credit

Trivia questions taken from [this article](https://careersidekick.com/brain-teaser-job-interview-questions-facebook-google-apple/)

