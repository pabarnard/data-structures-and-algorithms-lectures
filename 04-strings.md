# Strings

A **string** is a sequence of characters typically used to represent text.  They consist of letters, numbers, punctuation symbols, spaces and/or other characters.  In many languages they are enclosed with double quotation marks like so: `"Hello world!"`.  Some languages allow you to define them in other ways, but it depends on each one.  For example, Python allows single quotes `''`, but not in Java as they're reserved for the `char` data type.

In most programming languages, strings are treated as *immutable* objects, which are items that cannot be changed after they're created.  (We'll cover mutable vs. immutable data in depth in a future lesson.)  Some languages provide mutable alternatives.

NOTE: This page, and many others, will be as language-agnostic as possible so that it's approachable regardless of the language(s) you use.

## Tips for solving string challenges
When working with string problems, here are some useful pointers:

- **Remember to use pseudocode and T-diagrams:** Think about the steps needed to solve the problem, one at a time.  Determine what variables, programming statements (e.g. loops, if statements), etc. are needed, and understand how your variables change.
- **Practice! Practice! Practice!** Solve problems early and often!  One does not become an expert overnight.
- **Understand immutability:** In languages like Java, Python, and C#, strings are immutable.  Operations like concatenation create new strings, which can affect performance.
- **Use efficient data structures:** For repeated modifications, use `StringBuilder` (Java, C#) or a list (Python) instead of naive concatenation (the `+` or a similar operation).
- **Leverage built-in methods:** Functions like `split`, `join`, `substring`, `replace`, and `find` can simplify solutions.  **WARNING:** Beware that some languages might have built-in methods for specific actions that might not be available in others or might have different names.  For example, Python has a method called `isalnum` that checks if a string only has numbers and letters and is at least one character long, but there is no equivalent method for JavaScript strings.
- **Hashing and frequency maps:** Use hash maps or arrays to track character counts (e.g. anagrams, palindromes).
- **Useful techniques:** Keep strategies like the sliding window and two-pointer technique in mind.  (We'll cover them in depth in a future lesson!)
- **Regular expressions:** From time to time this is actually the fastest way to validate or extract patterns.

## Sample problems (arranged from easy to difficult)

Do not try to solve all these at once.  Focus on one at a time, and take it slowly.  Make sure you understand the problem, the constraints, the inputs and outputs, and feel comfortable experimenting.  In an interview setting, you will be asked to explain your solution, so talk it out!

Please check the links out, as they explain the problems in much more detail, and they talk about the constraints, which are omitted here for brevity.

1. **Reverse a string:**  Given a string as input, return a new string that's the original string reversed.  For example, if you are given "edam", return "made".  A variant of this problem on LeetCode can be found here: https://leetcode.com/problems/reverse-string/description/
2. **Check if a string is a palindrome:** Given a string as input, return true if the string is a palindrome - in other words, return true if the string is the same forwards and backwards, and false otherwise.  For example, "dad" returns true, and "deer" returns false.  A variant of this challenge can be found here: https://leetcode.com/problems/valid-palindrome/description/
3. **Longest common prefix:** Given an array of strings as input, return the prefix (same common first letters) common to all entries, or an empty string if there is no common prefix.  For example, given ["green", "greed", "greet"], return "gree" as every entry starts with those letters in that order.  This problem can be found on LeetCode here: https://leetcode.com/problems/longest-common-prefix/description/
4. **Valid anagrams:** Given two strings as input, check if the first is an anagram of the other and vice versa.  For example, "add" and "dad" returns true, but "fine" and "nice" return false.  This problem can be found on LeetCode here: https://leetcode.com/problems/valid-anagram/description/  
5. **Find first unique character:** Given a string as input, return the first character from left to right that is found only once in the string, or return an empty string if no characters are unique.  For example, "good" returns "g" (at index 0), while "deed" returns "" (all characters are found twice or more).  A variant of this challenge can be found here: https://leetcode.com/problems/first-unique-character-in-a-string/description/.
6. **Count all palindromic substrings:** Given a string as input, return an integer representing the number of substrings that are palindromes.  This problem can be found at https://leetcode.com/problems/palindromic-substrings/description/.
7. **Word break:** Given a string and an array of words (strings) as input, return true if the string can be formed as a combination of any of the words.  For example, "blackberry" and ["berry","black"] returns true, while "applequal" and ["apple","equal"] returns false because no letters can overlap.  This problem can be found at https://leetcode.com/problems/word-break/description/
8. **Decode string:** Given a string with numbers, letters and square brackets as input, return the decoded string.  For example, "5[b]2[am]" returns "bbbbbamam", and "3[m4[ea]]" returns "meaeaeaeameaeaeaeameaeaeaea".  This problem can be found at https://leetcode.com/problems/decode-string/description/.
9. **Find all anagrams in a string:** Given two strings `a` and `b` as input, return an array of starting indices such that a substring of `a` starting at each index that has a length equal to the length of string `b` contains an anagram of all the letters in `b`.  For example, `a = "reer"` and `b = "er"` returns [0, 2], as at index 0 in `a`, the substring "re" is an anagram of "er", and at index 2 in `a`, the substring `er` is an anagram of the string b (`er`).  The problem can be found at https://leetcode.com/problems/find-all-anagrams-in-a-string/description/.
10. **Strange printer:** Given a string as input, return the number of turns required for a strange printer to print all the letters.  The printer can only print consecutive sequences of the same letter each turn.  For example, "baaa" returns 2.  This problem can be found at https://leetcode.com/problems/strange-printer/description/.

## Official documentation (where possible)

### Python
- Official Python 3 documentation on strings with useful methods: [https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str](https://docs.python.org/3/library/stdtypes.html#text-sequence-type-str), plus more info at [https://docs.python.org/3/library/string.html](https://docs.python.org/3/library/string.html)
- String methods from W3 Schools: [https://www.w3schools.com/python/python_ref_string.asp](https://www.w3schools.com/python/python_ref_string.asp)

### Java
- Official Java 17 documentation on the `String` class with useful methods: [https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/String.html)  
- `StringBuilder` (Java 17): [https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/StringBuilder.html](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/StringBuilder.html)

### JavaScript
- Mozilla MDN documentation on strings with useful methods: [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
- String methods from W3 schools: [https://www.w3schools.com/js/js_string_methods.asp](https://www.w3schools.com/js/js_string_methods.asp)

### C#
- String class from Microsoft with useful methods and other informaton: [https://learn.microsoft.com/en-us/dotnet/api/system.string](https://learn.microsoft.com/en-us/dotnet/api/system.string)
- `StringBuilder`: [https://learn.microsoft.com/en-us/dotnet/api/system.text.stringbuilder](https://learn.microsoft.com/en-us/dotnet/api/system.text.stringbuilder)

### C++
- `std::string`: [https://cplusplus.com/reference/string/string/](https://cplusplus.com/reference/string/string/)
- String Methods: [https://en.cppreference.com/w/cpp/string/basic_string](https://en.cppreference.com/w/cpp/string/basic_string)

## Additional resources
- [LeetCode string challenges](https://leetcode.com/tag/string/)  
- [GeeksforGeeks - String overview with more information](https://www.geeksforgeeks.org/string-data-structure/)  
- [HackerRank String challenges](https://www.hackerrank.com/domains/algorithms?filters%5Bsubdomains%5D%5B%5D=strings)