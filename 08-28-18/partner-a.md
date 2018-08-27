## Problem:
### Given a string that includes curly braces containing a set of |pipe| separated options, select one of those options at random from the set, and replace the set in the string with the option selected. ###
For example:
  - input:
    - ```"test string. option {1|2|3}"```
  - output (any one of the following):
    - ```"test string. option 1"```
    - ```"test string. option 2"```
    - ```"test string. option 3"```

note:
  - Input strings will always be well formed.
  - Options can be empty strings.

also, sets can be nested to any depth. For example:
  - input:
    - ``"--{A: {1|2|3||={100|200}=} :A| b: {4|5|6}} :b --"``
  - output (any one of the following):
    - `"--A: 1 :A--"`
    - `"--A: 2 :A--"`
    - `"--A: 3 :A--"`
    - `"--A:  :A--"`
    - `"--A: =100= :A--"`
    - `"--A: =200= :A--"`
    - `"-- b: 4 :b --"`
    - `"-- b: 5 :b --"`
    - `"-- b: 6 :b --"`

## Solution

``` ruby
test = "{1|2} and {7|3|4} test:{{ 1| {3|4|5}| 6}| num}"
test_2 = "1:{a|b|c|d} 2:{e 3:{f|g} 4:{h|i}|{j{{|||{|||}}}|k|l} 3:m 4:{n|o|p}}"

def resolve_option(string, start_idx)
  options = []
  string[start_idx] = "|"
  curr_idx = start_idx
  while string[curr_idx] != "}"
    curr_char = string[curr_idx]
    if curr_char == "|"
      options.push("")
    elsif curr_char == "{"
      string = resolve_option(string, curr_idx)
      next
    else
      options[-1] += curr_char
    end
    curr_idx += 1
  end
  string[start_idx..curr_idx] = options.sample
  string
end

def resolve_string(string)
  new_string = string.dup
  curr_idx = 0
  while curr_idx < new_string.length
    if new_string[curr_idx] == "{"
      new_string = resolve_option(new_string, curr_idx)
    else
      curr_idx += 1
    end
  end
  new_string
end

puts "test: '#{test}'"
puts "  #{resolve_string(test)}"
puts "  #{resolve_string(test)}"
puts "  #{resolve_string(test)}"
puts "  #{resolve_string(test)}"
puts "  #{resolve_string(test)}\n\n"

puts "test_2: '#{test_2}'"
puts "  #{resolve_string(test_2)}"
puts "  #{resolve_string(test_2)}"
puts "  #{resolve_string(test_2)}"
puts "  #{resolve_string(test_2)}"
puts "  #{resolve_string(test_2)}"
```
