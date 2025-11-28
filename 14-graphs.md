# Graphs

When you hear the word "graph," you might visualize bar graphs or pie graphs or a similar visual figure in statistics and infographics.  Perhaps you think of graphs of functions from mathematics, like the graph of a basic parabola such as $y = x^2$.  In computer science, graphs take on a different meaning.  

A **graph** in computer sciences is an abstract data structure represented by a bunch of vertexes and edges.  A *vertex* or *node* is a data container.  It could hold strings, numbers or any other data that you may deem fit.  An *edge* or *link* is a connection from one vertex to another.

Graphs can be undirected or directed.  An *undirected graph* is depicted with edges that do not have a direction indicated in any way, shape or form; vertexes are connected by simple lines.  A *directed graph* contains edges that point in one or both directions between two nodes. 

Here is a visual of an *undirected graph*:
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

Here is a *directed graph:*
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

Graphs have tons of applications!  When you're trying to find the fastest or shortest way to get to your destination via GPS or a map application, a graph is traversed to determine your route.  If you want to see who's following you and who you're following in social media, a graphic depiction comes in handy.

## Representations of a graph
Talk about defining a graph; adjacency lists, adjacency matrixes

## Traversing a graph
Talk about breadth-first vs. depth-first search
Finding shortest path (e.g. Dijkstra's Algorithm)

## Topological sorting


## Cycles and detecting them


## Minimum spanning trees


## When to use each type of graph


## Practice problems


## References