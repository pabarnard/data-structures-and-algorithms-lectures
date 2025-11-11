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
In the example above, the sliding window is of fixed length.  However, many problems may have windows of varying length, such as finding the length of the longest subarray consisting of only unique values.  The general idea is this:
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
NOTE: The actual code will vary based on each problem, and you might update calculations elsewhere as needed.

## Two-pointer technique
Talk about two-pointer technique and talk about how you can expand to multiple pointers, especially for problems like linked lists and multidimensional data, like 2-D arrays

## Prefix sum

## Binary search

## Greedy algorithm
