# Graphs

When you hear the word "graph," you might visualize bar graphs or pie graphs or a similar visual figure in statistics and infographics.  Perhaps you think of graphs of functions from mathematics, like the graph of a basic parabola such as $y = x^2$.  In computer science, graphs take on a different meaning.  

A **graph** in computer sciences is an abstract data structure represented by a bunch of vertexes and edges.  A *vertex* or *node* is a data container.  It could hold strings, numbers or any other data that you may deem fit.  An *edge* or *link* is a connection from one vertex to another.

Graphs can be undirected or directed.  An *undirected graph* is depicted with edges that do not have a direction indicated in any way, shape or form; vertexes are connected by simple lines.  A *directed graph* contains edges that point in one or both directions between two nodes. 

Here is a visual of an *undirected graph* (Example 1):
```
                     *****
                     * C *
                     *****
                    /
                   /
                  /
*****        *****
* A *--------* B *
*****        *****
                  \ 
                   \
                    \
                     *****
                     * D *
                     *****
```
Notice that there is no direction specified in this graph.

Here is a *directed graph* (Example 2):
```
                     *****
                     * C *
                     *****
                    --
                    /|
                   /
                  /
*****        *****
* A *------->* B *
*****        *****__
                 |\ 
                   \
                   _\|
                     *****
                     * D *
                     *****
```
Notice how A points to B, B points to C, and B and D point to each other.

A **weighted graph** is a graph where each edge has a value, or weight, assigned to it.  For example, an edge might represent a distance between two cities.

Here is an undirected weighted graph (Example 3):
```
                     *****
                     * C *
                     *****
                    /
                   / 5
                  /
*****   10   *****
* A *--------* B *
*****        *****
                  \ 
                   \ 3
                    \
                     *****
                     * D *
                     *****
```
Graphs have tons of applications!  When you're trying to find the fastest or shortest way to get to your destination via GPS or a map application, a graph is traversed to determine your route.  If you want to see who's following you and who you're following in social media, a graphic depiction comes in handy.

## Representations of a graph
Unfortunately, graphs are not an inherent data structure in most, if not all, languages because there are many ways to define and implement them.  Two popular ways to define a graph are through adjacency lists and adjacency matrices.

An **adjacency list** is a collection of unordered lists, where each list contains the nodes that are adjacent to a specific one.  There are several ways to represent an adjacency list: through classes, through linked lists, through arrays, or through maps.  For this section, we'll use maps to represent adjacency lists.  In an undirected graph, such as in example 1, the list would look like this:
```
{
    "A": ["B"],
    "B": ["A","C","D"],
    "C": ["B"],
    "D": ["B"]
}
```
For example, node B is adjacent to nodes A, C, and D, while node C is only adjacent to node B.  You can use a set to represent the nodes linked.

Now for a directed graph, like in example 2, the adjacency list might look like this:
```
{
    "A": ["B"],
    "B": ["C","D"],
    "C": [],
    "D": ["B"]
}
```
Notice how C does not point to any nodes.  Each list/set only contains the nodes that the current node can travel to next; for example node A can travel to node B, but node B cannot travel back to node A.

For a weighted graph - whether it's directed or not, you have to not only save the nodes adjacent to each one, but also the weights as well.  
One representation for the adjacency list in example 3 is this:
```
{
    "A": [("B",10)],
    "B": [("A",10),("C",5),("D",3)],
    "C": [("B",5)],
    "D": [("B",3)]
}
```
Notice how each entry now consists not only of the node, but the weight itself.  For example, going from A to B has a weight of 10.  The nodes and weights paired together can be saved as arrays, maps or a different data structure.

Another way to create a graph is through an adjacency matrix.  An **adjacency matrix** is a 2-D array (or matrix) containing the connections between all nodes.  In the graph in Example 1, it would look like this:
```
x = [[0,1,0,0], // Rows represent connections *from* a node; in this row it means nodes coming from A
     [1,0,1,1], // Nodes from B
     [0,1,0,0], // Nodes from C
     [0,1,0,0]] // Nodes from D
      A B C D <--- Columns denote connections to that node, so the first column is all connections to node A
```
Here's a mathematical representation:
$$
\begin{bmatrix}
0 & 1 & 0 & 0\\
1 & 0 & 1 & 1\\
0 & 1 & 0 & 0\\
0 & 1 & 0 & 0\\
\end{bmatrix}
$$
Each row in the adjacency matrix denotes all the possible connections *from* a specific node, and each column represents all the connections *to* a specific node.  Using zero-indexing, `x[0]` is a subarray denoting all the nodes coming from "A", `x[1]` means all the nodes from "B", and so on.  Now each of these subarrays, like `[0,1,0,0]` for `x[0]`, has a value of either 0 or 1, where 0 means no connection and 1 means there is a connection.  (You can use alternate values instead, but these are probably the most intuitive to use.)  Each entry in the subarray means a connection to nodes A, B, C, and D, respectively, for a subarray like `[0,1,0,0]`.  This means for `x[0]`, i.e. node "A", the values `[0,1,0,0]` mean there is no connection from A to A itself, there *is* a connection from A to B, no connection from A to C, and no connection from A to D.  

Think of `x[row][col]` as `x["starting node"]["ending node"]`, and if `x["starting node"]["ending node"]` is 0, there is no connection, but if `x["starting node"]["ending node"]` is 1, we have one.  Note that when you use arrays, numerical indexes are used, so beware.  For example, `x[2][1]` equaling 1 means we have a connection from node C (the row with index 2) to node B (the column with index 1).

For a *weighted* graph, instead of using 1, you can use the weights instead.  The graph in Example 3 would have an adjacency matrix like this:
```
x = [[0,10,0,0],
     [10,0,5,3],
     [0,5,0,0],
     [0,3,0,0]]
```
For undirected graphs, adjacency matrices are symmetric about the diagonal.  (A diagonal in a square matrix [equal rows and columns] is defined as the line of values from the top left to the bottom right.)  For directed graphs, some connections will not be two-way, i.e. node 1 could connect to node 2, but node 2 cannot travel to node 1, and weights would be represented appropriately.

An adjacency list is best if you do not have a bunch of connections and the graph is sparse.  However, if you have a ton of connections and nodes and the graph itself is rather dense, an adjacency matrix is best.  Also consider memory and time tradeoffs when using one representation vs. another.  For example, you have $O(N^2)$ space for a graph with $N$ nodes if you use an adjacency matrix, but you might not need as much in an adjacency list.

## Traversing a graph
Traveling through a graph can be messy if you don't have a strategy in mind.  You might prioritize findest the shortest route in terms of distance between two locations.  Maybe you prefer the fastest time, even if it isn't the shortest distance.  Keep your goal in mind, and it'll help you determine which way to traverse a graph.

Two common techniques for going through a graph from one node to another are breadth-first search and depth-first search.

**Breadth-first search (BFS)** prioritizes through the nodes in each level before traveling to the next one.  For example, given the following graph (Example 4):
```
      A----             Level 1
     / \   \
    B   C---D           Level 2
   / \   \
  E   F   G             Level 3
          |
          H             Level 4
```
If we start at A, we then examine all the nodes adjacent to it in the next level, so B, C, and D.  Then we move on to the next set of nodes afterwards adjacent to those that we haven't visited yet, so E, F, and G.  H is visited last in the final level.

To facilitate traveling through the nodes through breadth-first search (BFS), a queue is usually used to hold the next nodes to visit.  New nodes are added to the back of the queue, while the oldest nodes are removed.  Note that we must keep track of which nodes have been visited already to prevent the possibility of an infinite loop due to going on a circular path where we revisit a node - i.e., a cycle.  (We'll cover cycles in the next section!)  You can track which nodes were visited by using a set or an array or a similar data structure to help you mark the nodes you've seen already so that we don't add them to the queue again.  

BFS starts off with one node, which is loaded into the queue to start.  Then we travel through the queue, removing the oldest node, which we'll call X, each time.  Then for each node adjacent to X that we have NOT visited yet, add those to the queue.  Once they're enqueued, mark node X as visited.  Repeat the process until the queue is empty.  (The pseudocode is left out to help you think through how to write the code yourself!)

**Depth-first search (DFS)** starts at one node, and then we go through each adjacent node, traveling down as far as we can before moving on to the next adjacent node (if applicable).  In example 4, we start at A, and then we travel down to B, and then travel down to E, then backtrack to B to go to F, then backtrack to B and back to A.  Then we go from A to C and repeat the process.

To enable us to travel down the graph, we use a stack.  The newest node is pushed to the top of the stack, and then we keep adding to the top of the stack as long as we can.  Once we reach the end, then we pop nodes off as we backtrack and then travel to adjacent nodes.  Note that like in BFS, DFS tracks the nodes we've visited so we don't risk an infinite loop.  

DFS starts at a specific node, which is added to the stack and marked as visited.  Then we pick a node adjacent to it, and then push that to the stack.  We repeat the process until we cannot proceed any farther, so then we backtrack and pop nodes off.  We continue to push and pop nodes until the stack is fully empty.

DFS can also be accomplished by using recursion, although you must be careful in that you don't want to risk stack overflow due to the call stack becoming too large.

Note that picking which note to travel to and push to the stack - or call via recursion - will depend on the graph itself.  If it's a weighted graph, you might want to pick the adjacent node with the least or most weight.  If it's unweighted, it might not matter as much which node to travel to first.

Both BFS and DFS enable you to travel down a graph.  When to use each of them depends on the problem in question, and in many cases it won't matter which one to use.  However, sometimes one will be better than the other.  For example, if your priority is to locate a specific node as quickly as possible from the starting point, depth-first search (DFS) will usually be better.  If you want to visit adjacent spots as quickly as you can first before moving deeper into the graph, breadth-first search (BFS) will likely be superior.  BFS is more useful for shortest-distance problems.

DFS prioritizes paths, while BFS prioritizes levels.  BFS will be better for unweighted graphs, while DFS is best for weighted graphs.

## Cycles and detecting them
When you have a graph, it's often useful to find cycles.  A **cycle** is a path of nodes in which only the first and last nodes are the same, and no other nodes are duplicated.  Cycles can be detected in directed and undirected graphs.  (A **circuit** is like a cycle in that the first and last nodes are the same with at least one edge visited, but other nodes can be duplicated, including the starting/ending node.)

Here are some examples of cycles:
```
Directed graph with A-B-C-D-A:
A -> B
^    |
|    v
D <- C

Undirected graph with B-C-D-A-B (or any 
vertex as a starting point in this case):
A----B----C
\         |
 \________D
```
Cycles are important to detect because you don't want to have an algorithm run infinitely.  For example, when modeling traffic, you usually don't want cars traveling in circles.  On the other hand, you might be a pedestrian planning a run that circles multiple neighborhoods.  In networks you don't want a cycle because you don't want data structure or power being rerouted forever.

There are multiple approaches to detecting graphs.  Let's break down three methods you can use.  (There's a fourth called the Bellman-Ford algorithm, but that will be covered in the next section on finding the shortest path.)

### Method I: Depth-first search
The most common strategy is to utilize depth-first search (DFS).  With DFS you can build a stack - or use a call stack via recursion - holding the nodes you've visited so far.  Once you encounter a node that's already in the stack, you have detected a cycle.  

You can use DFS for directed and undirected graphs.  However, if you do so for an undirected graph, be careful!  You must keep track of what your parent - or last - node is so that you don't accidentally revisit it.  For a directed graph, we have to check if the next node in line has already been visited at some point along the path; you don't need to worry about the parent node.

You might consider using a set to keep track of the nodes you've visited.  Just make sure in depth-first search to remove nodes when backtracking.

### Method II: Union-find
Another method used to detect cycles is the union-find technique.  The **union-find technique** for *undirected* graphs starts by putting each node into its own set.  Then we examine each edge and if the two connected nodes are in different sets, merge them into a new set.  For example, if nodes A and B are in one set and C and D are in another, and you're examining the edge connecting B and C, then the two sets are merged into a new set containing A, B, C, and D.  If there is an edge where the two nodes are in the same set, then a cycle is detected.  But if after inspecting each edge there is a single set remaining, then there is no cycle.

The union-find technique uses a disjoint-set data structure - also called a "union-find data structure".  It's often used to determine if two elements belong in the same set or two separate sets.  Merging two sets is very efficient, as is checking if an element belongs.  Note that an element can only belong in one set.

Note that weights in the graph are ignored.  To repeat: the union-find technique works for undirected graphs, weighted or unweighted.

### Method III: Topological sort
Yet another way we can detect if a cycle exists is by attempting a topological sort for the graph if it is a directed graph.  A **topological sort** for a *directed* graph, weighted or unweighted, puts the nodes in order in such a way so that for each edge connecting from node $X$ to node $Y$, $X$ comes before $Y$.  In example 2, two possible topological sorts are `A, B, C, D` or `A, B, D, C`.  A couple of strategies for a topological sort are Kahn's algorithm and depth-first search.

Now if there is a cycle for the directed graph, there is no topological sort.  Weights are ignored.

Depending on the implementation, you might use a stack, set and/or queue.

### Summary of methods
The most general approach for detecting a cycle is with depth-first search (DFS), which works for any graph type.  The union-find technique works for undirected graphs, and if there are weights, they're not considered.  Topological sorting works for a directed graph, regardless of if there are weights or not.

If you need to consider negative cycles, i.e., cycles where the sum of the weights is negative, then use the Bellman-Ford algorithm, which will be described in the next section.

## Shortest path
When you need to find the shortest path between two nodes - or for all pairs of nodes, there are many algorithms out there.  The graph's type - weighted (including possibly negative weights) vs. unweighted and directed vs. undirected - and the goal of the problem play a major role in determining which algorithm works best.  

### Dijkstra's algorithm
One algorithm that's popular for weighted graphs - whether directed or not - is Dijkstra's algorithm.  **Dijkstra's algorithm** is used to calculate the shortest distance to all nodes from a specific one.  This kind of problem is a Single-Source Shortest Path (SSSP) algorithm.

The algorithm requires two data structures: a priority queue where the smallest value is the one to be popped first and a set to hold all the nodes we have not visited yet.

The graph cannot have negative weights.  If you need to consider negative weights, use the Bellman-Ford algorithm, which will be described in the next subsection.

The algorithm works like this:
1. Assign starting distance values for each node.  The starting node will have a distance of 0, and the remaining nodes will start with a value of infinity.  These values can be saved in an array, a map or any data structure you see fit.
2. Load the starting node into a priority queue.  Each entry in the priority queue will hold a node and its currently calculated distance to the starting node.  Initially each of these distances will be infinity.
3. Initial an empty set holding the nodes you've visited.
4. While the priority queue is not empty:
    - Grab the node `X` with the smallest overall distance from the starting point.
    - Save this new node `X` to the set of nodes visited so you don't go through it again.
    - Calculate the overall distance from the starting node through node `X` to each neighbor using the edge weight connecting it to `X`.  If this value is smaller than the saved distance for that neighbor, update it accordingly and change that node's priority value.  (Some languages, like Python, do not support changing priority natively, so you might have to implement lazy insertions, removing outdated entries as you remove from the queue.)
5. Return the distances from each node to the current one.

It is possible to save the paths holding the minimum distances from the starting node to the remaining nodes in the graph.  

Be careful if you're using an adjacency matrix vs. an adjacency list, as this choice will affect operations.

### Bellman-Ford algorithm
If you have negative weights in your graph (directed or not), then Dijkstra's algorithm will not work.  The **Bellman-Ford algorithm** (or Bellman-Ford-Moore) is used to find the shortest path from one node to each of the other nodes in a graph where negative weights are possible.  It is also an algorithm for finding the solution to an SSSP.

Here's how Bellman-Ford works:
1. Assign starting distance values for each node.  The starting node will have a distance of 0, and the remaining nodes will start with a value of infinity.  These values can be saved in an array, a map or any data structure you see fit.
2. Loop $n - 1$ times, where $n$ is the number of vertices (nodes) in the graph:
    - Loop through *each* edge in the graph:
        - If the calculated distance from the source to node $i$ + edge weight between nodes $i$ and $j$ < calculated distance from the source to node $j$, then update the distance from the source to node $j$.
3. Check for a negative cycle.  At this point, we go through each edge again, and if the calculated distance from the source to node $i$ + edge weight between nodes $i$ and $j$ < calculated distance from the source to node $j$, then there is a negative cycle because you can then always decrease the distances infinitely.  Note that if we don't have a negative cycle, no distances should change at all at this point; in other words the distances are optimized already.

**IMPORTANT:** To reiterate, if you have a negative cycle, i.e. adding the weights for at least one path that starts and ends at the same node results in a negative sum, this algorithm will NOT work because there is no optimal shortest path as the weight will trend to negative infinity.

We only need to loop $n - 1$ times because a graph with $n$ vertexes has at most $n - 1$ edges.  Even if we have cycles - provided the cycles are not negative - the algorithm will still hold.

It is possible to save the paths holding the minimum distances from the starting node to the remaining nodes in the graph, along with any negative cycles detected.

The Bellman-Ford algorithm is slower than Dijkstra's algorithm, but has more general applications.  Bellman-Ford runs in $O(V \cdot E)$ time, where $V$ is the number of vertexes (nodes) and $E$ is the number of edges, while Dijkstra runs in $O(V + E\log(V))$ time.  Usually $E \approx V^2$, so these simplify to $O(V^3)$ and $O(V+V^2\log(V))$ time, respectively, meaning Dijkstra is used more often as negative weights are rare in most applications.  

If you don't have negative weights, then use Dijkstra's algorithm due to its faster run time.  However, if you have negative weights, use the Bellman-Ford algorithm; if you have a negative cycle, though, then neither algorithm will work.

You likely won't need to implement Bellman-Ford algorithm, but it's good to be familiar with it and known when to use it compared to Dijkstra's algorithm.

### Other algorithms 
If you wish to find the shortest paths between all pairs of nodes, you can use Johnson's algorithm or the Floyd-Warshall algorithm.  Both of them work for weighted graphs, directed or undirected.  Each of them work for negative weights, but not for negative cycles.  These are beyond the scope of what you likely need to know in an interview.  However, it's good to know about these and other techniques for finding the shortest path in a graph.

## Minimum spanning trees
You are often given a graph with tons of nodes and edges.  You might want to clean the graph up by removing unnecessary edges.  A **spanning tree** is a pruned version of the original *undirected, weighted* graph, where there are no cycles in any of the edges while all the nodes remain connected.  (If the graph is not connected, i.e. not all the nodes are connected to one another, then you can generate spanning trees for each set of nodes that can be connected.)  The **minimum spanning tree** is a spanning tree for an *undirected, weighted* graph where the sum of the edges are as minimized as possible.

For example, if you have the following graph (Example 5):
```
    8      3
A ----- B --- C
        |   / |
       4| 2/  | 6
        | /   |
        D-----E
           3
```
One possible minimum spanning tree is:
```
    8      3
A ----- B --- C
            / 
          2/  
          /   
        D-----E
           3
```
Notice how the edges for `BD` and `CE` are removed.  Each node is connected, and there are no cycles.

Minimum spanning trees have many real-life applications, such as laying down wires for a fiber-optic network, electrical wiring for a power grid, clustering in machine learning, and many, many more.

We will discuss two popular ways to construct a minimum spanning tree: Kruskal's Algorithm and Prim's Algorithm.

In **Prim's algorithm** you start with a new graph from scratch by picking any vertex you wish with *no* edges included yet.  Then add one edge at a time in such a way so that we pick the edge with the lowest weight, and the node that's connected is not part of the new graph yet.  If more than one edge has the lowest weight, pick any one of them you wish.  Repeat the process by adding edges until all the vertices are connected together.  

In **Kruskal's algorithm** you begin by taking the edges and sorting them by their weight.  In each step, pick the edge that has the smallest weight while ensuring it does *NOT* form a cycle and connect the nodes together.  (If it does the edge is not considered.)  Continue to add edges until all the nodes are connected.  IMPORTANT: Unlike in Prim's algorithm where you will have a single graph that you build out, in Kruskal's algorithm initially you might have multiple subgraphs that aren't connected as edges are added in; e.g. for a graph with nodes A through J that are connected, you might have one subgraph with nodes A, B, and C connected but another with nodes G and H connected at some point, but eventually all the nodes will connect and form a single graph.

Kruskal's algorithm is usually a little faster than Prim's algorithm, although it will depend on how the graph is represented and what additional data structures are used (e.g. sets, priority queues).

## When to use each type of graph


## Practice problems
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

Consider the type of problem and which approach would work best (e.g. DFS, Dijkstra's algorithm).

- **Find the celebrity:** [LeetCode](https://leetcode.com/problems/find-the-celebrity/)
- **Number of islands:** [LeetCode](https://leetcode.com/problems/number-of-islands/)
- **Cheapest flights within K stops:** [LeetCode](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
- **Minimum cost to connect all points:** [LeetCode](https://leetcode.com/problems/min-cost-to-connect-all-points/)
- **Network delay time:** [LeetCode](https://leetcode.com/problems/network-delay-time/)
- **Max area of island:** [LeetCode](https://leetcode.com/problems/max-area-of-island/)
- **Course schedule:** [LeetCode](https://leetcode.com/problems/course-schedule/)
- **Minimum edge reversals so every node is reachable:** [LeetCode](https://leetcode.com/problems/minimum-edge-reversals-so-every-node-is-reachable/)


## References and extra information
- *Introduction to Algorithms* by Thomas Cormen, Charles Leiserson, Ronald Rivest, Clifford Stein
- *Algorithms, 4th Edition* by Robert Sedgewick and Kevin Wayne, with supplemental site [here](https://algs4.cs.princeton.edu/home/)
- [Baeldung](https://www.baeldung.com/cs/path-vs-cycle-vs-circuit): Graph cycles vs. paths vs. circuits