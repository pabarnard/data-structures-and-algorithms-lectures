# Trees

The first thing you might conjure up when you hear the word "tree" is a living plant with a trunk, leaves, branches, etc. that comes in varieties like oak, pine, and magnolia.  You can imagine a forest full of trees.

Trees take on a different meeting in computer sciences.  **Trees** consist of a series of nodes that point to other nodes.  You can think of a tree as a specialized type of directed graph.  The topmost node of the tree is called the **root**.  There can only be one root.  (Note that this is completely different from the roots of living trees, which are underground.)

Every node, except the root, has a **parent** node, which is the node found directly above the current one.  There can only be at most one parent node for each node in the tree.  The **child** nodes are the nodes that are next after the current one.  It's possible to have multiple children for each node.  A node cannot point to itself.  **Sibling** nodes are nodes that have the same parent node.

A node with no children is called a **leaf** node.

The **height** of the tree is the length of the longest path from the root node to any other node in the tree without repeating.  To find the height, count the number of edges traversed.

The **size** of the tree is the number of nodes found in the entire tree.

A node's **level** is represented as the number of edges required to reach it.

Here visually is a possible tree, and you can see how it resembles a pine tree (Example 1):
```
        10                  Level 0
       /  \
      /    \
    |/_    _\|
    5         4             Level 1
   / \         \
  /   \         \
|/_   _\|       _\|
1       7         3         Level 2
```
The 10 node is the root node of the tree.  The 5 node is the parent node of the 1 and 7 nodes, while the 1 and 7 nodes are siblings and also child nodes of the 5 node.

The height of the tree in the example is 2.  We have two leaf nodes: the 1 and 3 nodes.

You'll hear other common terms like *pruning* for removing a portion of the overall tree and *subtrees* for a specific piece of the tree.  There are other terms used to describe trees, like full trees (all nodes have 0 or 2 children), balanced trees (height of left and right subtrees differ by at most one) and perfect trees (a full tree with all leaf nodes at the bottom-most level, and all other nodes have two children).  You can read more from Baeldung [here](https://www.baeldung.com/cs/full-vs-complete-vs-perfect-tree).

Trees are used to save data in such a way so that searching can be done in roughly $O(\log(n))$ time, like information from a database.  Database indexing uses specialized types of trees to accomplish this task.  Trees are also used in machine learning to make decisions - hence the name "decision tree" - based on the data that's fed to the model.  Whenever you see suggestions pop up as you type what you're looking for in your favorite search engine (e.g. Google, Bing), the recommendations come from a tree as well.

WARNING: Be careful if you have duplicate values.  Some implementations of certain types of trees might not allow you to have duplicates, while you can make tweaks in other cases to accommodate them.  For example, you might have a counter to hold the number of instances of a given value or have the node represent another data structure holding the repeated values.

If you use the wrong type of tree, it might not be effective if you save data in a specific way, so be careful.  For example, if you store values into a tree, and you add values in order from smallest to largest, you basically are left with a singly linked list with additional pointers that do nothing, leading to $O(N)$ searches instead of $O(\log(N))$ search time.

## Types of traversals
There are four common types of ways to travel through a tree: pre-order traversal, in-order traversal, post-order traversal, and level-order traversal.

**Pre-order traversals** start with the current node, then recursively examines all nodes to the left, then recursively looks at all nodes to the right.

**In-order traversals** begin by recursively traveling through the nodes to the left of the current node, then examines the current node itself, then recursively goes through all the nodes to the right.

**Post-order traversals** look at all nodes to the left of the current node, then all nodes to the right, then finally the node itself.

**Level-order traversals** examine each node in each level in order, starting with the root node and working down the tree, traveling through each node in the current level - usually from left to right, depending on the implementation.  This is alternately called a **breadth-first search** or traversal of the tree.

        10                  Level 0
       /  \
      /    \
    |/_    _\|
    5         4             Level 1
   / \         \
  /   \         \
|/_   _\|       _\|
1       7         3         Level 2

In example 1, here are the traversals:
- Pre-order: 10, 5, 1, 7, 4, 3
- In-order: 1, 5, 7, 10, 4, 3
- Post-order: 1, 7, 5, 3, 4, 10
- Level-order: 10; 5, 4; 1, 7, 3 (other permutations are acceptable, as long as you have the values in each level from the top level all the way to the bottom)

## Binary trees
A **binary tree** is a tree where each node has anywhere from 0 through 2 children.  The data inside the nodes can be anything, and they can be saved anywhere.

Many algorithm challenges will use binary trees, so it's good to practice working with them!

## Binary search trees
A special type of binary tree is a binary search tree.  A **binary search tree (BST)** is a binary tree where values less than the current node are stored to the left and values bigger than the current node are stored to the right.

Here is an example of a binary search tree (Example 2):
```
        15                  Level 0
       /  \
      /    \
    |/_    _\|
    12       18             Level 1
   / \        
  /   \        
|/_   _\|      
4       13                  Level 2
 \
  \
  _\|
    6                       Level 3
```
Notice how at the root node 15 all values that are smaller are in the left subtree (12, 4, 13, 6) and the sole value bigger is in the right subtree (18).  When looking at the subtree with the nodes 12, 4, 13, and 6, all values less than 12 are to the left while all values bigger than 12 are to the right.  Notice these 4 nodes are all smaller than 15 in this subtree.

## Heaps (binary heap)
A **heap** is a data structure with the heap property: in a max heap, the parent's value is bigger than or equal to its children, while in a min heap, the parent is smaller or equal to its children.  Thus in a max heap, the biggest value is at the beginning (root), and in a min heap its smallest value is at the start (root).  For this page, we'll focus on a *binary heap,* which uses a binary tree.  (An alternate implementation of a heap uses an array.)

Heaps are used a lot as a basis for priority queues.  In fact, some languages even call priority queues "heaps", even though they're different data structures.  They're used most frequently when minimum and maximum values need to be saved or extracted frequently.

Note that in a heap, whenever a value is added or removed, the heap property may be violated.  This requires the tree to be re-balanced in order to re-establish the heap property by rearranging nodes or values as needed.  The actual implementation will vary based on the type of heap.  (There are many implementations of heaps, which is beyond the scope of this page, but you can read up on them on your own.  We're going to focus on when and how to use heaps.)

A heap will not necessarily have a specific ordering in terms of insertion or deletion.

Here is a visual of a possible maximum binary heap (Example 3):
```
        15                  Level 0
       /  \
      /    \
    |/_    _\|
    8        10             Level 1
   / \        
  /   \        
|/_   _\|      
2       6                   Level 2
```
Notice how each possible parent node must have a value bigger than or equal to its children in all cases.

## Tries
So far in the examples we've seen numbers.  But trees can hold any kind of data.  A special type of tree that can hold characters is a trie (pronounced "try").  A **trie** is a tree where each node holds a single item - usually a single character.  Alternately this is called a *prefix tree*.  Think of prefixes like "pre-", "post-", "in-", "un-", etc. that change the meaning of a word.  Here prefixes in this sense mean the same starting letters.

Here is an illustration of a trie (Example 4):
```
            |
            |
            |
            .       Starting point
           / \
          /   \
    -----A     R------
    |   / \        | |
    W  C   R----   A E--
   /|  |\  |\  |   | | |
  E A  E T E C M   Y D E--
    |                  | |
    Y                  L F
                       |
                       S
```
At the root of the tree there is no character.  From there we can pick a node to travel to next.  From there we construct words from the path traveled.  For example, we can create "REEL", "ARM", "ARE", etc.

Depending on the implementation, some nodes will have a boolean field indicating that the current node is a valid place to stop, even though you can travel farther down.  For example, you could form "REEL" or "REELS".

Tries are used a lot in auto-completions of words and phrases in search engines and in predictive algorithms.

If you have a lot of phrases or words, tries are very useful, but if you don't have a large set, tries will not be so great due to their high memory usage.

## Balanced trees
When you use a tree data structure, ensuring that the tree is not heavily tilted in one direction is important to ensure that retrievals can be accomplished in $O(\log(n))$ time as frequently as possible.  These trees should have $O(\log(n))$ height; such a tree is a **balanced tree**.

A **self-balancing tree** is a tree that rebalances itself when nodes are inserted or removed to ensure the height remains $O(\log(n))$ height.

There are many types of balanced tree data structures, each of which has its own implementation and definition of balance.

Named after its inventors, Georgy Adelson-Velsky and Evgenii Landis, an **AVL tree** is a self-balancing binary search tree.  The height of the left and right subtrees cannot differ by more than 1.  When a node is inserted or removed, the tree might be rotated at spots - in other words, left and right subtrees might be required to flip as you retrace, or move up, the tree.

Similar to an AVL tree is a red-black tree.  A **red-black tree** is a self-balancing binary search tree like an AVL tree that satisfies these properties:
- Each node is assigned a "color": red or black
- Null nodes are black
- Red nodes cannot have a red child
- All paths from one node to a leaf node travel through the same number of black nodes (this is called the starting node's "black height")

For a red-black tree, the path from the root to the leaf node farther away cannot be more than twice the distance of the path from the root to the nearest leaf node.

When a node is added or removed from an AVL tree, the tree rebalances itself by rotating the tree and by recoloring nodes as needed while still meeting the requirements specified in the list up above.  There will not be more than three rotations to rebalance the tree.

AVL trees are stricter with rebalancing height than red-black trees, while adding and removing is faster for red-black trees.  Rebalancing is faster for red-black trees due to requiring fewer rotations.

A more generalized version of a self-balancing binary search tree is the B-tree.  A **B-tree** is a self-balancing tree that allows for multiple children per node.  This allows for smaller heights for the tree because more nodes can be used in each level.  They're used for database indexing and file management.

You likely won't need to worry about implementing self-balancing trees in interviews, but they can come up in system design interviews, so it's a good idea to familiarize yourself with them.

## Segment trees
When you need to perform frequent operations like the minimum value, maximum value, or the sum for a specific interval or range of values, especially if the values are in a random order, a segment tree can be useful.  A **segment tree** is a tree data structure where each node holds the minimum, maximum, or a sum, along with the starting and ending points where this value is correct.

Here's an illustration of a segment tree for sums with 0-indexing (Example 5):
```
Array: [8, 2, 5, 3, 1, 2]

        20 [0:5]------ 
        /             \
      14 [0:2]         6 [3:5] --------
      /      \            |           |
  10 [0:1]    5 [2:2]  4 [3:1]     2 [5:5]
 /        \             /    \
8 [0:0]   2 [1:1]   3 [3:3]  1[4:4]
```
Notice how the overall sum is at the top, and then for each level we break the intervals in roughly half, and repeat the process until each node only holds one value.

Most implementations use a binary tree, but you can have as many children as needed.  Finding any minimum or maximum for any interval requires $O(\log_m(n))$ time, where $m$ is the number of children allowed per node and $n$ is the total number of values.

Building segment trees requires $O(n\log(n))$ time, where $n$ is the number of segments.  These trees take up quite a bit of memory.  But then querying the tree for the minimum, maximum, or sum for any interval requires $O(\log(n) + k)$ time, where $n$ is the number of segments and $k$ is the number of intervals reported.

## Practice problems
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

Consider which type of tree would be most appropriate for the problem.

- **Range sum of BST:** [LeetCode](https://leetcode.com/problems/range-sum-of-bst/)
- **Longest common prefix:** [LeetCode](https://leetcode.com/problems/longest-common-prefix/)
- **Validate BST:** [LeetCode](https://leetcode.com/problems/validate-binary-search-tree/)
- **Reorganize string:** [LeetCode](https://leetcode.com/problems/reorganize-string/)
- **Word break:** [LeetCode](https://leetcode.com/problems/word-break/)
- **Lowest common ancestor of a binary tree:** [LeetCode](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- **Furthest building you can reach:** [LeetCode](https://leetcode.com/problems/furthest-building-you-can-reach/)
- **Skyline problem:** [LeetCode](https://leetcode.com/problems/the-skyline-problem/)
- **Vertical order traversal of a binary tree:** [LeetCode](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)