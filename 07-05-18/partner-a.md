# Partner A

## Looking Ahead

* What do you want to do in 5 years? How would this job fit into your plan and help you toward your goals?

## The Big Picture

* What happens when you type in 'www.google.com' and hit enter?

### Answer 

This is one of the most common interview questions of all time. **It will come up at interviews.** Memorize it.

0. Browser checks its own DNS cache for a corresponding IP address, then your OS’ DNS cache, then (most likely) checks the default router's DNS cache, then ISP / configured DNS server until it gets an answer.
0. Browser builds HTTP GET string with “http://[url]” as the requested URL
0. Browser sends request over the network (if asked how that works, mention the Border Gateway Protocol and say you don’t know how it works)
0. (Possible interaction with proxy server / load balancer / CDN / etc.)
0. Server parses request string and routes it using Regex on the request path
0. Application layer assembles a response, possibly via a connection to a DB server
0. Response goes back over the network
0. Browser parses the response
0. Browser checks the headers, in particular the status code.
0. Browser goes down each HTML element and either paints the DOM or executes the tag
0. The browser builds a new GET request for each CSS or JS tag, goes through the same steps as above, and runs the code before proceeding.

Further reading:

* [Link 1 (short)][quora scrape]
* [Link 2 (medium)][igoro]
* [Link 3 (long)][what happens repo]

[quora scrape]: https://jiangchengl.wordpress.com/2015/08/20/what-happens-when-you-type-www-example-com-in-the-browser-address-and-enter-press-button/
[igoro]: http://igoro.com/archive/what-really-happens-when-you-navigate-to-a-url/comment-page-4/
[what happens repo]: https://github.com/alex/what-happens-when

## Find the Missing Number

* You are given an unsorted array of integers ranging from 1 to ```array.length - 1```. Each number appears once, except for a single number, which is missing from the array. Find that missing number.

### Solution

You could sort the array then iterate through it to find the missing number. However, the sorting would take ```O(nlog n)``` time. This problem can be solved in linear time by utilizing the fact that the sum of a linear series of n numbers is ```n *(n+1) / 2```. 

```javascript
function missingNumber(arr) {
  let n = arr.length + 1;
  let sum = 0;
  let expectedSum = n * (n+1) / 2;
  
  for(var i = 0, i < arr.length; i++){
    sum += arr[i];
  }
  
  return expectedSum - sum;
}
```

## Well-formed String

A string with the characters `[,],{,},(,)` is said to be well-formed if the different types of brackets match in the correct order.

For example, `([]){()}` is well-formed, but `[(]{)}` is not.

Write a function to test whether a string is well-formed.

### Solution

* This is the perfect situation for a stack.
* If we store all left brackets in a stack then every time we encounter a right bracket, its pair should be on the top of the stack, or else it is unmatched.
* Additionally, if there are any unmatched left brackets at the end, the string is not well-formed.

---
```ruby
def well_formed(str)
  left_chars = []
  lookup = { '(' => ')', '['=> ']', '{'=> '}' }

  str.chars.each do |char|
    if lookup.keys.include?(char)
      left_chars << char
    elsif left_chars.length == 0 || lookup[left_chars.pop] != char
      return false
    end
  end
  return left_chars.empty?
end
```
