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
Talk about breadth-first vs. depth-first search
Finding shortest path (e.g. Dijkstra's Algorithm)

## Topological sorting


## Cycles and detecting them


## Minimum spanning trees


## When to use each type of graph


## Practice problems


## References