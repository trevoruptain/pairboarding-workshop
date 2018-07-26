# Partner A

NB: Today's pairboarding session focuses on refreshing the skills you learned during the job search. If you feel as if you have mastered topological sort, try solving some medium/hard [LeetCode](https://leetcode.com/problemset/all/?topicSlugs=graph) problems related to graphs.

## Playing Nice

Do you do your best work alone or in a group?  Does the type of work matter?

## Kahn's Algorithm

Implement topological sort using Kahn's algorithm. Assume the following setup:

```ruby
class Vertex
  attr_reader :value, :in_edges, :out_edges

  def initialize(value)
    @value, @in_edges, @out_edges = value, [], []
  end
end

class Edge
  attr_reader :to_vertex, :from_vertex, :cost

  def initialize(from_vertex, to_vertex, cost = 1)
    self.from_vertex = from_vertex
    self.to_vertex = to_vertex
    self.cost = cost

    to_vertex.in_edges << self
    from_vertex.out_edges << self
  end

  def destroy!
    self.to_vertex.in_edges.delete(self)
    self.to_vertex = nil
    self.from_vertex.out_edges.delete(self)
    self.from_vertex = nil
  end

  protected
  attr_writer :from_vertex, :to_vertex, :cost
end
```

If your partner needs a hint, you can walk them through the following steps:

* Determine the in-edge count of each node.
* Collect nodes with zero in-edge count in a queue.
* While the queue is not empty:
  - Pop node `u` from queue,
  - remove `u` from the graph (depending on your implementation, this may or may not involve the `destroy!` method; what are the complications to destroying as we loop? What is another way we can track the number of `in_edges`?),
  - check if there is a new node with in-degree zero (among the neighbors of `u`)
  - If yes, put that node into the queue.
  - We maintain a list that records in which order the nodes are removed.
* If the queue is empty:
  - if we removed all nodes from the graph, return the list
  - else we return an empty list that indicates that an order is not possible due to a cycle
  
### Solution

```ruby
def topological_sort(vertices)
  in_edge_counts = {}
  queue = []

  vertices.each do |v|
    in_edge_counts[v] = v.in_edges.count
    queue << v if v.in_edges.empty?
  end

  sorted_vertices = []

  until queue.empty?
    vertex = queue.shift
    sorted_vertices << vertex

    vertex.out_edges.each do |e|
      to_vertex = e.to_vertex

      in_edge_counts[to_vertex] -= 1
      queue << to_vertex if in_edge_counts[to_vertex] == 0
    end
  end

  sorted_vertices
end
```
