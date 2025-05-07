Compute the **shortest weighted path** in a graph defined by `strArr`.

---

### 🧠 Problem Summary

* Input: `strArr`, an array where:

  * First element is number of nodes `n`
  * Next `n` elements are node names
  * Remaining elements are weighted edges in form `"A|B|3"` → edge between `A` and `B` with weight `3`

* Output: Shortest path **from the first node to the last node**, formatted like `"A-B-C"`. If no path, return `"-1"`.

---

### ✅ Strategy

We’ll use **Dijkstra’s Algorithm**, which is perfect for finding shortest paths in a weighted graph with non-negative weights.

---

### 🐍 Python Solution

```python
import heapq
from collections import defaultdict

def WeightedPath(strArr):
    n = int(strArr[0])
    nodes = strArr[1:n+1]
    edges = strArr[n+1:]

    graph = defaultdict(list)
    
    # Build the graph
    for edge in edges:
        u, v, w = edge.split('|')
        w = int(w)
        graph[u].append((v, w))
        graph[v].append((u, w))  # bidirectional

    start = nodes[0]
    end = nodes[-1]

    # Dijkstra's algorithm
    heap = [(0, start, [start])]  # (cost, current_node, path)
    visited = set()

    while heap:
        cost, current, path = heapq.heappop(heap)

        if current == end:
            return '-'.join(path)

        if current in visited:
            continue
        visited.add(current)

        for neighbor, weight in graph[current]:
            if neighbor not in visited:
                heapq.heappush(heap, (cost + weight, neighbor, path + [neighbor]))

    return "-1"

# Example usage
print(WeightedPath(["4","A","B","C","D","A|B|2","C|B|11","B|D|2"]))  # Output: A-B-D
```

---

### 🚀 How It Works

* We use a **min-heap** to always expand the path with the lowest total weight.
* The heap stores tuples of `(current total weight, current node, path so far)`.
* When we reach the destination node, we return the path.
* If no path exists, we return `"-1"`.

---


