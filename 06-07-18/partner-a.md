# Partner A

## Behavioral Questions

* Tell me a little bit about yourself and your journey to becoming a software engineer.
* What are some of your professional development goals?

## The Skyline Problem

A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Now suppose you are given the locations and height of all the buildings as shown on a cityscape photo (Figure A), write a program to output the skyline formed by these buildings collectively (Figure B).


<img src="https://leetcode.com/static/images/problemset/skyline1.jpg" alt="Drawing" style="width: 300px;"/>
<img src="https://leetcode.com/static/images/problemset/skyline2.jpg" alt="Drawing" style="width: 300px;"/>


The geometric information of each building is represented by a triplet of integers [Li, Ri, Hi], where Li and Ri are the x coordinates of the left and right edge of the ith building, respectively, and Hi is its height.

For instance, the dimensions of all buildings in Figure A are recorded as: `[ [2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8] ]` .

The output is a list of "key points" (red dots in Figure B) in the format of `[ [x1,y1], [x2, y2], [x3, y3], ... ]` that uniquely defines a skyline. A key point is the left endpoint of a horizontal line segment. Note that the last key point, where the rightmost building ends, is merely used to mark the termination of the skyline, and always has zero height. Also, the ground in between any two adjacent buildings should be considered part of the skyline contour.

For instance, the skyline in Figure B should be represented as:`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`.

Notes:
* The input list is already sorted in ascending order by the left x position Li.
* The output list must be sorted by the x position.
* There must be no consecutive horizontal lines of equal height in the output skyline. For instance, `[...[2 3], [4 5], [7 5], [11 5], [12 7]...]` is not acceptable; the three lines of height 5 should be merged into one in the final output as such: `[...[2 3], [4 5], [12 7], ...]`

#### Follow-ups (15 mins)

What is the time complexity of your solution?

What if our position and height information were floats? How would this change your approach?

Bonus: Can you achieve an `nlogn` solution?


### Solution

```ruby
def skyline(buildings)

  # find the max_x of all buildings
  max_x = buildings.max_by { |b| b[1] }[1]

  # create an array containing height information for every position
  # initialize it with [x,0] for every position up to max
  height_arr = []
  (max_x + 1).times do |i|
    height_arr << [i, 0]
  end

  # for each building go from its left to right coordinate and replace
  # the corresponding height info in our height_arr if greater
  buildings.each do |build|
    (build[0]..build[1]).each do |i|
      height_arr[i][1] = build[2] if build[2] > height_arr[i][1]
    end
  end

  # in order to output the skyline coordinates correctly we need to
  # consider drops in height to mean the LOWER number (see [7, 12])
  height_arr.each_with_index do |coord, i|
    next if i == 0
    height_arr[i-1][1] = coord[1] if coord[1] < height_arr[i-1][1]
  end

  result = []

  # iterate over our height_arr and generate "key points"
  (0..height_arr.length-1).each do |i|

    # skipping until we hit our first building, as specified
    next if result.empty? && height_arr[i][1].zero?

    # if we have a height at x == 0 just register it
    if i == 0
      result << height_arr[i]
      next
    end

    # when we have a change in height we register it
    result << height_arr[i] if height_arr[i][1] != height_arr[i-1][1]

    # log the last point as zero, as specified
    result << [i, 0] if i == height_arr.length - 1
  end

  result
end

p skyline([ [2, 9, 10], [3, 7, 15], [5, 12, 12], [15, 20, 10], [19, 24, 8] ])
  == [[2, 10], [3, 15], [7, 12], [12, 0], [15, 10], [20, 8], [24, 0]]

```

### Follow-ups Solutions

* Time-Complexity: The nested loop that goes through every rectangle and hits every 'pixel' in our height array that is subtended by that rectangle give us a time-complexity of `O(nm)` in the worst case, where `n` is the number of buildings and `m` is the maximum number of width pixels.

* Floats: If our rectangles had coordinates that were floats, then using a height array would be more tricky. For example, if the `max_x` were 10, but one of the left corners were 8.8, then the height array would have to have 100 buckets; in other words the height array would have to have the same resolution as our input information.

* Floats: One way to optimize this would be to first get a set (hash) of critical points: points at the left or right corners of the rectangles. Heights will only change at these points. Then you can loop through the rectangles and update the heights of any critical points that fall in the range of each rectangle. Now you can handle floats trivially because we are using a hash rather than an array!

* nlogn: This is a little trickier. If we have a sorted set of critical points then as we scan through them we can keep a set of 'active rectangles'. Thus, any
time we encounter a left edge we add to our set of actives, any time we encounter a right edge we take away from the set. How could we efficiently keep track of which points are left edges and which ones right edges? Furthermore, anytime we hit a critical point we register the largest height from our active set at that critical point. What data structure would allow us to optimally select the largest height from our active set? Discuss all the specifics of implementing this strategy!

Credit: [LeetCode](https://leetcode.com/problems/the-skyline-problem/description/)
