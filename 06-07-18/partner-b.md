# Partner B

## Behavioral Questions

* Tell me about yourself by walking me through your resume.
* Give me an example of when you took an unpopular stance in a meeting with peers and your leader and you were the outlier. What was it, why did you feel strongly about it, and what did you do?

## The Lonely Island

* This problem is a very [common interview question](https://www.glassdoor.com/Interview/Find-Island-in-matrix-QTN_2143992.htm).
* Solution taken from [Geeks for Geeks](http://www.geeksforgeeks.org/find-number-of-islands/)

Given a boolean 2D matrix, find the number of islands. A group of connected `true`s forms an island. For example, the below matrix contains 5 islands.

```
Input : mat = [[T, T, F, F, F],
                   [F, T, F, F, T],
                   [T, F, F, T, T],
                   [F, F, F, F, F],
                   [T, F, T, F, T]]
Output : 5
```

### Solution

This problem can be solved by applying Depth First Search (DFS) on each component. 
In each DFS call, a component or a sub-graph is visited. We will call DFS
on the next un-visited component. The number of DFS gives the number of connected
components.

A cell in 2D matrix can potentially be connected to 8 neighbors. Unlike standard
DFS, where we recursively call for all adjacent vertices, here we can recursively
call for 8 neighbors. We keep track of visited componentss so that they are 
not visited again.


```ruby
# 
# In order to get neighbor coordinates:
#
# [x - 1, y - 1], [x - 1, y], [x - 1, y + 1]
# [x, y - 1]    ,   SELF    , [x, y + 1]
# [x + 1, y - 1], [x + 1, y], [x + 1, y + 1]


def count_islands(matrix)
  rows = matrix.length
  cols = matrix[0].length
  visited = Array.new(rows) { Array.new(cols) }

  # Initialize count as 0 and traverse through all 
  # cells of the given matrix 
  count = 0 
  (0...rows).each do |row|
    (0...cols).each do |col|

      # If a cell with a true value is not visited yet,
      # then new island is found
      if !visited[row][col] && matrix[row][col] 
        # Visit all cells in this island
        # increment island count

        visit_island(row, col, visited, matrix)
        count += 1
      end
    end
  end

  count 
end

def visit_island(row, col, visited, matrix)
  neighbor_row = [-1, -1, -1, 0, 0, 1, 1, 1]
  neighbor_col = [-1, 0, 1, -1, 1, -1, 0, 1]

  visited[row][col] = true 

  (0...8).each do |idx|
    if is_island(row + neighbor_row[idx], col + neighbor_col[idx], visited, matrix)
      visit_island(row + neighbor_row[idx], col + neighbor_col[idx], visited, matrix)
    end
  end
end

def is_island(row, col, visited, matrix)
  return (row >= 0 && row < matrix.length) && (col >= 0 && col < matrix[0].length) && (matrix[row][col] && !visited[row][col])
end

```

Time complexity: O(row x col)
