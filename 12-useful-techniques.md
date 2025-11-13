# Useful techniques

We're now going to focus on common strategies for solving algorithm challenges.  This page will focus on techniques that do NOT involve recursion.  The next section will cover recursion, along with common techniques use.

## Sliding window
A **sliding window** is a subset - or basically a portion - of a data structure and you only consider its contents inside.  It's used most in string and array challenges.  

Here's an illustration of a sliding window of size 3 for an array with 10 elements:
```
[1, 3, 5, 2, 4, 6, 1, 2, -3, 5]

[1, 3, 5, 2, 4, 6, 1, 2, -3, 5]
|_______|
    |
    |
[1, 3, 5]

[1, 3, 5, 2, 4, 6, 1, 2, -3, 5]
   |_______|
       |
       |
   [3, 5, 2]

[1, 3, 5, 2, 4, 6, 1, 2, -3, 5]
      |_______|
          |
          |
      [5, 2, 4]
```
We start off the window at the first three values, and then we move the window rightward, adding the newest value while removing the oldest one.  So in the example above, we start with `[1, 3, 5]`, then move rightward to `[3, 5, 2]`, then to `[5, 2, 4]`, then to `[2, 4, 6]`, etc. until we reach `[2, -3, 5]`.  

Here's some pseudocode to illustrate a *sliding window of fixed length `k`*:
```
FUNCTION problemToSolve() {
    CREATE variables holding relevant data for sliding window, including possibly a map or set for frequency count or unique values
    FOR first k values in item to iterate through (e.g. string, array) {
        Update variables as needed until the windo
    }
    FOR remaining values in item to iterate through {
        Remove leftmost (oldest) value
        Add newest value
        Update variables accordingly
    }
    RETURN desired result
}
```
In the example above, the sliding window is of fixed length.  

However, many problems may have windows of varying length, such as finding the length of the longest subarray consisting of only unique values.  The general idea is this in pseudocode:
```
FUNCTION problemToSolve() {
    CREATE variables holding relevant data for sliding window, including a variable denoting the left end of the sliding window (usually an index) and possibly maps and sets as needed
    FOR loop for moving the right end of the sliding window {
        UPDATE calculations and variables as needed
        WHILE current sliding window does not meet current requirements of problem {
            MOVE left end accordingly
            UPDATE calculations and variables as needed
        }
    }
    RETURN result
}
```
NOTE: When utilizing the sliding window, the actual code will vary based on each problem, and you might update calculations elsewhere as needed.

### Practice problems
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please follow the links to take a look at the problems in detail and tackle them on your own.  Do your best to solve these on your own first before you read the solutions!

- **Longest harmonious subsequence:** [LeetCode](https://leetcode.com/problems/longest-harmonious-subsequence/)
- **Maximum average subarray I:** [LeetCode](https://leetcode.com/problems/maximum-average-subarray-i/)
- **Repeated DNA sequences:** [LeetCode](https://leetcode.com/problems/repeated-dna-sequences/)
- **Longest substring without repeating characters:** [LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- **Maximum erasure value:** [LeetCode](https://leetcode.com/problems/maximum-erasure-value/)
- **Minimum window substring:** [LeetCode](https://leetcode.com/problems/minimum-window-substring/)

## Two-pointer technique
The **two-pointer technique** is a strategy where you keep track of two items at the same time.  It involves creating variables pointing to different items.  They could hold numerical indexes for locations in arrays and strings, or they could point to a specific node in a linked list or a similar data structure.  

Here's an illustration with an array by sorting with a selection sort: 
```
[5, 3, 2, 1, 8, 4, 10, 5, 2]

 |
 |
 v
[5, 3, 2, 1, 8, 4, 10, 5, 2]
 ^ 
 |
 |

    |
    |
    v
[5, 3, 2, 1, 8, 4, 10, 5, 2]
 ^
 |
 |

       |
       |
       v
[5, 3, 2, 1, 8, 4, 10, 5, 2]
 ^
 |
 |


          |
          |
          V
[5, 3, 2, 1, 8, 4, 10, 5, 2]
 ^
 |
 |

          |
          |
          V
[1, 3, 2, 5, 8, 4, 10, 5, 2]
 ^
 |
 |

    |
    |
    v
[1, 3, 2, 5, 8, 4, 10, 5, 2]
    ^
    |
    |
```
The pointer below the array is used to reference the item that will be swapped for the smallest possible item on the right.  The pointer above the array is used to search for the smallest value on the right.  (If there's a tie, the first instance of the smallest value is picked.)  Once values are swapped, then the pointer below the array moves down to the next value, with the pointer above the array pointing to the same value.

This is one such application of the two-pointer technique.  It comes up mostly in array, string and linked list problems.  In fact, you can actually extend this idea to multiple pointers to track multiple items at once.

### Practice problems
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please follow the links to take a look at the problems in detail and tackle them on your own.  Do your best to solve these on your own first before you read the solutions!

- **Valid palindrome:** [LeetCode](https://leetcode.com/problems/valid-palindrome/)
- **Move zeroes:** [LeetCode](https://leetcode.com/problems/move-zeroes/)
- **Three sum:** [LeetCode](https://leetcode.com/problems/3sum/)
- **Palindromic substrings:** [LeetCode](https://leetcode.com/problems/palindromic-substrings/)
- **Boats to save people:** [LeetCode](https://leetcode.com/problems/boats-to-save-people/)
- **Trapping rain water:** [LeetCode](https://leetcode.com/problems/trapping-rain-water/)

## Prefix sum
The **prefix sum** technique is an algorithm used to keep track of running sums so that one can calculate a subarray's sum regardless of its starting and ending indexes.  This technique also applies for keeping track of how many times a condition is met as we travel through a data structure, usually an array.  It is used a lot whenever there are a ton of calculations required.

Here's an illustration of using the prefix sum technique for an array:

```
sum = 0
array = [1, 2, 3, 4, 5, 6]
sums = []
// After first value
sum = 1
array = [1, 2, 3, 4, 5, 6]
sums = [1]
// After second value
sum = 3
array = [1, 2, 3, 4, 5, 6]
sumArray = [1, 3]
// After third value
sum = 6
array = [1, 2, 3, 4, 5, 6]
sumArray = [1, 3, 6]
// ...
// After final value
sum = 21
array = [1, 2, 3, 4, 5, 6]
sumArray = [1, 3, 6, 10, 15, 21]
```
Notice that we start at the beginning and create an array holding the sums, and then we have a variable holding a sum.  As we move through the original array, we save the cumulative sum each time.

The power of this techinques lies in trying to find the sum of any subarray.  Instead of requiring $O(n)$ time, it can be done in $O(1)$ time.  For example, if we wanted the sum of the values 3 through 5, inclusively, we'd only need to take the sum of 1-5 by using the sum array and then subtract the sum of just 1-2 from the sum array: so we'd get 15 - 3 = 12 without needing to loop again.  We just look up cumulative sums from the sum array.

This technique is not just used for sums.  It can be used for frequencies as well.  And it can also be used for sums *after (and possibly including)* the current entry - so a suffix sum - instead of just before (and possibly including) the current value. 

### Practice problems
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please follow the links to take a look at the problems in detail and tackle them on your own.  Do your best to solve these on your own first before you read the solutions!

- **Running sum of 1-D array**: [LeetCode](https://leetcode.com/problems/running-sum-of-1d-array/)
- **Find the highest altitude:** [LeetCode](https://leetcode.com/problems/find-the-highest-altitude/)
- **Ways to make a fair array:** [LeetCode](https://leetcode.com/problems/ways-to-make-a-fair-array/)
- **Zero array transformation I:** [LeetCode](https://leetcode.com/problems/zero-array-transformation-i/)
- **Subarray sum equals k**: [LeetCode](https://leetcode.com/problems/subarray-sum-equals-k/)
- **Find the original typed string II:** [LeetCode](https://leetcode.com/problems/find-the-original-typed-string-ii/)

## Binary search

## Greedy algorithm
