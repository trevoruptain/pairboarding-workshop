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
```

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

## Making the Switch

You’re in a room with three light switches, each of which controls one of three light bulbs in the next room. You need to determine which switch controls which bulb. All lights are off to begin, and you can’t see into one room from the other. You can inspect the other room only once. How can you find out which switches are connected to which bulbs? 

### Solution

Let’s call the switches 1, 2, and 3.

Leave switch 1 off.

Turn switch 2 on for ten minutes.

Now turn it off and quickly turn on switch 3.

Go into the room and inspect…

The bulb that is still warm but not lit up is controlled by switch 2. The one that’s currently lit up is switch 3. The last one is switch 1.

## Frenemies

You’re about to get on a plane to Seattle. You want to know if it’s raining. You call 3 random friends who live there and ask each if it’s raining. Each friend has a 2/3 chance of telling you the truth and a 1/3 chance of messing with you by lying. All 3 friends tell you that “Yes” it is raining. What is the probability that it’s actually raining in Seattle? 

### Solution

You only need 1 of your friends to be telling the truth for it to be raining in Seattle.

It’s fastest just to calculate the odds that all 3 are lying, and it’s not raining.

Each friend has a 1/3 chance of lying. Multiply the odds together… you get 1/27 (1/3 * 1/3 * 1/3).

We’re not done yet though… 1/27 is the probability that all 3 friends lied at the same time.

The probability that at least 1 told you the truth? 26/27 or around a 96% that it’s raining in Seattle.

## Credit

Trivia questions taken from [this article](https://careersidekick.com/brain-teaser-job-interview-questions-facebook-google-apple/)
