# Arrays
An **array** is a collection of elements, each identified by an index or key, and stored in *contiguous* memory locations - in other words, all the elements must touch one another.

Here are some things to keep in mind with arrays:
- They are indexed starting usually at index 0.
- Grabbing from an array is efficient in that randomly retrieving any item requires only $O(1)$ time.
- Usually arrays are of fixed length and the same data type, but some languages give a little more freedom in terms of flexibility for variable space and data.
    - If you are working with a language where arrays must have a predefined length (e.g. Java), you might still be able to use a dynamic array-like data structure to allow you to expand and contract as needed, like an `ArrayList`, `List`, `Vector`, etc.
- Arrays can be multi-dimensional!
- Some problems may ask you to solve **in place.**  In other words, do NOT use a secondary array or data structure to hold values temporarily while rearranging the values in the array.

## Multi-dimensional arrays
Many are comfortable with one-dimensional arrays that look like `[1, 3, 2, 2]` and `["John", "Amanda", "Jack"]` (or similar symbols like `{}` depending on the language).  However, it's very common to deal with arrays that contain arrays.  A **matrix** is a 2-D array of values, and it pops up a lot in mathematics and computer science.

An example of a 2-D array of integers in JavaScript looks like this:
```js
let matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
    [10, 11, 12]
];
console.log(matrix[0]); // [1, 2, 3]
console.log(matrix[0][1]); // 2
```
In fact, you can go to 3-D, 4-D and beyond.  Here's a 3-D array:
```js
let boxOfData = [
    [
        [1, 2],
        [3, 4]
    ],
    [
        [0, 3],
        [6, 9]
    ],
    [
        [10, 15],
        [12, 8]
    ]
];
console.log(boxOfData[0]); // [[1, 2], [3, 4]]
console.log(boxOfData[1][0]); // [0, 3]
console.log(boxOfData[2][1][1]); // 8
```

## Tips for solving array challenges
As you tackle problems that involve arrays, here are some pointers to guide you in your journey:

- **Remember to use pseudocode and T-diagrams:** Think about the steps needed to solve the problem, one at a time.  Determine what variables, programming statements (e.g. loops, if statements), etc. are needed, and understand how your variables change.
- **Practice! Practice! Practice!** Solve problems early and often!  One does not become an expert overnight.  (Yes, these first two tips are exactly the same as before, but they bear repeating because they're that important!!)
- **Know the time complexity for basic operations:** Accessing an item in the array is $O(1)$, insertions/deletions at the *end* are $O(1)$, and *arbitrary* insertions/deletions are $O(n)$.  
- **Sorting:** Oftentimes you will need to sort the data from smallest to largest or in alphabetical order.  **WARNING:** Usually in algorithm challenges you are **discouraged** from modifying the original array, as for one this can introduce side effects and other unintended behavior down the road, and for two, you might be working with data from APIs and databases, which usually can't be changed anyway.
- **Watch edge cases:** Common edge cases include empty arrays, arrays with only one entry, arrays with the same value, arrays that have all negative values, very large arrays to test performance, etc.
- **Prioritize finding _a_ solution first, then refactor:** Try brute force if you are more of a beginner or if you are not sure where to start.  Then optimize the solution by trying to find ways to reduce the time complexity down, e.g. from $O(n^2)$ to $O(n\log(n))$ or even $O(n)$.  Common strategies include - but are not limited to - sorting, hash maps/tables and sets.
- **Useful techniques:** This includes the two-pointer technique, sliding window, binary search and prefix sums.
- **Watch for off-by-one errors:** Many times people struggle with the starting and/or ending statements in loops, and this can lead to loops starting or ending at the wrong index.  

## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

1. **Find the maximum element:** You're given an array of numbers as input.  Your goal is to find and return the maximum value.  For example, if you're given `[8, 2, 5, 7, 8, 5]`, return `8`.  A link to this problem can be found here: [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/program-to-find-largest-element-in-an-array/).
2. **Reverse an array:** Given an array of entries as input, reverse its entries.  (Some variants require you to reverse the array in place without a secondary array or data structure and without returning the data, while others require you to create a new array and return that.)  For example, if you have `[8, 3, 4, 6]` as input, then you wind up with `[6, 4, 3, 8]`.  Here's a link to this challenge: [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/program-to-reverse-an-array/#).
3. **Check if array is sorted:** Given an array as input, check if its values are sorted in non-decreasing order; i.e., starting at the beginning, is each value that comes after the current at least the same or bigger?  Return true if so and false if not.  For example `[3, 3, 5, 7]` returns `true`, but `[1, 3, 2, 5, 7]` returns `false`.  Here's a link to this challenge: [CodeChef](https://www.codechef.com/practice/course/arrays/ARRAYS/problems/ARRAYSORTED).
4. **Two sum:** Given an array of integers and a target integer as input, return an array of two values representing the indexes such that the sum of the values at those indexes add up to the target.  There will be exactly one solution, and the indexes must be sorted in ascending order.  For example, given `arr = [1, 3, 8, 4]` and `target = 7`, return `[1, 3]`, as the value at index 1 (3) and index 3 (4) add up to the target of 7.  Links to this problem can be found here: [LeetCode](https://leetcode.com/problems/two-sum/) and [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/2sum/).
5. **Move zeroes:** Given an array of values as input, some of which are 0, rearrange the order of the numbers *in place* in such a way so that the zeroes come at the end while the relative order of the remaining non-zero values is maintained.  For example, if you have `[3, 4, 0, 0, 1, 2, 0, 2]`, then you will wind up with `[3, 4, 1, 2, 2, 0, 0, 0]`.  Links to this problem can be found here: [LeetCode](https://leetcode.com/problems/move-zeroes/) and [AlgoMonster Explanation](https://algo.monster/liteproblems/283).
6. **Rotate array:** Given an array of values and a non-negative integer `k` as inputs, rotate the array by k spots to the right, wrapping around as needed.  For example, if you have `[1, 2, 3, 4]` and `k = 2`, then we wind up with `[3, 4, 1, 2]` after the rotations are complete.  Links to this problem can be found here: [LeetCode](https://leetcode.com/problems/rotate-array/) and [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/complete-guide-on-array-rotations/).
7. **Maximum subarray:** Given a non-empty array of integers as input, return the maximum sum that can found by taking any subarray (an array of contiguous values - i.e. values that are touching, like `[5]`, `[1, 3]`, `[3, 5]`, `[3, 5, 8]`, etc. in `[1, 3, 5, 8]`) found.  This uses an algorithm called Kadane's algorithm (more info found here: https://www.algodaily.com/lessons/kadanes-algorithm-explained).  For example, if you're given `[3, 2, -1, 5, 2, -3, 1]`, return `11` since that's the sum of the subarray `[3, 2, -1, 5, 2]`, and this is the maximum sum possible from all subarrays.  Links to this problem can be found here: [LeetCode](https://leetcode.com/problems/maximum-subarray/) and [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/largest-sum-contiguous-subarray/).  (A similar problem can be found here: https://leetcode.com/problems/minimum-size-subarray-sum/).
8. **Product of array except self:** Given an array of values, `arr`, as input, return a new array where the value saved at index `i` is the product of all values in `arr` except at `arr[i]`.  For example, if you have `[2, 3, 5, 5]`, return `[75, 50, 30, 30]`.  More info can be found at these links: [LeetCode](https://leetcode.com/problems/product-of-array-except-self/) and [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/a-product-array-puzzle/).
9. **Median of two sorted arrays:**  Given two sorted arrays as input, return the median of *all* values combined.  (Hint: you'll need binary search.)  For example, if you have `[1, 2, 2, 5, 8]` and `[5, 5, 8]`, return 5.  (The median is the middle value, or the average of the two middle values if you have an even number of entries.)  More info can be found here: [LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/) and [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/median-of-two-sorted-arrays-of-different-sizes/).
10. **Maximum sum rectangle in a 2-D matrix:** Given a 2-D matrix of values as input, return the maximum sum from any rectangle formed by taking a slice of the matrix.  For example, if you have `[[2, 3, 1],[0, -3, 1]]`, return 6 from `[2, 3, 1]`.  Links can be found here: [GeeksforGeeks](https://www.geeksforgeeks.org/dsa/maximum-sum-rectangle-in-a-2d-matrix/) and [LeetCode (variant)](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/).

## Official documentation for selected languages (where possible)
### Python
- Official Python documentation on lists: https://docs.python.org/3/tutorial/datastructures.html#more-on-lists
- Lists from W3 Schools: https://www.w3schools.com/python/python_lists.asp

### Java
- Overview of arrays from Java's official documentation: https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html
- Arrays from W3 Schools: https://www.w3schools.com/java/java_arrays.asp
- `ArrayList`s from Java 17: https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/ArrayList.html

### JavaScript
- MDN from Mozilla: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array
- Arrays from W3 schools: https://www.w3schools.com/js/js_arrays.asp
- More on arrays: https://javascript.info/array

### C#
- Arrays from Microsoft: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/arrays
- `ArrayList`s: https://learn.microsoft.com/en-us/dotnet/api/system.collections.arraylist?view=net-9.0

## Additional resources
- [GeeksforGeeks - arrays](https://www.geeksforgeeks.org/array-data-structure/)  
- [LeetCode array challenges](https://leetcode.com/problem-list/array/)   
- [educative.io - Java with a section on arrays](https://www.educative.io/courses/data-structures-coding-interviews-java)