# Linked lists
A **node** is a location in memory that holds data and can have *pointers* that reference different memory locations - usually the next node in line and perhaps the previous node, depending on the data structure the node is part of.  Each node will usually hold a different set of data.  A **linked list** is a collection of nodes in memory that are connected together.

There are three main types of linked lists:
- Singly linked list
- Doubly linked list
- Circular linked list

One big advantage of a linked list is that all the nodes are in disparate locations in memory.  In other words each node is in a different spot and not necessarily adjacent to one another.  So the first node can exist in one spot and another can exist much farther away and still be connected via pointers.

Arrays are usually in contiguous locations in memory; in other words they are next to each other.  This makes adding to the beginning of an array very inefficient as every other item has to move down the line while new memory is allocated for expanding the array itself, but adding to the start of a linked list is much faster.  Conversely, adding to the end of a linked list might not be as efficient as adding to the end of an array if the linked list does not contain a pointer to the last node.

Most of the time you'll solve problems with singly and circular linked lists, although doubly linked lists do pop up.

## Singly linked lists
A **singly linked list** is a collection of nodes that point one way.  Visually it looks like this:
```
Visual of a single node:
********
* Data * ----->
********  next

Visual of the entire singly linked list:
 head
  |
  |
  v
*****        *****        *****        *****        
* 1 * -----> * 2 * -----> * 3 * -----> * 4 * -----> null
*****  next  *****  next  *****  next  *****  next  
```
Each node contains data, represented by the numbers above.  The data doesn't necessarily have to be a number - it could hold booleans, strings or even other objects and data structures.  From each node is a pointer, denoted "next", that points to the next node in line.  (Technically the "next" attribute points to a memory address, and then the data can be accessed there accordingly.)

The singly linked list starts off with a pointer, denoted "head", that points to the very first node in the list.  The end of the list is denoted by the word "null" at the end which means that the final node points to nothing in memory.

Some implementations of singly linked lists have a pointer called "tail" that reference the *last* node in the list; i.e. the tail points to the node that have a next attribute of "null" (or a similar value).

This is called a *singly* linked list because we can only travel one way - forward.

Singly linked lists are used frequently as the basis for many other data structures, including stacks and queues.  

## Doubly linked lists
A **doubly linked list** is a collection of nodes like a singly linked list.  The difference is that with a singly linked list, each node has only one pointer that references the next node in line, while in a doubly linked list each node has two pointers: one for the next node in line, and one for the *previous* node in the list.

Here are visuals for one node in the doubly linked list and the entire list itself:
```
Visual of a single node:
       ********
<----- * Data * ----->
 prev  ********  next

Visual of the entire doubly linked list:
            head
              |
              |
              v
            *****        *****        *****        *****        
null <----- * 1 * -----> * 2 * <----- * 3 * -----> * 4 *
            *   * <----- *   * -----> *   * <----- *   * -----> null
            *****        *****        *****        *****        
```
A doubly linked list contains a pointer to the head of the list.  Some implementations also have a tail (not pictured) at the end of the list.

Doubly linked lists have real-life applications: photo carousels in websites, saving operations that you can undo and redo, and navigating forwards and backwards in a web browser.  (You can alternately use two stacks here as well.)

## Circular linked lists
A **circular linked list** is a linked list that does not contain a null value, and the last node in the linked list points to the first node in the list.  The list itself can be singly or doubly linked.  

Here's an illustration of a circular, singly linked list:
```
head
  |
  |
  V
*****        *****
* 1 * -----> * 2 *
*****        *****
  ^            |
  |            |
  |            V
*****        *****
* 4 * <----- * 3 *
*****        *****
```
Notice how the node with the value 4 points to the first node, i.e. the head node with the value 1 enclosed, in the list.

Some implementations will have a `tail` pointer indicating the last node in the circular list.

## Big O comparison
When it comes to adding at the beginning of a data structure in terms of Big O time:
- All linked lists: $O(1)$
- Arrays: $O(n)$

When you add to the end of the data structure in Big O time:
- Linked lists with NO `tail` attribute: $O(n)$
- Linked lists with `tail` attribute: $O(1)$
- Arrays: $O(1)$

Looking up any item in the data structure:
- Linked lists of all types: $O(n)$
- Arrays: $O(1)$

There are tradeoffs when it comes to picking arrays vs. linked lists, so choose based on the type of operations you will perform most.

## Tips for solving problems
- **Beware edge cases:** Watch out for cases like an empty list, a list with only one node.
- **Be careful when modifying the head of the list (and possibly the tail):** If you're not careful, you might lose many more nodes than expected or lose the first node.
- **WARNING: You are NOT allowed to change the data in each node!!** You must solve these challenges by rearranging the nodes by manipulating the "next" attribute of each one.  You might need to move the head (and possibly tail) of the list.
- **Create pointer variables that run - or travel - through the list:** You might need multiple pointers, and you might need variables to create new lists by rearranging nodes.  Pointers are useful for holding nodes temporarily until they're ready to be added (back in)to the list.
- **For doubly linked lists, make sure you modify the prev and next attributes of each node:** You must preserve the integrity of the list so that you can traverse it properly.

## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

Most of the time you'll deal with singly linked list problems, but if you want to challenge yourself, you can use the same problems as those for singly linked lists, except be careful with the `prev` attribute in addition to the `next` attribute.

1. **Reverse a linked list:** You're given the head of a linked list.  Rearrange the nodes in such a way so that the list is reversed and return the head of the reversed list.  For example, if you're given the list `head -> 5 -> 3 -> 2 -> 10 -> null`, return `head -> 10 -> 2 -> 3 -> 5`.  (Hint: while there's an $O(n^2)$ runtime solution that might be more intuitive, try to see if you can come up with an $O(n)$ solution by using additional pointers.)  This problem can be found here on LeetCode: https://leetcode.com/problems/reverse-linked-list/
2. **Merge two sorted linked lists:** You're given the head of two linked lists, each of which have its values sorted in non-decreasing order.  Merge the two lists into a new one that's sorted, and then return the head of the merged list.  For example, if you have list 1: `head -> 3 -> 3 -> 5` and list 2: `head -> 2 -> 4 -> 7 -> 10`, return `head -> 2 -> 3 -> 3 -> 4 -> 5 -> 7 -> 10`.  More on this problem can be found here: https://leetcode.com/problems/merge-two-sorted-lists/
3. **Remove duplicates from sorted linked list:** You're given a sorted singly linked list which may contain duplicate values.  Remove the nodes that are duplicates and then return the head of the updated list.  For example, if you're given `head -> 5 -> 6 -> 8 -> 8 -> 10 -> 10 -> 11`, return `head -> 5 -> 6 -> 8 -> 10 -> 11`.  This problem can be practiced on LeetCode here: https://leetcode.com/problems/remove-duplicates-from-sorted-list
4. **Linked list cycle:**  You're given the head of a linked list as input, where one node may point to a previously encountered node, including itself.  Return true if there is such a cycle in the list - i.e., return true if a node points to itself or a previous node, and return false otherwise.  (Hint: you might find another data structure helpful for keeping track of which nodes we've encountered.)  You can find more info about this problem here: https://leetcode.com/problems/linked-list-cycle.  Here are some examples:
```
head -> 5 -> 8 -> 2 -> null // This returns false

head -> 1 -> 2 -v // return true, as the 2 node points to itself
             ^  |
             |  |
             ----
```
5. **Sort list:** You're given the head of a singly linked list as input.  Sort the nodes so that the data starting with the updated head is in non-decreasing order from beginning to end.  Do NOT change the values in the nodes!  For example, if you have `head -> 5 -> 3 -> 6 -> 6 -> 2 -> 1`, return `head -> 1 -> 2 -> 3 -> 5 -> 6 -> 6`.  You can practice this problem here: https://leetcode.com/problems/sort-list/
6. **Merge nodes in between zeroes:** You're given the head of a singly linked list with 0 at the beginning and the end, and all other nodes will be 0 or a positive value.  Modify the linked list so that all non-zero nodes contained between two nodes with a value of 0 are combined to form a single node holding the sum of those values.  The modified list will not contain any zeroes.  For example, if you have `head -> 0 -> 5 -> 2 -> 3 -> 0 -> 0 -> 5 -> 0`, return `head -> 10 -> 5`.  More info on this problem can be found here: https://leetcode.com/problems/merge-nodes-in-between-zeros
7. **Reorder list:** You're given the head of a singly linked list.  Your goal is to rearrange the nodes like so: given a node denoted as $N_i$, where $i = 0, 1, 2, ..., n-1$ and $n$ is the number of nodes in the list, rearrange the list from $N_0 \rightarrow N_1 \rightarrow N_2 \rightarrow ... \rightarrow N_{n-1}$ to $N_0 \rightarrow N_{n-1} \rightarrow N_1 \rightarrow N_{n-2} \rightarrow N_2 \rightarrow N_{n-3} \rightarrow ...$.  Basically you're taking the back half of the list, reverse it, then alternate the first half of the list with the reversed second half of the list.  For example, you go from `head -> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7` to `head -> 1 -> 7 -> 2 -> 6 -> 3 -> 5 -> 4`.  You can practice here: https://leetcode.com/problems/reorder-list/
8. **Merge k sorted lists:** You're given an array of sorted linked lists in non-decreasing order.  Each entry in the array is the head of a linked list.  Merge all of the linked lists into a new one and return the head of the merged list.  For example, if you have `[head->3->4, head->5, head->null, head->1->1->7]`, return `head->1->1->3->4->5->7`.  More can be found here: https://leetcode.com/problems/merge-k-sorted-lists/

## Additional resources
- [LinkedList documentation for Java 17 - uses doubly linked lists](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/LinkedList.html)  
- [Deques in Python, often used to implement linked lists](https://docs.python.org/3/library/collections.html#collections.deque) - note that Python does not natively have linked lists
- [datastructures-js npm package in JavaScript](https://datastructures-js.info/) - note that JavaScript does not have many built-in data structures, so they must either be defined manually or added via a package
- [LinkedList<T> documentation for C# - uses doubly linked lists](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.linkedlist-1)  
- [HackerRank linked list practice problems](https://www.hackerrank.com/domains/data-structures/linked-lists)  
- [LeetCode linked list practice problems](https://leetcode.com/problem-list/linked-list/)  
- [GeeksforGeeks - more on linked lists](https://www.geeksforgeeks.org/data-structures/linked-list/)  