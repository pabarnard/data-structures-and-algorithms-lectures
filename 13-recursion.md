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
        savedTerms for n = n;  SAVE the value
    } ELSE {
        savedTerms for n = fibonacci(n-2,savedTerms) + fibonacci(n-1,savedTerms);
    }
}
```
Notice the initial `if` statement, which checks to see if a value has already been calculated, and if so, just reuse it.  Also notice how we're passing the memo - `savedTerms` - along in the recursive step that holds the saved calculations.  DISCLAIMER: Some languages, like Java, do not allow you to create optional parameters like `savedTerms` in the pseudocode above, so you'd have to create the memos before the initial function call.

## Common approaches that may use recursion

### Divide and conquer

### Dynamic programming
Talk about top-down (recursion, usually with memoization) vs. bottom-up (iteration)

### Backtracking

## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

## Useful references