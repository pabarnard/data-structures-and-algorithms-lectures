# Queues

A **queue** is a data structure that operates like a line in a grocery store.  So items are added, or **enqueued**, to the back of the line, while items are removed, or **dequeued**, from the front of the line.  So in a grocery line, the person waiting the longest is served first, while the latest person to arrive gets served last.  Queues act as a first in, first out (FIFO) data structure, unlike stacks.

Many implementations of queues allow you to peak at the **head**, or front, of the queue, without removing it.  Some also allow you to examine the **tail**, or back, of the queue.

## Applications for queues
Queues are used a lot in managing web traffic, such as handling API requests, visitors to a specific site, managing customers attempting to grab an item online in high demand, and much more.  Call centers process customers in the order that they were received.

Anytime you want to process data, traffic or anything else in sequential order where it's first in, first out is a good application for a queue.

## Priority queues (heaps) and other types of queues
Mention circular queues, priority queues, double-ended queues (deque)

## When and how should a queue be used?  When should a different data structure be used?
Queues are useful if you need to store *and* process data in order.  Remember that queues are FIFO, while stacks are LIFO (last in, first out).

Like stacks, a queue should not be used for accessing a random item, as it's $O(n)$ time.  Arrays and maps are superior.

Adding to the back of the queue is an $O(1)$ operation, as is removing from the head of the queue.

**IMPORTANT:** Some tutorials use arrays to serve as queues.  You can use them if you're in a pinch, or if a language doesn't natively support queues.  **HOWEVER,** in most cases an array does NOT function as a true queue: if you consider the first element as the head of the queue and the last element as the tail, removing from the front is very likely an $O(n)$ operation in most programming languages.  A well-defined queue should be able to remove from the front in $O(1)$ runtime, and arrays usually don't function this way.  *Thus be mindful if you use an array as a queue, as dequeuing is then likely $O(n)$ time instead of $O(1)$ time.*

## Tips for solving problems


## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

## Useful references

