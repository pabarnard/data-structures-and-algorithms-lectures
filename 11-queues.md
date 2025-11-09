# Queues

A **queue** is a data structure that operates like a line in a grocery store.  So items are added, or **enqueued**, to the back of the line, while items are removed, or **dequeued**, from the front of the line.  So in a grocery line, the person waiting the longest is served first, while the latest person to arrive gets served last.  Queues act as a first in, first out (FIFO) data structure, unlike stacks.

Many implementations of queues allow you to peak at the **head**, or front, of the queue, without removing it.  Some also allow you to examine the **tail**, or back, of the queue.

## Applications for queues
Queues are used a lot in managing web traffic, such as handling API requests, visitors to a specific site, managing customers attempting to grab an item online in high demand, and much more.  Call centers process customers in the order that they were received.

Anytime you want to process data, traffic or anything else in sequential order where it's first in, first out is a good application for a queue.

Whenever you use a data structure like a graph or a tree, a queue is useful for looping through each level of the data structure.  This is *breadth-first search* (BFS), where we cover the breadth of one level before moving down to the next one.

## Priority queues (heaps) and other types of queues
There are actually several types of queues that are good to know about.  So far you've learned about normal queues.  But there are other types to consider as well: priority queues, double-ended queues (deques) and circular queues.

A **priority queue** works like a normal queue, except the difference is that data is saved in a specified order when added.  Most implementations of priority queues by default place the smallest value at the head and the largest value at the tail, although depending on the language you might be able to specify a different way to sort and save the data.  Many languages use a *heap* data structure to implement a priority queue.  While we will not cover heaps in this section, know that heaps are tree data structures such that parent nodes will hold larger values than the child nodes in a maximum heap and vice versa for a minimum heap.  A great animation can be found at https://visualgo.net/en/heap.

It's worth noting that adding or removing from a priority queue requires $O(\log(n))$ time.

A **double-ended queue (deque)** is like a normal queue as well, but it allows for efficiently removing and adding to both the head and tail of the queue.  So if you often will remove from the tail of the queue or add to the head of the queue, then a deque will work best.

A **circular queue** is a queue where the tail points to the head, effectively forming a loop.  It's used often when memory is limited and you need to specify a limit when it comes to how much data needs to be saved.  Often you won't need to use circular queues in algorithm challenges but it's good to know, as occasionally you might need to implement or use one.

## When and how should a queue be used?  When should a different data structure be used?
Queues are useful if you need to store *and* process data in order.  Remember that queues are FIFO, while stacks are LIFO (last in, first out).

Like stacks, a queue should not be used for accessing a random item, as it's $O(n)$ time.  Arrays and maps are superior.

Adding to the back of the queue is an $O(1)$ operation, as is removing from the head of the queue.

**IMPORTANT:** Some tutorials use arrays to serve as queues.  You can use them if you're in a pinch, or if a language doesn't natively support queues.  **HOWEVER,** in most cases an array does NOT function as a true queue: if you consider the first element as the head of the queue and the last element as the tail, removing from the front is very likely an $O(n)$ operation in most programming languages.  A well-defined queue should be able to remove from the front in $O(1)$ runtime, and arrays usually don't function this way.  *Thus be mindful if you use an array as a queue, as dequeuing is then likely $O(n)$ time instead of $O(1)$ time.*

## Tips for solving problems
- **Consider using a double-ended queue (deque):** A double-ended queue is useful if you often need to enqueue (add) the head (front) of the queue or dequeue (remove) the back (tail) of the queue.
- **Priority queues for smallest and largest problems:** If you need to grab the $k$th smallest or largest item, and you can't mutate the original data, a priority queue is best for holding values in order.  If a priority queue sorts data from smallest to largest, and you need to store data from largest to smallest, a trick you can use is to negate - i.e., multiply by -1 - the values as you save them into the priority.  For example, if you needed to find the 3rd largest value in the array `[3, 8, 2, 1, 5, -4]`, you can multiply each value by -1 to get `[-3, -8, -2, -1, -5, 4]` and then save these values into the priority queue to get `[-8, -5, -3, -2, -1, 4]`.  Once you locate the value, then you can grab it and multiply by -1 to get its original value back.  So in this case, the 3rd largest value will be 3 after grabbing -3 from the queue by taking out the -8 and -5.
- **Consider the queue type:** Think about the best time to use a normal queue vs. a priority queue vs. a circular queue.  If you need to process the data in the order it came in, a normal queue will be best.  A priority queue is useful for problems where you need to retrieve the smallest or largest value quickly from unsorted data.  Circular queues are better if you need to specify a capacity or have limited memory, and you wish to overwrite old data that is no longer needed.
- **Use queues for breadth-first search (BFS):** If you need to travel down a tree or a graph or a similar data structure, and you want to cover each level or tier in its entirety, then breadth-first search (BFS) is the way to go.  (Trees will be examined in detail soon!)

## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

1. **Implement queue using stacks:** You are to design a queue data structure from scratch using two stacks only and no built-in data structures otherwise.  It should be able to check if the queue is empty, pop items from the head (front), examine what's at the front, and push new values to its tail (back).  You can find this problem on LeetCode [here](https://leetcode.com/problems/implement-queue-using-stacks/).
2. **kth largest element in array:** Given an array of integers, return the `k`th largest element found, NOT the `k`th distinct element.  Solve this using a heap *without* sorting.  For example, if the array is `[3, 8, 5, -3, 3, 4]` and `k = 2`, return 5 as that's the second largest element.  You can try this problem on LeetCode [here](https://leetcode.com/problems/kth-largest-element-in-an-array/). 
3. **Sort characters by frequency:** You're given a string as input.  You are to return a new, sorted string such that its characters are sorted from most to least frequent, and all occurrences of a character are grouped together.  For example, if you have "abababbmam", return "aaaabbbbmm".  If there are any ties in terms of frequency, the tied characters can be picked in any order, provided that all occurrences of a specific character are grouped together, so "aabb" or "bbaa" are okay, but not "abab" as all the "a"s must be next to one another, and the same with all the "b"s.  You can try this problem on LeetCode [here](https://leetcode.com/problems/sort-characters-by-frequency/).
4. **Sliding window maximum:** You're given an array of integers and a separate integer `k` as input.  The integer `k` represents the size of a sliding window.  Your goal is to save the largest value for each possible sliding window from left to right into a new array, and then return that array.  For example, if you have `[3, 1, 4, 5, -2, 8, 1, 4, 7]` and `k = 4`, return `[5, 5, 8, 8, 8, 8]`.  Try this problem out on [LeetCode](https://leetcode.com/problems/sliding-window-maximum/).
5. **Rotting oranges:** You're given a starting `m` x `n` array of integers as input, where each integer is 0 for an empty cell, 1 for a fresh orange or 2 for a rotten orange.  Each minute that passes by results in all fresh oranges that are adjacent to the top, bottom, left or right of a rotten orange spoiling and becoming rotten themselves.  Return the minimum number of minutes required for all oranges to turn rotten, or -1 if it's impossible.  For example, if you have `[[0, 1, 1], [1,0,1], [2,0,0]]`, return -1 as only one fresh orange can become rotten.  But if you have `[[0,1,1], [1,1,1], [2,0,0]]`, return 4.  Try this problem out on [LeetCode](https://leetcode.com/problems/rotting-oranges/).
6. **Making a large island:** You have an `m` x `n` array of integers as input, where each 0 is ocean and 1 is an island.  You are allowed to change at most *one* of the 0 values to 1.  Return the size of the largest island possible after changing (if applicable) a single 0 to a 1.  For example, if you have `[[1,0,1],[1,1,0]]`, return 5, as either 0 can be changed to get a single island of size 5.  This problem can be found on LeetCode [here](https://leetcode.com/problems/making-a-large-island/).

## Useful references
- [Java Queue interface documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Queue.html), [Java Deque interface documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Deque.html), [Java ArrayDeque class documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/ArrayDeque.html) and [Java PriorityQueue class documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/PriorityQueue.html)
- [Python deque data structure from collections module](https://docs.python.org/3/library/collections.html#collections.deque) and [Python heapq module for heaps (priority queues)](https://docs.python.org/3/library/heapq.html)
- [JavaScript arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) - note that there is no official data structure for queues, so arrays can effectively serve the same purpose, although not as efficiently.  You can use the `push` and `shift` methods, but note that the `shift` method is an $O(n)$ operation instead of $O(1)$ for dequeuing.
- [C# Queue<T> documentation](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.queue-1)  
- [LeetCode queue and similar challenges](https://leetcode.com/problemset/) - select "Queue", "Breadth-First Search", "Heap (Priority Queue)" at least
- [GeeksforGeeks - queues](https://www.geeksforgeeks.org/queue-data-structure/)  
- [HackerRank queue challenges](https://www.hackerrank.com/domains/data-structures/queues)  
