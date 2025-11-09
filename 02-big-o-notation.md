# Big O Notation

**Big O notation** is used to denote how an algorithm scales as the size of an input - or a series of inputs - increases.  For example, if the size of an input array increases, how does it affect the performance of an algorithm in terms of space and time?  Very often in interviews you will be asked to solve problems and explain why you went with one method or another, and frequently you will have to talk about time and space complexity in the implementation of your solution to an algorithm challenge.

By the time you are done with this page, you should:
- Understand how Big O works
- Explain what **time and space complexity** mean
- Analyze and compare algorithm efficiency
- Explain common **tradeoffs** between time and space
- Apply Big O in real code

## Overview of Big O notation
Big O notation looks like this: $O(???)$, where the question marks indicate a value or expression.  Big O notation is used to talk about the time and space complexity of an algorithm.  It expresses the *worst-case performance* in terms of time and space, so it serves as an upper bound.

When combining operations we add them together like so: $O(n^2+3n+1)$.  

Here are some rules of thumb for simplifying these expressions:
- We keep the highest order term, which is $n^2$, so this becomes $O(n^2)$. (The expression itself is made up, so don't about where these values came from, as the point is to simplify it.)  
- Whenever a number is multiplied by anything with $n$ (or a similar variable), the number is discarded like so: $O(5n)$ becomes $O(n)$. 
- The highest power (e.g. the 5 in $n^5$) is the term usually retained, so for example if you have $O(n^5+8n^4+6n^3)$, we keep the $n^5$ as the highest power is 5 (note that the numbers 8 and 6 aren't considered as they're constants).
- Exponential (e.g. $2^n$) and factorial ($n! = n \times (n - 1) \times (n - 2) \times ... \times 3 \times 2 \times 1$) terms grow the fastest, with factorials usually blowing up faster than exponentials.

Now let's talk about time and space complexity!

## Time complexity
**Time complexity** measures how the runtime of an algorithm grows relative to the input size.  

Here are some common time complexities, from best to worst:

| Big O          | Name             | Examples                                                           |
|:--------------:|------------------|--------------------------------------------------------------------|
| $O(1)$         | Constant         | Accessing an array element by index, grabbing an item in a map     |
| $O(\log(n))$   | Logarithmic      | Binary search to find one value in a sorted array                  |
| $O(n)$         | Linear           | Looping through an array                                           |
| $O(n\log(n))$  | Linearithmic     | Merge sort, quick sort average case                                |
| $O(n^2)$        | Quadratic        | Nested loops (e.g. bubble sort, insertion sort)                    |
| $O(2^n)$        | Exponential      | Recursive Fibonacci without memoization                            |
| $O(n!)$        | Factorial        | Finding all arrangements of $n$ unique elements                    |

Don't worry if some of terms (e.g. binary search, merge sort) do not make sense at this moment, as we will cover them as you progress through the material.

To illustrate big O time complexity, here are some examples in JavaScript:
```js
const myStr = "happy times"; // Strings are O(n) space (more on that below)
// Loop that's O(n) time since we are going through each character in the entire string
for (let k = 0; k < myStr.length; k++) {
    console.log(myStr[k]); // Print each character in the string
}
```

## Space complexity
**Space complexity** measures how much *additional memory* your algorithm uses, relative to the input size.  This means that the sizes of the inputs do NOT count towards space complexity.

A variable that holds a number or boolean variable requires $O(1)$ space because the amount of memory required is the same no matter the value.  On the other hand, if an array is needed, $O(n)$ space is used up.  It's important to note that the array can hold up to $n$ items, even if the algorithm winds up not saving any values into it, and this is because we consider the *worst-case scenario*.

```js
const x = true; // Boolean values are O(1) space, as are numbers
const arr1 = []; // Array that could hold any number of items: O(n) space
const arr2 = [[1, 3, 5], [2, 1, 4]]; // O(m*n) space, as we have m sublists of size n (note that we don't actually do any counting)
```

## Time vs. space tradeoffs
Usually making a program faster means using more memory — and vice versa.  These are called **time-space tradeoffs**.

### Examples of tradeoffs:
- Hash maps and sets allow for $O(1)$ fast lookups, but they require extra space.
- Sorting an array **in-place** saves memory but may be slower than other sort methods.  For example, while selection sort allows you to sort an array in place, it runs in $O(n^2)$ time, it doesn't require more than $O(1)$ space since no new arrays are needed.  Merge sort is faster with $O(n\log(n))$ time, but it requires $O(n)$ space each time the array is split and merged.
- Adding to the end of an array or list is usually $O(1)$ time, but for a singly-linked list it's $O(n)$ time.  On the other hand, adding to the beginning of an array or list is $O(n)$ time due to needing to move items around before space is made for the new entry, while in a singly-linked list it can be done in $O(1)$ time by rearranging pointers regardless of the size of the list itself.

Being aware of these tradeoffs helps you make smart choices depending on the problem.

## Example problems
For thes problems, determine the time and space complexity of the two approaches in each challenge.  Solutions are provided at the end.

__Problem 1:__ The two-sum problem: you're given an array of integers and another integer - a target value - as input.  Return `true` if it's possible to find two  integers at two different indexes that add up to the target value, and `false` otherwise.

Here's approach 1 in JavaScript:
```js
function twoSum(arr, target) {
    for (let i = 0; i < arr.length - 1; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] + arr[j] === target) {
                return true;
            }
        }
    }
    return false;
}
```
Here's approach 2 in JavaScript:
```js
function twoSum(arr, target) {
    let numbersFound = new Set(); // A set holds unique values
    for (let i = 0; i < arr.length; i++) {
        const currentValue = arr[i];
        if (numbersFound.has(target - currentValue)) { // For example, if the target is 12 and the current value is 4, have we found an 8 yet?
            return true;
        }
        if (!numbersFound.has(currentValue)) { // Add new value to set if we haven't found it yet
            numbersFound.add(currentValue);
        }
    }
    return false;
}
```

__Problem 2:__ Check if an array are sorted: you are given an array of integers as input.  You are to return `true` if the array is sorted from smallest to largest (non-decreasing order) and `false` otherwise.

Approach 1 in JavaScript:
```js
function isSorted(arr) {
    for (let i = 1; i < arr.length; i++) {
        if (arr[i - 1] > arr[i]) {
            return false;
        }
    }
    return true;
}
```
Approach 2 in JavaScript:
```js
function isSorted(arr) {
    let originalArr = [...arr]; // Create deep copy of original array
    arr.sort((a,b) => a - b); // Sort in non-decreasing order; note that this is done in place and you should NOT modify the original inputs usually in most problems - this is only done for this demo
    for (let i = 0; i < arr.length; i++) {
        if (originalArr[i] !== arr[i]) {
            return false;
        }
    }
    return true;
}
```
## Additional resources and references
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/) - A quick guide to time and space complexities of common operations
- [VisuAlgo](https://visualgo.net/en) - Great for visualizing algorithms and their efficiency
- [Big O from Free Code Camp](https://www.freecodecamp.org/news/big-o-cheat-sheet-time-complexity-chart/) - More on Big O notation

## Solutions to example problems
- Problem 1, Approach 1: Uses $O(1)$ space due to only using two variables (`i` and `j`) that hold numbers and requires $O(n^2)$ space due to a nested loop involving the array.
- Problem 1, Approach 2: Uses $O(n)$ space as the worst-case scenario is each value in the input array is unique and thus required to be saved into the set.  (This trumps the $O(1)$ space for the `i` and `currentValue` variables.)  Uses $O(n)$ time due to only needing a single for loop that's not nested.
- Problem 2, Approach 1: Uses $O(1)$ space as the only variable, `i`, is a number, and $O(n)$ time is required due to the single loop.
- Problem 2, Approach 2: Uses $O(n)$ space due to needing memory for a new copy of the array, and it's $O(n\log(n))$ time to sort as shown.  (Most sorting techniques in real life are $O(n\log(n))$ time, but some specialized ones can run in $O(n)$ time.)