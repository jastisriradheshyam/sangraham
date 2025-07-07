+++
title = 'Graphs and Tress Representation'
date = 2025-07-07T07:46:43.416Z
draft = false
description = 'List of Graphs and Tress Representation'
+++

# Trees

## Parent Child Pointers

- Each node stores a reference to its child nodes
- Common in binary trees

```python
class Node:
    def __init__(self, value):
        self.val = value
        self.left = None
        self.right = None
```

```go
type Node struct {
    Val int
    Left *Node
    Right *Node
}

func GetNode(val int) *Node {
    var node *Node
    node = new(Node)
    node.Val = val
    node.Left = nil
    node.Right = nil
    return node
}
```

## Array Representation (Binary trees)

- Tree nodes stored in an array where:
  - Node at index `i` has children at `2i+1` and `2i+2`
- Common for heaps

```python
tree = [10,20,30,40,50,60]
```

```go
tree := []int{10,20,30,40,50,60}
```

## Adjacency List

- For general trees, each node maps to a list of its children

```python
tree = {
    'A': ['B','C']
    'B': ['D','E']
    'C': ['F']
}
```

```go
tree = map[rune][]rune{
    'A': {'B','C'}
    'B': {'D','E'}
    'C': {'F'}
}
```

## Adjacency set

- Faster lookup when checking if an edge exists.
- basically map of maps

```python
tree = {
    'A': {'B','C'},
    'B': {'D'},
    'C': {}
}
```

```go
tree map[rune]map[rune]interface{}{
	'A': {'B': struct{}{},'C':struct{}{}},
    'B': {'D':struct{}{}},
    'C': {}
}
```

# Graphs

## Adjacency List

- Most space-efficient for sparse graphs
- stores each node and a list of its adjacent nodes

```python
graph = {
    'A':['B','C'],
    'B':['A','D'],
    'C':['A','D'],
    'D':['B','C']
}
```

```go
graph := map[rune][]rune{
    'A':{'B','C'},
    'B':{'A','D'},
    'C':{'A','D'},
    'D':{'B','C'},
}
```

## Adjacency set

- Faster lookup when checking if an edge exists.
- basically map of maps

```python
graph = {
    'A': {'B','C'},
    'B': {'A','D'},
    'C': {'A'}
    'D': {'B'}
}
```

```go
graph map[rune]map[rune]interface{}{
	'A': {'B': struct{}{},'C':struct{}{}},
    'B': {'A': struct{}{},'D':struct{}{}},
    'C': {'A':struct{}{}},
    'D': {'B':struct{}{}},
}
```

## Adjacency matrix

- Great for dense graphs
- 2D matrix where `matrix[i][j] = 1` (or weight) means edge from `i` to `j`.

```python
matrix = [
    [0,1,1,0],
    [1,0,0,1],
    [1,0,0,1],
    [0,1,1,0]
]
```

```go
matrix = [][]int{
    {0,1,1,0},
    {1,0,0,1},
    {1,0,0,1},
    {0,1,1,0}
}
```

## Edge List

- List of all edges
- Useful for algorithms like Kruskal's (minimum spanning tree)

```python
edges = [
    ('A','B'),
    ('A','C'),
    ('B','D'),
    ('C','D'),
]
```

```go
edges := [][]rune{
    {'A','B'},
    {'A','C'},
    {'B','D'},
    {'C','D'},
}
```

## Hash Maps of Hash Maps (Weighted Graphs)

- Ideal for representing weights between edges
- inner dictionaries/maps store neighbors and corresponding weights

```python
graph = {
    'A': {'B': 3, 'C': 1},
    'B': {'C': 7},
    'C': {}
}
```

```go
graph := map[rune]map[rune]interface{}{
	'A': {'B': struct{}{},'C':struct{}{}},
    'B': {'A': struct{}{},'D':struct{}{}},
    'C': {'A':struct{}{}},
}
```