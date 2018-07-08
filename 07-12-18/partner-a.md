# Partner A 

## Basically Steve Jobs

Tell me about a time when you had to use your presentation skills to influence someone's opinion.

## Alien Language

Given a sorted dictionary (array of words) of an alien language, find the order of the characters in the language.

### Example
```
Input:  words = ["baa", "abcd", "abca", "cab", "cad"]
Output: 'b', 'd', 'a', 'c'
```
Note that words are sorted and in the given language "baa" comes before "abcd", therefore 'b' is before 'a' in output. Similarly, we can find other orders:
```
Input:  words = ["caa", "aaa", "aab"]
Output: 'c', 'a', 'b'

### Solution

We can solve this problem by creating vertices of the characters, then finding the topological sorting of the vertices.

* Create a number of vertices equal to the size of alphabet in the given alien language. For example, if the alphabet size is 5, then there can be 5 characters in words. 

* For every pair of adjacent words in given sorted array:
  * Let the current pair of words be word1 and word2. One by one compare characters of both words and find the first mismatching characters.
  * Create an edge from the mismatching character of word1 to that of word2.
* Print the topological sorting of the vertices.

```ruby
def alien_letter_order(words)
  vertices = {}
  
  words.reduce(:+).split('').uniq.each do |letter|
    vertices[letter] = Vertex.new(letter)
  end
  
  (0...words.length).each do |i|
    word1, word2 = words[i], words[i + 1]
    smaller = word1.length < word2.length ? word1.length : word2.length
    
    (0...smaller).each do |j|
      if word1[j] != word2[j]
        Edge.new(vertices[word1[j]], vertices[word2[j]])
        break
      end
    end
  end
  
  topological_sort(vertices.values).map { |v| v.value }
end
```

### Discuss:
* What are the time and space complexities of this method?

### Credit:
* Adapted from [this](https://www.geeksforgeeks.org/given-sorted-dictionary-find-precedence-characters/) Geeks for Geeks problem.
