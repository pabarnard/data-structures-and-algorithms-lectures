# Stacks

A **stack** is a data structure where data starts at the bottom and new items get added above it.  It is a last in, first out (LIFO) data structure.  Imagine cooking a stack of pancakes: you put the first one at the bottom, and then each new one is placed at the top.  Thus the oldest pancake is at the bottom and the newest one is at the top.  

When removing from a stack, you remove the item at the top first, and then the next item removed is the one on top of the remainder.  If you eat a stack of pancakes, the safest way would be to eat the topmost one first, then the next one immediately below that, and so on until the last pancake at the bottom is consumed.  Another way to look at it is a stack of plates, where you remove the one at the top first.  If you were to remove a plate that isn't the topmost one, you might find a bunch of them falling faster than a Jenga tower that's about to topple - or worse, having them break!

Adding to the top of a stack is called **pushing**, which is $O(1)$ time.  Removing from the top of the stack is called **popping,** and this is also $O(1)$ time. Many implementations include a way to examine the topmost item in the stack, usually called **peeking** or looking at the **top**.

## Applications for stacks
Stacks are used in recursion to keep track of function calls using a *call stack.*  If the stack gets too big, there's *stack overflow*, causing the code to crash.

Some implementions of the undo and redo operations utilize stacks.  (They can also be implemented using linked lists.)  One stack holds the operations for undoing while another holds the operations for redoing, and once a new operation is perform, the stack holding the redo operations is cleared out.

## When and how should a stack be used?  When should a different data structure be used?
Stacks are used most when the newest operation or piece of data that's set aside should be revisited first because of its LIFO structure.

A stack should not be used for accessing a random item, as it's $O(n)$ time.  Arrays and maps are superior.

Some programming languages, like Java, have their own classes for stacks.  For Java, it's recommended to use the `Deque` interface, and one implementation is actually the `LinkedList` class.  In Python, the `deque` class from the `collections` module is best.

Other languages, however, don't have their own implementation.  In that case, you can use an array, as pushing to the end of an array is $O(1)$ time in both stacks and arrays.  Popping from the top of a stack is the same as popping from the end of an array, as removing in both cases is $O(1)$ time. 

## Tips for solving problems
- **Monotonic stacks:** A monotonic stack contains values in strictly increasing or decreasing order, which is useful in problems like finding the "next greater element."
- **Multiple stacks:** Use multiple stacks when needed for problems like implementing queues with stacks, keeping track of operations like undoing and redoing, etc.
- **Be aware of parentheses and string problems:** These types of problems often utilize stacks, like if you have a valid set of parentheses.

## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

1. **Valid parentheses:** You're given a string consisting of only parentheses `()`, curly braces `{}`, and/or square brackets `[]` as input.  Your goal is to return true if the input contains valid braces that open and close properly, and false otherwise.  For example, if you have `"(({}[]))"`, return true.  You can find this problem on LeetCode [here](https://leetcode.com/problems/valid-parentheses/).
2. **Next greater element:** You're given two arrays of non-negative integers, each with *distinct* (unique) values as input.  The first array is a subset of the second array; in other words all the elements in the first array can be found in the second.  Your goal is to examine each value in the first array and then find the same value in the second array, and then in the second array locate the first value strictly larger than this one, and then save that value into a new array.  If there is no value bigger on the right, save the value -1.  Return this array of indexes.  For example, if you're given `arr1 = [3, 1, 5, 8]` and `arr2 = [7, 3, 1, 4, 5, 2, 8, 6]`, return `[4, 4, 8, -1]`.  You can practice this problem on LeetCode [here](https://leetcode.com/problems/next-greater-element-i/).
3. **Final prices with a special discount in a shop:** You're given an array of prices.  For each index `i`, `0 < i < prices.length`, it's possible to get a discount equal to `prices[j]`, where `j` is an index such that `j > i` and `j < prices.length`.  The index `j` is minimized so that `prices[j] <= prices[i]`.  If no such index `j` exists, there is no discount for `prices[i]`.  Return a new array consisting of the final prices of each item after applying discounts where possible.  For example, if `prices = [3, 2, 5, 7, 10, 2]`, return `[1, 0, 3, 5, 8, 2]`.  You can practice this problem on LeetCode [here](https://leetcode.com/problems/final-prices-with-a-special-discount-in-a-shop/)
4. **Implement a stack using queues:** Using two queues, design the stack data structure.  (We'll talk about queues in the next lesson!)  You can find this problem on [LeetCode](https://leetcode.com/problems/implement-stack-using-queues/).
5. **Remove all adjacent duplicates in a string:** You're given a string and an integer `k` as input.  Your goal is to remove the all substrings of length `k` from the string, and repeat this process as often as possible.  The remainder of the string is to be returned as a new string.  For example, if you're given `str = "bbmmmbcaaacdddeef", k = 3`, return `"cceef"`.  You can try this challenge on LeetCode [here](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/).
6. **Minimum stack:** You are to design a special stack data structure where pushing, popping, and retrieving the topmost value are to be done in $O(1)$ time like normal stacks, and you can retrieve the minimum element of the entire stack in $O(1)$ time too.  You can practice on [LeetCode](https://leetcode.com/problems/min-stack/).
7. **Largest rectangle in histogram:** You're given an integer array as input, where each value is the height of a histogram with a width of 1.  Your goal is to return the area of the largest rectangle you can form with the histograms.  For example, if you're given `[3, 2, 5, 2, 3, 1, 7]` as input, return 10.  The $O(N^2)$ runtime solution is straightforward, but a faster solution is much more difficult.  You can challenge yourself on [LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/).
8. **Longest valid parentheses:** You're given a string consisting of only parentheses.  Return the length of the longest substring consisting of valid parentheses.  For example, if you have `"(()()"`, return 4.  You can find this problem on [LeetCode](https://leetcode.com/problems/longest-valid-parentheses/).

## Useful references
- [Java 17 Stack documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Stack.html) and [Java 17 Deque documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/Deque.html)  
- [Python list methods](https://docs.python.org/3/tutorial/datastructures.html#more-on-lists) and [Python deque data structure from collections module](https://docs.python.org/3/library/collections.html#collections.deque)  
- [JavaScript arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) - note that there is no official data structure for stacks, so arrays can effectively serve the same purpose.
- [C# Stack<T> documentation](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.stack-1) and [LinkedList<T> documentation for C# - uses doubly linked lists](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.linkedlist-1)
- [LeetCode linked list practice problems](https://leetcode.com/problem-list/stack/)  
- [GeeksforGeeks - stacks](https://www.geeksforgeeks.org/stack-data-structure/)  
- [LeetCode stack problems](https://leetcode.com/tag/stack/)  
- [HackerRank stack problems](https://www.hackerrank.com/domains/data-structures/stacks)  