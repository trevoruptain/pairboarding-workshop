## Introduction

Tell me about your career path up to this point.

(Assume you are applying to an early stage startup that builds a platform to help nonprofits collect donations)

## Being Managed

Describe a time you disagreed with your manager and how you handled it.

**NB**: if you haven't been employed before, replace "manager" with another authority figure like a professor or teacher.

## `streaming_sample`

You know how to use `rand` to randomly sample an element from an
array.

Now, write a function that, given an input stream of objects, will
sample a value. The stream has limited length.

* Use only `O(1)` memory.
* Every value in the stream should have an equal probability of being
  sampled.

### Solution

```ruby
def streaming_sample(stream)
  sample = stream
  num_els = 1 #needs to set to the first stream because otherwise first one never gets picked

  while true
    next_value = stream.next_value
    break if next_value.nil?

    # keep sample with probability 1 / (num_els + 1)
    keep_prob = 1.fdiv(num_els + 1)
    sample = next_value if rand() < keep_prob

    num_els += 1
  end

  sample
end
```

Let's prove this works by **induction**. First, note that for `num_els
= 1`, this says we keep the previous sample (`nil`), with probability
`0`. So after 1 element, every element has an equal chance of being
sampled (the only element is selected with probability `1`).

Next, assume that we've iterated through `m` elements, and that the
streaming sample has selected an element (so far) with equal
probability `1/m`. Then the probability of keeping the current sampled
element after considering the `m + 1`th element is `1 / m * m / (m +
1) == 1 / (m + 1)`. Likewise, the probability of selecting the `m +
1`th element is `1 / (m + 1)`.

## `median`

Given two **sorted** arrays, find the median element amongst the two
arrays. That is, if both arrays were combined, find the median element
from the combined array. Assume that there is not enough memory to
actually combine both arrays. There exists an O(log n + log m)
solution.

### Solution

Since they are sorted, you can find the middle element of each to find
the medians of each list. The actual median is now somewhere in
between these two numbers. You can then discard the non-relevant
portions of each list. Repeat the process. When the middle elements
from both lists converge, you have now found the median element.
