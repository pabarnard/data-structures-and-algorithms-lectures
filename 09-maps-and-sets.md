# Maps and sets

## Maps
A **map** is a collection of key-value pairs.  To use a real-life analogy, imagine that you have to call or text a friend.  That person will usually only have a single phone number.  So the key would be the phone number and the value would be the name of the person you want to talk to.  You can easily reverse it by making the key the person and the value the phone number.

Another analogy would be a person and their address.  You can define a key for the person and a value holding an address, or vice versa.  It's the same idea with capitals and countries.

Most languages have a built-in `Map` class or data structure, and some will have multiple variants, like `HashMap` and `TreeMap`.  Depending on the language, you might need to specify the types for the key and value, and other times you can directly add immediately without needing to specify.

Some languages allow you to use an object or dictionary, like this:
```
{
    "key": value
}
```
An important point of maps is that when you grab a value linked to a key, it's usually $O(1)$ time for hash maps where order doesn't matter or $O(\log(n))$ time for tree maps where the keys are saved in a specified order (e.g. numerically, alphabetically or a custom order), allowing for (relatively) instant look-ups regardless of the number of key-value pairs.  However, you use additional memory if a map is required, so there is a time-space tradeoff.

Some of you might be wondering if a list would be better than a map.  A list is better if you need to preserve insertion order, while it's not guaranteed in some implementations of maps.  Maps are better for instantaneous lookups as a whole than lists.

## Sets
A **set** is a collection of unique items.  For example, you could have a set of unique IDs from a database or an API.

Values can be added or removed from sets.  If you attempt to add a duplicate, the operation will not be allowed.

Like with maps, most languages will have a built-in `Set` class or data structure, and some will have multiple variants, like `HashSet` and `TreeSet`.  Depending on the language, you might be required to specify the data type for each item, and other times you can add or remove items of variable types.

You can find the intersection of two or more sets - i.e., the values common to all sets.  Also you can find the union of multiple sets - i.e. the values found in one or more of the sets in question.

Checking if a set contains a value is an $O(1)$ operation for hash sets (order doesn't matter) or an $O(\log(n))$ operation for tree sets (entries are sorted in a specified order).

Add or removing a value is an $O(1)$ or $O(\log(n))$ operation, depending on the implementation.

## Times to use a map vs. a set
A map is better for:
- Linking items and values together, e.g. license numbers and drivers.
- Frequency tracking, e.g. counting how many times a letter or character has been found.
- Duplicate values, especially if multiple items can be linked to the same value.

Use a set for:
- Tracking values we've found.
- Ensure uniqueness, especially in scenarios like looking for duplicate values.
- Finding values in common or not found in two or more sets of items.

Below is a useful table with brief explanations and use cases for various sets and maps:
| Implementation        | Underlying Structure | Time Complexity (Avg) | Time Complexity (Worst) | Ordered? | Allows Duplicates? | Common Languages / Classes | Use Cases |
|-----------------------|----------------------|------------------------|--------------------------|----------|--------------------|----------------------------|-----------|
| **HashSet / HashMap** | Hash Table           | O(1) insert/lookup     | O(n) (hash collisions)   | No       | No (keys unique)   | Java: `HashSet`, `HashMap` <br> Python: `set`, `dict` <br> JS: `Set`, `Map` <br> C++: `unordered_set`, `unordered_map` | Fast membership tests, frequency counting, caching |
| **TreeSet / TreeMap** | Balanced BST (e.g., Red-Black Tree) | O(log n) | O(log n) | Yes (sorted order) | No (keys unique) | Java: `TreeSet`, `TreeMap` <br> C++: `set`, `map` | Ordered data, range queries, in-order traversal |
| **LinkedHashSet / LinkedHashMap** | Hash Table + Linked List | O(1) | O(n) | Yes (insertion order) | No (keys unique) | Java: `LinkedHashSet`, `LinkedHashMap` | Preserving insertion order while keeping O(1) lookups |
| **Multiset / Multimap** | Hash Table or Tree | O(1) avg (hash) <br> O(log n) (tree) | O(n) (hash collisions) <br> O(log n) (tree) | Depends (unordered vs ordered) | Yes (duplicates allowed) | C++: `multiset`, `multimap` <br> Java: `Multimap` (Guava) | Counting frequencies, storing multiple values per key |
| **OrderedDict (Python)** | Hash Table + Linked List | O(1) | O(n) | Yes (insertion order) | No | Python: `collections.OrderedDict` | Maintaining insertion order with dictionary semantics |

Some key takeaways:
- **Hash-based** sets/maps are fastest on average but unordered.  
- **Tree-based** sets/maps guarantee order with O(log n) operations.  
- **LinkedHash** variants preserve **insertion order** while keeping O(1) lookups.  
- **Multisets/Multimaps** allow duplicates, useful for frequency-based problems.  
- Choosing the right implementation depends on whether you need **speed, order, or duplicates**.
- **Sets** ensure uniqueness, while **maps** associate keys with values.  
- Hash-based implementations are faster but unordered; tree-based are ordered but slower.  
- Many string and array problems reduce to **frequency counting** or **duplicate detection** using sets/maps.  
- Designing your own hash map or set is a **classic interview challenge**.

## Hashing
**Hashing** is the process of converting data into a sequence of characters.  A **hash function** is responsible for taking input data and returning a **hash value** or **hash code** representing the scrambled sequence.  The values are then saved in a **hash table** for fast look-up.  Many sets and maps utilize a hash function so that a key maps to a unique location in memory, and then value can be retrieved accordingly in the case of maps.

One thing to be careful about is the possibility of a **collision**, which occurs when two hashed keys point to the same item.  So hash functions should minimize the probability of collisions.

In most algorithm challenges, you likely won't need to write your own hash function, but there may be occasions when you need it.  Most of the time you'll instead utilize hash maps and hash sets without needing to worry about collisions and hash functions.

If you're going into security, you'll want to bone up on hashing algorithms, which is beyond the scope of this series.

## Sample problems (arranged from easy to difficult)
Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.  Do your best to solve these on your own first before you read the explanations or solutions!

Consider whether to use a set or map - or both - in these problems!  You might need additional techniques to help you solve these problems, especially the harder ones.

1. **Contains duplicate:** Given an array of numbers as input, return true if the array has a duplicate value and false otherwise.  You can practice this problem on LeetCode [here](https://leetcode.com/problems/contains-duplicate/).
2. **Intersection of two arrays:** Given two arrays of numbers as input, return a new array consisting of only *unique* values where each entry can be found in the two arrays.  For example, if you have `[3, 5, 1, 3, 4]` and `[2, 3, 3, 5, 8, 12]` as input, return `[3, 5]`.  Note that duplicates don't count.  This problem can be found on [LeetCode](https://leetcode.com/problems/intersection-of-two-arrays/).
3. **Valid anagram:** Given two strings as input, return true if the first string is an anagram of the second and false otherwise.  For example, `"bad"` and `"dab"` returns true, while `"door"` and `"room"` returns false.  More can be found on [LeetCode](https://leetcode.com/problems/valid-anagram/).
4. **Group anagrams:** Given an array of strings as input, return an array where each item is a subarray consisting of anagrams of the same sets of letters.  For example, given `["ram","mar","arm","dog","god","dot","tom","mot"]`, return `[["ram","mar","arm"],["dog","god"],["dot"],["tom","mot"]]`.  The arrays and entries can be in any order.  This can be practiced on [LeetCode](https://leetcode.com/problems/group-anagrams/).
5. **Longest substring without repeating characters:** You're given a string of characters as input.  Your goal is to return the length of the longest subtring consisting of unique characters.  For example, if you have `"bamanda", return 4 as the longest substring consisting of unique characters is `mand`.  You can try this problem on [LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/).
6. **Bulls and cows:** You're given two numbers as strings as input, the first representing the secret number and the second representing a guess.  You are to return a string of the form "xAyB", where "xA" means there are `x` digits in the guess that are in the secret and in the correct position, while "yB" means there are `y` digits in the guess that are in the secret number but in the wrong position.  For example, if you have a secret "13142" and a guess "01151", return "1A1B".  (Note that even though we have three 1's, the 1 in the middle of the guess is in the correct spot, but only a single of the remaining 1's can be used that's in the secret.)  You can practice here: [LeetCode](https://leetcode.com/problems/bulls-and-cows).
7. **Design a HashMap / HashSet:** You are to design a hash-based set or map from scratch with various methods.  You can find more info here on LeetCode: [Design HashMap](https://leetcode.com/problems/design-hashmap/) and [Design HashSet](https://leetcode.com/problems/design-hashset/).
8. **Minimum window substring:** You're given two strings as input: the first string `"x"` consists of a bunch of characters and the second `"y"` with a series of characters to find.  Your goal is to return the shortest substring in `"x"` such that it contains all the letters in `"y"` - including duplicates, or return `""` if none can be found.  For example, if you have `x = "BLUEGREEN"` and `y = "ELURE"`, return `"LUEGRE"`.  You can try this problem on [LeetCode](https://leetcode.com/problems/minimum-window-substring/).

## Documentation for sets and maps in various languages
- Documentation for hash sets and maps in Java: [HashSet](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashSet.html), [HashMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/HashMap.html), [TreeSet](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/TreeSet.html) and [TreeMap](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/TreeMap.html)
- Documentation of sets and dictionaries (effectively maps) in Python: [set](https://docs.python.org/3/library/stdtypes.html#set), [dict](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict)
- Documentation of sets and maps in JavaScript: [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set), [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
- Documentation of sets and maps in C#: [HashSet<T>](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1), [Dictionary<TKey,TValue>](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2) and [SortedSet<T> (effectively TreeSet<T>)](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.sortedset-1)