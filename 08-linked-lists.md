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
 head
  |
  |
  v
*****        *****        *****        *****        
* 1 * -----> * 2 * -----> * 3 * -----> * 4 * -----> null
*****  next  *****  next  *****  next  *****  next  
```
Each node contains data, represented by the numbers above.  From each node is a pointer, denoted "next", that points to the next node in line.  (Technically the "next" attribute points to a memory address, and then the data can be accessed there accordingly.)

The singly linked list starts off with a pointer, denoted "head", that points to the very first node in the list.  The end of the list is denoted by the word "null" at the end which means that the final node points to nothing in memory.

This is called a *singly* linked list because we can only travel one way - forward.

Add some sample problems here!  In the future, add *a lot of visuals*!

## Doubly linked lists

## Circular linked lists

## Additional resources

Advantages vs. disadvantages compared to other data structures (e.g. arrays/lists)