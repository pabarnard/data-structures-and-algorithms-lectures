# Recursion

**Recursion** is when a function makes a call to itself.  This concept is probably one of the most confusing out there in computer sciences.  

To illustrate recursion we will use factorials, which are products from multiplying 1, 2, 3, ..., up to $n$.  Multiplying these values together is called "n factorial", denoted $n! = n \times (n - 1) \times (n - 2) \times ... \times 3 \times 2 \times 1$.  For example, $5! = 5 \cdot 4 \cdot 3 \cdot 2 \cdot 1$.  $1! = 1$, and by definition, $0! = 1$.  

Here's how factorials are calculated with recursion:
```
FUNCTION factorial(value) {
    IF (value is 1 or 0) { // Base case
        RETURN 1;
    } ELSE {
        RETURN value * factorial(value-1); // Recursive step
    }
}
```
There are few important terms to know when it comes to recursion.  The first is the **call stack**, which is a stack of recursive function calls.  For example, when calculating `factorial(4)`, the call stack looks like this:

```
Initial call:
*********************
* factorial(4)      *
*********************

Next call:
*********************
* factorial(3)      *
*********************
* factorial(4)      *
*********************

Next call:
*********************
* factorial(2)      *
*********************
* factorial(3)      *
*********************
* factorial(4)      *
*********************

Next call:
*********************
* factorial(1)      *
*********************
* factorial(2)      *
*********************
* factorial(3)      *
*********************
* factorial(4)      *
*********************
```

For each additional call that's required, we take what's called the **recursive step**, which is when we invoke the function again.  At this point, when `factorial(1)` is called, we reach the **base case,** which is the stopping point for recursion.  This is when we return values and clear the call stack:
```
Call stack:
*********************
* factorial(1)      * ---> Returns 1
*********************
* factorial(2)      *
*********************
* factorial(3)      *
*********************
* factorial(4)      *
*********************

After returning 1:
*********************
* factorial(2)      * -> returns 2*factorial(1), or 2
*********************
* factorial(3)      *
*********************
* factorial(4)      *
*********************

After returning 2:
*********************
* factorial(3)      * -> returns 3*factorial(2), or 6
*********************
* factorial(4)      *
*********************

After returning 6:
*********************
* factorial(4)      * -> returns 4*factorial(3), or 24
*********************
```
Once the call stack is fully cleared, we return 24.

There's a limit to how many recursive calls you can make.  If the call stack gets too large, we run into **stack overflow**.  This occurs when the base case is never reached.

Here's a basic illustration of stack overflow:
```
FUNCTION countdown(n) {
    RETURN countdown(n-1);
}
```
Notice that we don't have a base case specified, so this will run until the call stack overflows.

**IMPORTANT:** Make sure at least one variable is changing value with each recursive call, otherwise stack overflow will occur!!

Recursion is used frequently when a problem needs to be broken down into smaller chunks (such as by dividing and conquering, which we'll talk about more a little later).  It's also used when trying to find an optimal value or a minimum or maximum when writing loops per se might not be sufficient.  Many tree and graph problems use recursion when it might be preferred over using a data structure like a stack for depth-first search or a queue for breadth-first search.

A real-life application for recursion is searching for files in multiple folders.  Here's an illustration:
```
/Documents
    /Budget
        /2023
            December.xlsx
        /2024
            January.xlsx
            February.xlsx
            notes.txt
    /Calendars
        workSchedule.xlsx
        planner.docx
    backlog.xlsx
```
If we search for all files with the extension `.xlsx` in the Documents folder, we find `backlog.xlsx` and two new subfolders: Budget and Calendars.  Then we recursively search those, and eventually we find five files total that have the `.xlsx` extension: December, January, February, workSchedule, and backlog.

## Pros and cons of recursion
Recursion is useful when a problem can easily be broken down into smaller chunks.  Applications include graph and tree data structures, where depth-first search (DFS) and breadth-first search (BFS) are used.  If you need to be very thorough and consider all possibilities without worry about time constraints, a well-written recursive algorithm is your best choice.

Recursion, however, can be dangerous.  There is the risk of stack overlow if there are too many calls and there is not enough optimization.  Additionally, using an iterative approach - such as a for loop - may prove much, much faster than recursion, especially if the iterative approach is as thorough as the recursive one.  

Many problems that are solved with loops can be written with a recursive algorithm, and vice versa.  So it's up to you to decide which way is best to tackle the problem in question.  One approach might be easier to code out; e.g. the statements used to program a for or while loop might not be very intuitive vs. writing a recursive solution, whereas sometimes the recursive approach might be overkill.

## Memoization
When writing a recursive solution, calculations often need to be saved so that they don't need to be repeated.  Imagine the Fibonacci sequence, which starts with the values 0 and 1, and each term afterwards is the sum of the last two values.  (Some sources start with the values 1 and 1 instead, but the sequence is otherwise the same.)  The sequence is defined like so:
$$
\begin{align*}
F_0 &= 0 \\
F_1 &= 1 \\
F_2 &= F_0 + F_1 = 0 + 1 = 1 \\
F_3 &= F_1 + F_2 = 1 + 1 = 2 \\
F_4 &= F_2 + F_3 = 1 + 2 = 3 \\
F_5 &= F_3 + F_4 = 2 + 3 = 5 \\
... \\
F_n &= F_{n-2} + F_{n-1}
\end{align*}
$$
A recursive approach would look like this:
```
FUNCTION fibonacci(n) {
    IF (n <= 1) {
        RETURN n;
    } ELSE {
        RETURN fibonacci(n-2) + fibonacci(n-1);
    }
}
```
For small integers $n$, this is perfectly fine.  Now imagine if $n$ were 40 or more.  For `fibonacci(40)`, you'd have to calculate `fibonacci(39)` and `fibonacci(38)`, and then for `fibonacci(39)` you'd need `fibonacci(38)` and `fibonacci(37)`, and for `fibonacci(38)` you'd need `fibonacci(37)` and `fibonacci(36)`.  Notice how we'd have to calculate `fibonacci(38)` and `fibonacci(37)` twice.  The problem here is that each of those would have to calculate the smaller terms, and it turns out the number of times each value is calculated would increase *exponentially*.  So natively this would be very inefficient!

Wouldn't it be nice if there were a way to save these calculations as we go?  It turns out there is!!  Memoization is our hero that will come to the rescue!  **Memoization** is the process of creating information as memos that will hold calculations already completed.  We will create a cache that will hold these memos.  These can be arrays, objects or anything that's mutable in most cases.  In our example of the Fibonacci sequence, we will use an object (dictionary):
```
FUNCTION fibonacci(n, savedTerms = {}) {
    IF (n is in savedTerms) {
        RETURN savedTerms value for n;
    }
    IF (n <= 1) {
        savedTerms for n = n; // SAVE the value
    } ELSE {
        savedTerms for n = fibonacci(n-2,savedTerms) + fibonacci(n-1,savedTerms);
    }
    RETURN savedTerms value for n;
}
```
Notice the initial `if` statement, which checks to see if a value has already been calculated, and if so, just reuse it.  Also notice how we're passing the memo - `savedTerms` - along in the recursive step that holds the saved calculations.  DISCLAIMER: Some languages, like Java, do not allow you to create optional parameters like `savedTerms` in the pseudocode above, so you'd have to create the memos before the initial function call.

## Common approaches that may use recursion
Recursion is used in a lot of ways to solve algorithm challenges.  We'll outline three common approaches: divide and conquer, backtracking, greedy algorithms, and dynamic programming (DP).

### Divide and conquer
Whenever a problem can be broken down into smaller subproblems that are the same or similar to the original problem in question, a common approach is to **divide and conquer** to obtain a solution.  This means *dividing* the problem into simpler and smaller chunks, none of which are overlapping, and each one can be solved *independently.*   These smaller problems are then broken down further as needed, usually recursively, until it can't be simplified any more.  Once the problem is broken down as much as possible, then each subproblem is solved, or *conquered*.  These independent solutions are then combined to form a unified answer to the overall original problem.

Dividing and conquering is used a lot when parallel computing is required.  Quicksort and merge sort use this strategy as well.  Searching for values that are in order - in other words, binary search - uses the divide and conquer technique to narrow the possibilities down each time.

### Backtracking
If you're given a problem that involves finding all possible valid solutions or you need to build out a solution as you go, backtracking can come in handy.  The **backtracking** technique involves going through possible answers, and if one answer is invalid, then all possible solutions that build from that are not correct as well, so you undo the most recent operation - or backtrack - and then try another candidate for an answer.  So try one possibility, keep exploring recursively until it is a valid answer, in which case we save or return it, or if we hit a roadblock where the candidate is now no longer a possible correct solution, we backtrack to the point where it's still valid and then move on to the next possibility.  Memoization is not often used as calculations are not repeated often, but you still need to keep track of progress as you go.

Backtracking is better than brute force in that we can prune, or eliminate, possible sets of answers that don't meet the conditions of the problem.

Examples of backtracking include generating all permutations of a series of numbers (e.g. all arrangements of `[1,2,3]` in an order), solving real-life puzzles like Sudoku, crosswords, the N-queens puzzle, and much more.

### Greedy algorithm
Whenever you are dealing with a problem that involves optimization, like finding the least coins needed to obtain a certain amount of change, you often need to make many decisions along the way.  If you choose to take the optimal choice every time - so take the best pick *locally* at that moment - you are working with a **greedy algorithm**, which involves obtaining a solution by making the best available decision at each step.  **IMPORTANT:** Note that a greedy algorithm will produce *a* solution, but it will NOT necessarily be the *globally* - as in overall - best solution.  Greedy algorithms are useful if you want to obtain a relatively quick solution if finding the best one would take too long, like in the traveling salesman problem, where a person must start at one city and visit the others exactly once before returning.

There are two important considerations when it comes to whether to pick a greedy algorithm:
1. **Optimal substructure:** If each subproblem has an optimal solution, then the globally best solution can be formed from the solutions to the subproblems.  For example, if you're looking for the shortest destination between cities A and E, and that route passes through cities B, C, and D, then along the same path the shortest distance between any pair of cities, such as B and E, C and D, etc. can be formed using the same route.  Notice how each subproblem - searching for the best route between any two cities - has an optimal solution.
2. **Greedy choice property:** For each step the algorithm makes the best choice at that moment *without considering the past or future*.  So the optimization is *local only*.

An example of a greedy algorithm would be the activity selection problem, where you're given a list of activities with start and end times, and your goal is to pick the most activities possible that don't overlap.  The way to solve this would be by picking the earliest activity by *finishing time*.  Another one would be finding the least coins needed to make a given amount based on an array of coin denominations.

If you find you want the globally optimal solution, dynamic programming might be the best way to go instead, where it's more thorough.  More on that below!

### Dynamic programming
When a problem can be broken down into smaller chunks that can be solved, dynamic programming is another approach to consider.  **Dynamic programming** is a technique that finds optimal solutions to smaller subproblems, often recursively, and these smaller chunks overlap (unlike divide and conquer, where there is no overlap), and the overall best solution can be constructed from the optimal solutions of the subproblems.  The solutions to the subproblems are stored to prevent duplicate calculations.  Examples include finding the longest common substring for any two strings, finding a term in the Fibonacci sequence, and calculating terms in Pascal's triangle.

There are two approaches to dynamic programming: top-down and bottom-up.  

The **top-down** approach entails starting with the overall problem and working down to smaller subproblems.  Usually recursion is used in conjunction with memoization to save previous calculations.  In the Fibonacci sequence via the top-down approach, you would start with the $n^{th}$ term, then move to the $(n-1)^{th}$ term, the $(n-2)^{th}$ term, etc. until you reach the simplest case.  

The **bottom-up** approach starts with the simplest case possible and then works up to the overall problem to be solved.  Usually iteration is utilization with a table of some sort (e.g. an array) to hold calculations.  Applying the bottom-up approach with the Fibonacci sequence would mean starting with the first and second terms, and then adding iteratively to obtain each successive term until the desired one is reached.

If you can come up with a bottom-up approach to a problem, it will usually be superior to the more intuitive top-down approach because it will usually be more - or at least just as - efficient in terms of space and time.

## General strategy for picking the right technique(s) to use to solve an algorithm challenge
When you have to tackle a problem that may involve recursion, it helps to break down the problem and identify which approaches work best.  Consider:
- **Divide and conquer:** The problem can be broken down into smaller subproblems that can be solved **independently** (no overlap).
- **Dynamic programming (DP):** The problem can be broken down into smaller suproblems that can be solved with overlap, and each subproblem has an optimal solution.  Consider whether a top-down approach with memoization or a bottom-up approach with tabulation is best.
- **Greedy algorithm:** If you want to obtain a solution as quickly as possible by picking the best one each step of the way, then this is your approach.  Note that the overall solution might not be optimal, and if you want the optimal solution, then divide and conquer or dynamic programming will suit you better than a greedy algorithm.
- **Backtracking:** If the problem asks you to find multiple solutions or make many decisions along the way, and you can eliminate possible sets of solutions as you go, then this is the best way to go.  Be careful as this is usually the slowest apporach.

Note that you want optimal substructure if you want to use divide and conquer or dynamic programming.  It may also apply for a greedy algorithm, provided that it yields optimal solutions at each step.

## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

Your goal is to figure out the best approach that will solve each challenge.  It might involve DP.  Maybe it's divide and conquer.  Practice early and often!

**TO BE ADDED**

## Useful references
- *Introduction to Algorithms* by Thomas Cormen, Charles Leiserson, Ronald Rivest, Clifford Stein - arguably one of the best books out there
- *Algorithm Design Manual* by Steven Skiena
- *Algorithms* by Robert Sedgewick and Kevin Wayne