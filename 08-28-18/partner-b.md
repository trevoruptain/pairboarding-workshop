# Partner B

## Are you effective?
* What three things are you working on to improve your overall effectiveness?

## Warm-up
* Given an array of length N, with integer values between 0 and N (not including 0 or N), return any integer that appears in the array more than once, i.e.

```
[ 1, 2, 3, 3, 4 ] => 3
[ 3, 1, 2, 2, 5, 5 ] => 2 or 5 (either is fine)
[ 0, 1, 2 ] => invalid input (can’t have 0)
```

Bonus: **Can you get your solution down to O(1) space?**

### Answer
For each number (K), multiply the value at index K by -1. If the value at that index is already negative, that is the duplicate value.

```
[ 3, 1, 1, 2 ] => [ 3, 1, 1, -2 ]
[ 3, 1, 1, -2 ] => [ 3, -1, 1, -2 ]
[ 3, -1, 1, -2 ] => [ 3, -1, 1, -2 ] => return 1
```

## Longest Palindromic Substring
* Given a string s, find the longest palindromic substring in s.

```
Example 1:
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

```
Example:
Input: "cbbd"
Output: "bb"
```

### Answer
**Non-optimal Solution - best case O(N), worst case O(N^2)**

This is a non optimal (see below for optimal solution), but much easier to understand solution. It uses the following algorithm. At a position of the string, it compares the character at the left and right to see if they're the same. If they are, it looks one character further out on each side and compares them. And so on until it reaches an end of the string or finds the two characters are different. It does this at each position of the string, finding the longest palindrome centered around each position, keeping track of which is longest overall.

```ruby
def find_longest_palindrome(s)  
  longest = ""  
  0.upto s.length do |i|  
   odd = palindrome_at_position(s, i, i)  
   longest = odd if odd.length > longest.size  
   # handle even length palindromes  
   even = palindrome_at_position(s, i, i+1)  
   longest = even if even.length > longest.size  
  end  
  longest  
 end

 def palindrome_at_position(s, left, right)  
  palindrome = ""  
  while (right < s.length &&  
      left >= 0 &&  
      s[left] == s[right])  
   palindrome = s[left,(right-left+1)]  
   left -= 1  
   right += 1  
  end  
  palindrome   
 end  
 ```

 
