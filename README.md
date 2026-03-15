# ExpNo 2: Implement Depth First Search Traversal of a Graph

### Name:VARUN A
### Register Number:212224240178

---

## Aim

To Implement **Depth First Search Traversal** of a Graph using Python 3.

---

## Theory

**Depth First Traversal** (or **DFS**) for a graph is similar to Depth First Traversal of a tree. The key difference is that graphs may contain **cycles** (a node may be visited twice). To prevent this, a **Boolean visited array** (or set) is used to avoid processing a node more than once. A graph can have more than one DFS traversal depending on the starting node and the order in which adjacent nodes are explored.

Depth-first search is an algorithm for traversing or searching trees or graph data structures. The algorithm starts at the root node (selecting an arbitrary starting node in the case of a graph) and explores **as far as possible** along each branch before **backtracking**. 

### DFS Traversal Steps Example:

* **Step 1:** Initially, the **stack** and **visited** arrays are empty.
    ![Initial state of DFS showing an empty stack and visited array](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/640b3c6f-3ac1-49a2-a955-68da9a71f446)

* **Step 2:** Visit **Node 0** and put its adjacent nodes which are not visited yet into the stack.
    ![DFS Step 2: Node 0 is visited and its neighbors 1, 2, and 3 are pushed onto the stack](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/86dcf7d9-1f9d-49b0-a821-5976a6e77606)

* **Step 3:** **Node 1** is at the top of the stack. Visit node 1, pop it from the stack, and put all of its adjacent unvisited nodes into the stack.
    ![DFS Step 3: Node 1 is visited and popped from the stack](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/e6017942-08b1-4742-87ad-c97eb97bf985)

* **Step 4:** **Node 2** is at the top of the stack. Visit node 2, pop it, and put all of its unvisited adjacent nodes (**3, 4**) into the stack.
    ![DFS Step 4: Node 2 is visited and neighbors 3 and 4 are added to the stack](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/6e6d123c-60ae-4f9c-a27c-c4fc7e57d57c)

* **Step 5:** **Node 4** is at the top of the stack. Visit node 4, pop it, and put all of its adjacent unvisited nodes in the stack (none in this example).
    ![DFS Step 5: Node 4 is visited and popped from the stack](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/20b76a05-5668-4da5-8189-e10fb1bb7238)

* **Step 6:** **Node 3** is at the top of the stack. Visit node 3, pop it, and put all of its adjacent unvisited nodes in the stack (none in this example).
    ![DFS Step 6: Node 3 is visited and popped from the stack](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/3b88f04a-7846-4f75-89b4-22bbd5b48e52)

The Stack becomes empty, which means all nodes have been visited, and the DFS traversal ends.

---

## Algorithm

1.  Construct a **Graph** with Nodes and Edges (typically using an **Adjacency List**).
2.  Depth First Search uses a **Stack** (either an explicit data structure or the **implicit call stack** via **Recursion**).
3.  Insert a **START node** to the STACK (or call the recursive function with the start node).
4.  Find its **Successors or neighbors** and check whether the node is **visited** or not.
5.  If **Not Visited**, add it to the STACK/call the function recursively.
6.  Else, **Backtrack** or continue the process until no more nodes need to be visited.

---

## Program:

The following Python code implements the DFS algorithm using a recursive approach (utilizing the function call stack).

```python
from collections import defaultdict

class Graph:
    def __init__(self):
        # Defaultdict to store graph as an Adjacency List
        self.graph = defaultdict(list)

    # Function to add an edge to graph
    def addEdge(self, u, v):
        self.graph[u].append(v)
        # For an undirected graph, add the reverse edge too
        # self.graph[v].append(u) 

    # Recursive function for DFS traversal
    def DFS_util(self, v, visited, traversal_order):
        # Mark the current node as visited and add it to the traversal list
        visited.add(v)
        traversal_order.append(str(v))

        # Recur for all the neighbors of this vertex
        # Sort keys/neighbors if a specific traversal order is desired (optional)
        for neighbor in sorted(self.graph[v]):
            if neighbor not in visited:
                self.DFS_util(neighbor, visited, traversal_order)

    # Main DFS function 
    def DFS(self, start_node):
        visited = set()
        traversal_order = []
        
        # Call the recursive helper function 
        self.DFS_util(start_node, visited, traversal_order)
        return traversal_order

# --- Example Usage 1 ---
print("--- Example 1 ---")
g1 = Graph()
# Adding edges based on Sample Input 1 (A B, A C, B E, C D, B D, C G, D F, G F, F H)
g1.addEdge('A', 'B') 
g1.addEdge('A', 'C') 
g1.addEdge('B', 'E')
g1.addEdge('C', 'D')
g1.addEdge('B', 'D')
g1.addEdge('C', 'G')
g1.addEdge('D', 'F')
g1.addEdge('G', 'F')
g1.addEdge('F', 'H')

# Assuming all edges are directed for simplicity, but often DFS is used on undirected.
# For undirected, we'd add g1.addEdge('B', 'A'), etc. 

# Run DFS starting from node 'A'
dfs_result_1 = g1.DFS('A')
print("DFS Traversal from 'A':")
print(dfs_result_1)


# --- Example Usage 2 ---
print("\n--- Example 2 ---")
g2 = Graph()
# Adding edges based on Sample Input 2 (0 1, 0 2, 0 3, 2 3, 2 4)
g2.addEdge('0', '1') 
g2.addEdge('0', '2') 
g2.addEdge('0', '3')
g2.addEdge('2', '3')
g2.addEdge('2', '4')

# Run DFS starting from node '0'
dfs_result_2 = g2.DFS('0')
print("DFS Traversal from '0':")
print(dfs_result_2)
```


<hr>
<h3>Sample Input</h3>
<hr>
8 9 <BR>
A B <BR>
A C <BR>
B E <BR>
C D <BR>
B D <BR>
C G <BR>
D F <BR>
G F <BR>
F H <BR>
<hr>
<h3>Sample Output</h3>
<hr>
['A', 'B', 'E', 'D', 'C', 'G', 'F', 'H']

![alt text](image-1.png)<hr>

<hr>
<h3>Sample Input</h3>
<hr>

5 5 <BR>
0 1 <BR>
0 2 <BR>
0 3 <BR>
2 3 <BR>
2 4 <BR>
<hr>
<h3>Sample Output</h3>
<hr>
['0', '1', '2', '3', '4']

![alt text](image.png)

<hr>
<h3>Result:</h3>
<hr>
<p>Thus,a Graph was constructed and implementation of Depth First Search for the same graph was done successfully.</p>
