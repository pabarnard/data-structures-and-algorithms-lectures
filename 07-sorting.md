# Sorting
**Sorting** is the process of arranging data in a specified order.  Most of the time this means sorting in one of the following ways:
- Alphabetically from A to Z - or from Z to A
- Numerically from smallest to largest - or from largest to smallest
- Chronological order, i.e. from oldest to newest - or reverse chronological order, i.e. from newest to oldest

If you look at a page like [this one](https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population), which displays a table where you can sort countries by population, by name, by the date that the most recent estimate was obtained, etc., you will see the data sorted accordingly.  Below are some screenshots of the first few rows of data when sorted alphabetically and in reverse:
Starting with A:
![Image of first few countries sorted by population from A to Z](AlphabetSorted.png)
Starting with Z:
![Image of first few countries sorted by population from Z to A](ReverseAlphabetSorted.png)

## Sorting in place vs. returning a new object
Now that you're familiar with sorting in general, let's consider whether it is best to rearrange the data as is or return a new data structure with the sorted data.  

If you do NOT need to preserve the order of the original data, you can call on a sorting algorithm that rearranges the data **in place.**  Sorting in place means that a secondary data structure, like an array, is not required to store data temporarily during the sorting process.  Examples of sorting algorithms that sort in place are insertion sort and quick sort.  (We'll provide more info about the big O time and space complexity a little farther down.)

But if you need to keep the original, unsorted data as is and use a new data structure to hold the *sorted* data, then you can use a sorting algorithm that creates the new data structure and then sorts the data accordingly.  An example is the `sorted` function in Python, which takes an iterable (e.g. a list) as input and returns a new list with the data sorted.  Common scenarios for preserving the original data include dealing with raw database information, especially if it will be re-saved, and dealing with data from an API.

**It's important to read the documentation to understand which sorting methods return a _new_ data structure compared to those that rearrange the original data _in place_.**

## Stable sorts
A **stable sort** is a sorting algorithm that preserves the relative order of values that are the same.  To illustrate:

Imagine your original data looked like this:
```
["Two of hearts", "Three of clubs", "Five of spades", "Three of diamonds"]
```
Notice that there are two cards that are of the same rank - the three of clubs and three of diamonds.  If we decided to sort the cards in ascending order in terms of rank while keeping the sort stable, the result will be:
```
["Two of hearts", "Three of clubs", "Three of diamonds", "Five of spades"]
```
Notice how the three of clubs still comes before the three of diamonds - hence the relative order of items of equal value is preserved.  If the sort were not stable, it's possible you could get this instead:
```
["Two of hearts", "Three of diamonds", "Three of clubs", "Five of spades"]
```
Notice that the three of diamonds is now before the three of clubs, but the original data had the three of clubs before the three of diamonds.  So because the order of these two cards changed, this sorting mechanism is not stable.

Be on the lookout when checking documentation for sorting techniques if the algorithm is stable or not!

## Using built-in sort methods
Most, if not all, languages have a built-in sorting method or function:

### JavaScript
Arrays have a method called `sort`, which rearranges the original data and sorts it.  This is NOT done in place.  Note that by default JavaScript will convert all values that are NOT `undefined` into strings, and then sorts, so `[5, 10, 1]` would be sorted to `[1, 10, 5]` instead of `[1, 5, 10]`, as `10` comes before `5` when comparing strings in Unicode.  (Values that are `undefined`, along with empty values, get moved to the end.)

You can pass in a callback function to the array `sort` method that serves as a comparator function between the parameters `x` and `y`, which are items in the array, and it the callback should return a positive value if `x` comes after `y`, a negative value if `x` comes before `y`, and 0 or `NaN` if the values are equal.  For example:

```js
let originalData = [1, -3, 5, 8, 2];
let sortCallback = (x, y) => x - y; // Example: if x = 5 and y = 2, then x - y = 3 > 0, so 5 will come after 2
originalData.sort(sortCallback); // originalData should now be [-3, 1, 2, 5, 8];
```

If you need to preserve the original data, then you can use a relatively newer method for arrays called `toSorted` that will return a new array with the data sorted.  It works otherwise the same way as the `sort` method.

Note that both sorting methods are not necessarily guaranteed to be stable, and the big O time and space complexities will vary.

You can read up on the array `sort` method [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) and the array `toSorted` method [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/toSorted).

### Python
There is a standalone method called `sorted` that accepts an iterable as input - e.g. a list - along with additional parameters like a lambda function (an anonymous function) to describe how to sort - and it returns a new list with the data sorted accordingly.  By default numbers are sorted in ascending order, and letters are sorted, with all upper-case letters sorted first, then lower-case letters (e.g. `['A', 'B', 'a', 'b']`).

Lists have a built-in method called `sort` that sorts data *in place.*

Both the `sorted` function and `list.sort` method are *stable* sorts.

You can read up more on sorting in Python in general [here](https://docs.python.org/3/howto/sorting.html#sortinghowto) and the `sorted` method [here](https://docs.python.org/3/library/functions.html#sorted).

### Java
If you're looking to sort an array of data, you can use the `Arrays.sort` or `Arrays.parallelSort` static methods, both of which accept arrays of primitive values and arrays of Objects.  (If you need to leverage several threads, use the `parallelSort` method.)

In many cases, especially with ArrayLists, Sets, Maps and more, and even more so with your own classes, you will often use the `Collections.sort` method, perhaps in conjunction with the Comparable or Comparator interface to specify how to sort the data.

You can read up more from Baeldung on sorting [here](https://www.baeldung.com/java-sorting) and on the Comparator and Comparable interfaces [here](https://www.baeldung.com/java-comparator-comparable).

## Big O time with real-life sorting
Methods that allow you to sort data vary widely by language, and their implementation will also vary.  Most of the time the sorting algorithm will take up $O(n\log(n))$ time.  There will be rare occasions when it might take $O(n^2)$ time in the worst case scenario or $O(n)$ time in the best case, but these are very infrequent, so you can usually assume $O(n\log(n))$ time.  

## Types of sorts
We will not go over how all these sorting techniques work in depth; this is for your information.  Real-life sorts usually involve at least some fort of quick sort, merge sort, a hybrid of solutions or different sorting techniques altogether.

| Algorithm       | Best case        | Average case      | Worst case     | Space complexity   | Stable? | In place? |
|-----------------|------------------|-------------------|----------------|--------------------|---------|-----------|
| Bubble Sort     | $O(n)$           | $O(n^2)$          | $O(n^2)$       | $O(1)$             | Yes     | Yes       |
| Selection Sort  | $O(n^2)$         | $O(n^2)$          | $O(n^2)$       | $O(1)$             | No      | Yes       |
| Insertion Sort  | $O(n)$           | $O(n^2)$          | $O(n^2)$       | $O(1)$             | Yes     | Yes       |
| Merge Sort      | $O(n\log(n))$    | $O(n\log(n))$     | $O(n\log(n))$  | $O(n)$             | Yes     | No        |
| Quick Sort      | $O(n\log(n))$    | $O(n\log(n))$     | $O(n^2)$       | $O(\log(n))$       | No      | Yes       |
| Heap Sort       | $O(n\log(n))$    | $O(n\log(n))$     | $O(n\log(n))$  | $O(1)$             | No      | Yes       |
| Counting Sort   | $O(n + k)$       | $O(n + k)$        | $O(n + k)$     | $O(k)$             | Yes     | No        |
| Radix Sort      | $O(nk)$          | $O(nk)$           | $O(nk)$        | $O(n + k)$         | Yes     | No        |
| Bucket Sort     | $O(n + k)$       | $O(n + k)$        | $O(n^2)$       | $O(n + k)$         | Yes     | No        |

More info can be found at https://www.bigocheatsheet.com/.

You can also use VisuAlgo to view animations of most of these sorting techniques at https://visualgo.net/en/sorting.