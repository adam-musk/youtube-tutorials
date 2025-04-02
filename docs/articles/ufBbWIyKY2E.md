---
layout: "../../layouts/BlogPost.astro"
title: "JavaScript Algorithms and Coding Challenges: A Beginner's Guide"
pubDate: "2025-03-02 14:26:39.427507"
youtubeVideoID: "ufBbWIyKY2E"
index:
---

# JavaScript Algorithms and Coding Challenges: A Beginner's Guide

> No description provided.



<iframe width="100%" height="auto" style="aspect-ratio: 16/9; border: none;" src="https://www.youtube.com/embed/ufBbWIyKY2E" frameborder="0" allowfullscreen></iframe>

This chapter introduces fundamental JavaScript algorithms and coding challenge strategies, particularly relevant for coding interviews and building a strong foundation in programming.  We will explore ten essential JavaScript algorithm problems designed for beginners, mirroring the style of challenges encountered on platforms like LeetCode.

## Introduction to Algorithm Challenges

This course, brought to you by mkar from Coding Monkey, aims to equip you with the skills to confidently tackle coding interview questions at leading technology companies.  We will focus on building a solid understanding of JavaScript algorithms through practical examples and step-by-step solutions. These exercises are designed for absolute beginners and will not only enhance your coding abilities but also prepare you for technical interviews at Big Tech companies, where starting salaries can be substantial.

Let's begin our journey into the world of JavaScript algorithms!

## 1. Reversing Strings and Integers

Reversing a string or an integer is a classic coding interview question.  It tests your understanding of basic data manipulation and algorithmic thinking.

### 1.1 Reversing a String

**Problem:** Given a string, return a new string with the characters in reverse order.

**Examples:**

*   Input: "coding money"
*   Output: "yenom gnidoc"

Let's explore several approaches to solve this problem.

#### 1.1.1 Using a Traditional `for` Loop

One way to reverse a string is by iterating through it character by character and building the reversed string incrementally.

```javascript
function reverseStringForLoop(str) {
  let reversed = '';
  for (let i = 0; i < str.length; i++) {
    reversed = str[i] + reversed;
  }
  return reversed;
}

console.log(reverseStringForLoop("coding money")); // Output: yenom gnidoc
```

In this approach:

*   We initialize an empty string variable `reversed`.
*   The `for` loop iterates from the first character to the last character of the input string `str`.
*   In each iteration, we prepend the current character `str[i]` to the `reversed` string.
*   Finally, we return the `reversed` string.

While functional, this traditional `for` loop involves several moving parts (initialization, condition, incrementer), which can be prone to errors.

#### 1.1.2 Using a `for...of` Loop (Modern JavaScript Syntax)

A cleaner and more readable approach in modern JavaScript is to use the `for...of` loop, which simplifies iteration over iterable objects like strings.

```javascript
function reverseStringForOfLoop(str) {
  let reversed = '';
  for (const char of str) {
    reversed = char + reversed;
  }
  return reversed;
}

console.log(reverseStringForOfLoop("coding money")); // Output: yenom gnidoc
```

This `for...of` loop achieves the same result as the traditional `for` loop but with more concise syntax.  It iterates directly over the characters of the string, making the code easier to understand and less error-prone.

#### 1.1.3 Using Built-in JavaScript Methods: `split()`, `reverse()`, and `join()`

JavaScript provides built-in methods that offer a more elegant and efficient way to reverse a string. These methods leverage the power of array manipulation.

```javascript
function reverseStringBuiltIn(str) {
  return str.split('').reverse().join('');
}

console.log(reverseStringBuiltIn("coding money")); // Output: yenom gnidoc
```

Let's break down this one-line solution:

*   **`split('')`**: The `split('')` method converts the string into an array of individual characters.  Passing an empty string as the separator ensures each character becomes a separate element in the array.

    > **`split()`**:  This JavaScript string method divides a String into an ordered list of substrings, puts these substrings into an array, and returns the array. The splitting is done by searching for a pattern.

*   **`reverse()`**: The `reverse()` method, applied to the array, reverses the order of elements in the array *in place*.

    > **`reverse()`**: This JavaScript array method reverses an array *in place*. The first array element becomes the last, and the last array element becomes the first.

*   **`join('')`**: The `join('')` method converts the reversed array back into a string.  Passing an empty string as the argument concatenates the array elements without any separator in between.

    > **`join()`**: This JavaScript array method creates and returns a new string by concatenating all of the elements in an array (or an array-like object), separated by commas or a specified separator string.

This method is concise and leverages JavaScript's built-in functionalities, making it a highly efficient approach for reversing strings.

**Note:** While built-in methods offer convenience, interviewers may sometimes restrict their use to assess your understanding of fundamental algorithms. Therefore, understanding the `for` loop and `for...of` loop approaches is crucial.

### 1.2 Reversing an Integer

**Problem:** Given an integer, return the integer with its digits reversed.

**Examples:**

*   Input: 15
*   Output: 51
*   Input: -15
*   Output: -51

Building upon our string reversal knowledge, we can easily reverse an integer. The core idea is to convert the integer to a string, reverse the string, and then convert it back to an integer.

```javascript
function reverseInteger(n) {
  const reversedString = n.toString().split('').reverse().join('');
  let reversedInteger = parseInt(reversedString);

  // Handle negative sign
  reversedInteger = reversedInteger * Math.sign(n);
  return reversedInteger;
}

console.log(reverseInteger(15));   // Output: 51
console.log(reverseInteger(-15));  // Output: -51
```

Let's break down the `reverseInteger` function:

*   **`n.toString()`**: Converts the input integer `n` into a string.
*   **`.split('').reverse().join('')`**: Reverses the string representation of the integer using the same string reversal technique we learned earlier.
*   **`parseInt(reversedString)`**: Converts the reversed string back into an integer.

    > **`parseInt()`**: This JavaScript function parses a string and returns an integer.

*   **`Math.sign(n)`**:  This is crucial for handling negative numbers. `Math.sign(n)` returns 1 if `n` is positive, -1 if `n` is negative, and 0 if `n` is zero.  Multiplying the reversed integer by `Math.sign(n)` ensures that the sign of the original integer is preserved in the reversed integer.

    > **`Math.sign()`**: This JavaScript Math method returns the sign of a number, indicating whether the number is positive, negative, or zero.

This approach effectively reverses both positive and negative integers.

## 2. Palindrome Check

**Problem:** Given a string, return `true` if the string is a palindrome, or `false` if it is not.

**Definition:** A palindrome is a string that reads the same forwards and backward.

**Examples:**

*   "kayak" is a palindrome (true)
*   "madam" is a palindrome (true)
*   "coding money" is not a palindrome (false)

Leveraging our string reversal skills, checking for a palindrome becomes straightforward.

```javascript
function isPalindrome(str) {
  const reversedStr = str.split('').reverse().join('');
  return str === reversedStr;
}

console.log(isPalindrome("kayak"));        // Output: true
console.log(isPalindrome("coding money")); // Output: false
```

In this function:

*   We reverse the input string `str` using `split('').reverse().join('')` and store it in `reversedStr`.
*   We then directly compare the original string `str` with the reversed string `reversedStr`.
*   If they are identical, the function returns `true` (it's a palindrome); otherwise, it returns `false`.

This solution is concise and efficient due to the reuse of our string reversal logic.

**Homework/Further Exploration:**

*   **Two-Pointer Technique:** Research and implement a palindrome check using the two-pointer technique. This method avoids creating a reversed string and can be more efficient in certain scenarios.
*   **`every()` Method:** Explore and utilize the JavaScript `every()` array method to solve the palindrome problem.

    > **`every()`**: This JavaScript array method tests whether all elements in the array pass the test implemented by the provided function. It returns a Boolean value.

## 3. Finding the Most Common Character in a String

**Problem:** Given a string, return the character that appears most frequently in the string.

**Examples:**

*   Input: "abcccde"
*   Output: "c"
*   Input: "11223333"
*   Output: "3"

This problem introduces the concept of character frequency analysis and utilizes data structures to efficiently count character occurrences.

### 3.1 Using a Character Map (Object)

To solve this, we can use a character map (implemented as a JavaScript object) to store the count of each character in the string.

```javascript
function mostFrequentChar(str) {
  const charMap = {};

  for (const char of str) {
    charMap[char] = charMap[char] + 1 || 1;
  }

  let maxCount = 0;
  let maxChar = '';

  for (const char in charMap) {
    if (charMap[char] > maxCount) {
      maxCount = charMap[char];
      maxChar = char;
    }
  }

  return maxChar;
}

console.log(mostFrequentChar("abcccde"));   // Output: c
console.log(mostFrequentChar("11223333"));  // Output: 3
```

Let's break down the `mostFrequentChar` function:

1.  **Character Map Creation (`charMap` Object):**
    *   We initialize an empty object `charMap` to store character counts.
    *   We iterate through each character `char` in the input string `str` using a `for...of` loop.
    *   For each character:
        *   `charMap[char] = charMap[char] + 1 || 1;` This line efficiently updates the count in the `charMap`.
            *   `charMap[char] + 1`: If the character `char` already exists as a key in `charMap`, we increment its existing count by 1.
            *   `|| 1`: If `charMap[char]` is `undefined` (meaning the character is encountered for the first time), the `|| 1` (OR operator) sets the initial count to 1.

2.  **Finding the Maximum Count and Character:**
    *   We initialize `maxCount` to 0 and `maxChar` to an empty string to track the highest count and corresponding character.
    *   We iterate through the keys (characters) of the `charMap` object using a `for...in` loop.

        > **`for...in` loop**: This JavaScript loop iterates over all enumerable string properties of an object.

    *   For each character `char` in `charMap`:
        *   `if (charMap[char] > maxCount)`: We check if the count of the current character `charMap[char]` is greater than the current `maxCount`.
        *   If it is, we update `maxCount` to the new higher count and `maxChar` to the character `char`.

3.  **Returning the Most Frequent Character:**
    *   Finally, we return `maxChar`, which holds the character with the highest frequency.

This approach effectively counts character frequencies using an object as a character map and then iterates through the map to find the character with the maximum count.

**Alternative Data Structure: `Map`**

JavaScript also offers the `Map` data structure, which is similar to objects but can be more suitable for certain scenarios.  `Map` keys can be of any data type, and it maintains the insertion order of elements. While objects are sufficient for this problem, `Map` is worth noting as another option for character mapping.

> **`Map`**: The `Map` object in JavaScript is a collection of key-value pairs where keys and values can be of any data type. Maps remember the original insertion order of the keys.

## 4. Array Chunking

**Problem:** Given an array and a chunk size, divide the array into many subarrays where each subarray is of length `size`.

**Examples:**

*   Array: `[1, 2, 3, 4, 5]` , Chunk Size: `2`
    Output: `[[1, 2], [3, 4], [5]]`
*   Array: `[1, 2, 3, 4, 5, 6, 7, 8]` , Chunk Size: `3`
    Output: `[[1, 2, 3], [4, 5, 6], [7, 8]]`

This problem involves array manipulation and demonstrates the concept of dividing a larger data structure into smaller, manageable pieces.

### 4.1 Iterative Approach with `slice()` and `push()`

We can solve this problem iteratively by using a `while` loop and the `slice()` method to extract chunks from the original array.

```javascript
function chunkArray(array, size) {
  const chunkedArray = [];
  let index = 0;

  while (index < array.length) {
    chunkedArray.push(array.slice(index, index + size));
    index += size;
  }

  return chunkedArray;
}

console.log(chunkArray([1, 2, 3, 4, 5], 2));      // Output: [[1, 2], [3, 4], [5]]
console.log(chunkArray([1, 2, 3, 4, 5, 6, 7, 8], 3)); // Output: [[1, 2, 3], [4, 5, 6], [7, 8]]
```

Let's understand the `chunkArray` function:

1.  **Initialization:**
    *   `chunkedArray = []`: We create an empty array `chunkedArray` to store the resulting subarrays (chunks).
    *   `index = 0`: We initialize an `index` variable to 0. This `index` will track our current position in the original `array`.

2.  **`while` Loop for Chunking:**
    *   `while (index < array.length)`: The `while` loop continues as long as our `index` is within the bounds of the original `array`. This ensures we process the entire array.
    *   `chunkedArray.push(array.slice(index, index + size))`:
        *   `array.slice(index, index + size)`:  The `slice()` method extracts a portion of the `array` starting from `index` up to (but not including) `index + size`. This creates a chunk of the desired `size`.
        *   `chunkedArray.push(...)`: We use the `push()` method to add this extracted chunk (subarray) to our `chunkedArray`.

        > **`push()`**: This JavaScript array method adds one or more elements to the end of an array and returns the new length of the array.

    *   `index += size`: We increment the `index` by `size`. This moves our starting position in the original `array` forward by the chunk size, preparing for the extraction of the next chunk.

3.  **Returning the Chunked Array:**
    *   `return chunkedArray`: After the `while` loop completes (we've processed the entire `array`), we return the `chunkedArray` containing all the subarrays (chunks).

This iterative approach effectively divides the input array into chunks of the specified size.  The `slice()` method plays a key role in extracting portions of the array, and the `while` loop ensures we process the entire array.

## 5. Capitalizing the First Letter of Each Word

**Problem:** Write a function that accepts a string and capitalizes the first letter of each word in the string.

**Examples:**

*   Input: "i want to open the five tile case"
*   Output: "I Want To Open The Five Tile Case"

This problem focuses on string manipulation and word-level processing.

### 5.1 Iterative Approach with `split()`, `slice()`, and `join()`

One way to capitalize the first letter of each word is to split the string into words, capitalize the first letter of each word individually, and then join them back into a string.

```javascript
function capitalizeWords(str) {
  const words = str.split(' ');
  const capitalizedWords = [];

  for (const word of words) {
    capitalizedWords.push(word.charAt(0).toUpperCase() + word.slice(1));
  }

  return capitalizedWords.join(' ');
}

console.log(capitalizeWords("i want to open the five tile case"));
// Output: I Want To Open The Five Tile Case
```

Let's break down the `capitalizeWords` function:

1.  **Splitting the String into Words:**
    *   `words = str.split(' ')`: We use the `split(' ')` method to split the input string `str` into an array of words, using a space (" ") as the delimiter.

2.  **Capitalizing Each Word:**
    *   `capitalizedWords = []`: We initialize an empty array `capitalizedWords` to store the capitalized words.
    *   `for (const word of words)`: We iterate through each `word` in the `words` array.
    *   `capitalizedWords.push(word.charAt(0).toUpperCase() + word.slice(1))`:
        *   `word.charAt(0).toUpperCase()`:
            *   `word.charAt(0)`: Extracts the first character of the `word`.

            > **`charAt()`**: This JavaScript string method returns the character at a specified index (position) in a string.

            *   `.toUpperCase()`: Converts the first character to uppercase.

            > **`toUpperCase()`**: This JavaScript string method converts a string to uppercase.

        *   `word.slice(1)`: Extracts the rest of the word, starting from the second character (index 1) to the end.

        > **`slice()`**: This JavaScript string method extracts a section of a string and returns it as a new string, without modifying the original string.

        *   `... + ...`: We concatenate the capitalized first character with the rest of the word.
        *   `capitalizedWords.push(...)`: We push the capitalized word into the `capitalizedWords` array.

3.  **Joining the Capitalized Words Back into a String:**
    *   `return capitalizedWords.join(' ')`: We use the `join(' ')` method to join the words in the `capitalizedWords` array back into a single string, using a space (" ") as the separator.

This approach iterates through each word, capitalizes its first letter, and reconstructs the sentence, effectively capitalizing the first letter of every word.

### 5.2 Using `map()` for a More Concise Solution

The `map()` array method provides a more concise way to achieve the same result.  `map()` creates a new array by calling a provided function on every element in the calling array.

```javascript
function capitalizeWordsMap(str) {
  return str.split(' ')
            .map(word => word.charAt(0).toUpperCase() + word.slice(1))
            .join(' ');
}

console.log(capitalizeWordsMap("i want to open the five tile case"));
// Output: I Want To Open The Five Tile Case
```

In this `map`-based solution:

*   `str.split(' ')`:  We split the string into an array of words, as before.
*   `.map(word => word.charAt(0).toUpperCase() + word.slice(1))`: We use the `map()` method to process each `word` in the array.
    *   `word => ...`: This is an arrow function that takes each `word` as input.
    *   `word.charAt(0).toUpperCase() + word.slice(1)`:  This is the same logic we used in the `for...of` loop to capitalize the first letter and combine it with the rest of the word. `map()` applies this transformation to each word in the array.
*   `.join(' ')`: We join the resulting array of capitalized words back into a string.

This `map()` solution is functionally equivalent to the `for...of` loop version but is more compact and often considered more idiomatic JavaScript for array transformations.

## 6. Anagram Check

**Problem:** Write a function to determine if two provided strings are anagrams of each other.

**Definition:** Two strings are anagrams if they contain the same characters with the same frequencies, disregarding spaces, punctuation, and case.

**Examples:**

*   "coding money", "money coding" -> true
*   "rail safety", "fairy tales" -> true
*   "hello", "olleh" -> true
*   "hello", "olleho" -> false

### 6.1 Character Map Comparison Approach

One approach to check for anagrams is to build character maps for both strings and then compare these maps for equality.

```javascript
function areAnagrams(stringA, stringB) {
  const charMapA = buildCharMap(stringA);
  const charMapB = buildCharMap(stringB);

  if (Object.keys(charMapA).length !== Object.keys(charMapB).length) {
    return false; // Different number of unique characters cannot be anagrams
  }

  for (const char in charMapA) {
    if (charMapA[char] !== charMapB[char]) {
      return false; // Character counts don't match
    }
  }

  return true; // Character maps are identical, strings are anagrams
}

function buildCharMap(str) {
  const charMap = {};
  const cleanedStr = str.toLowerCase().replace(/[^a-z0-9]/g, '');

  for (const char of cleanedStr) {
    charMap[char] = charMap[char] + 1 || 1;
  }

  return charMap;
}

console.log(areAnagrams("coding money", "money coding")); // Output: true
console.log(areAnagrams("rail safety", "fairy tales"));   // Output: true
console.log(areAnagrams("hello", "olleho"));        // Output: false
```

Let's analyze the `areAnagrams` function and the helper function `buildCharMap`:

1.  **`buildCharMap(str)` Helper Function:**
    *   `const charMap = {}`: Initializes an empty object `charMap` to store character counts.
    *   `const cleanedStr = str.toLowerCase().replace(/[^a-z0-9]/g, '')`:
        *   `str.toLowerCase()`: Converts the input string to lowercase to handle case-insensitivity.
        *   `.replace(/[^a-z0-9]/g, '')`:  Removes non-alphanumeric characters (spaces, punctuation, etc.) using a regular expression.

            > **Regular Expression**: `/[^a-z0-9]/g`
            >
            > *   `[...]`: Character set.
            > *   `^`: Inside a character set, `^` negates the set, meaning "match any character that is *not* in this set".
            > *   `a-z0-9`:  Matches lowercase letters 'a' through 'z' and digits '0' through '9'.
            > *   `[^a-z0-9]`: Matches any character that is *not* a lowercase letter or digit.
            > *   `/g`:  The global flag. It means "find all matches" rather than stopping after the first match.

        *   `.replace(..., '')`: Replaces all matches found by the regular expression with an empty string, effectively removing them.
    *   `for (const char of cleanedStr)`: Iterates through each character in the `cleanedStr`.
    *   `charMap[char] = charMap[char] + 1 || 1`: Updates the character count in `charMap`, as explained in the "Most Common Character" section.
    *   `return charMap`: Returns the completed character map.

2.  **`areAnagrams(stringA, stringB)` Function:**
    *   `const charMapA = buildCharMap(stringA)`: Creates a character map for `stringA` using `buildCharMap`.
    *   `const charMapB = buildCharMap(stringB)`: Creates a character map for `stringB` using `buildCharMap`.
    *   `if (Object.keys(charMapA).length !== Object.keys(charMapB).length)`: Checks if the number of unique characters (keys in the character maps) is different. If so, they cannot be anagrams, and we return `false`.

        > **`Object.keys()`**: This JavaScript method returns an array of a given object's own enumerable property names, iterated in the same order as a normal loop.

    *   `for (const char in charMapA)`: Iterates through the keys (characters) of `charMapA`.
    *   `if (charMapA[char] !== charMapB[char])`: For each character, it checks if its count in `charMapA` is different from its count in `charMapB`. If counts don't match for any character, they are not anagrams, and we return `false`.
    *   `return true`: If all checks pass (same number of unique characters and matching counts for each character), the strings are anagrams, and we return `true`.

This character map comparison approach is robust and correctly handles spaces, punctuation, and case differences.

### 6.2 Sorted String Comparison Approach

A simpler and more intuitive approach is to sort both strings alphabetically and then compare the sorted strings. If the sorted strings are identical, they are anagrams.

```javascript
function areAnagramsSorted(stringA, stringB) {
  return cleanString(stringA) === cleanString(stringB);
}

function cleanString(str) {
  return str.toLowerCase().replace(/[^a-z0-9]/g, '').split('').sort().join('');
}

console.log(areAnagramsSorted("coding money", "money coding")); // Output: true
console.log(areAnagramsSorted("rail safety", "fairy tales"));   // Output: true
console.log(areAnagramsSorted("hello", "olleho"));        // Output: false
```

Let's examine the `areAnagramsSorted` function and the helper function `cleanString`:

1.  **`cleanString(str)` Helper Function:**
    *   `str.toLowerCase().replace(/[^a-z0-9]/g, '')`: Cleans the string by converting to lowercase and removing non-alphanumeric characters, just like in `buildCharMap`.
    *   `.split('')`: Splits the cleaned string into an array of characters.
    *   `.sort()`: Sorts the array of characters alphabetically *in place*.
    *   `.join('')`: Joins the sorted array of characters back into a string.
    *   `return ...`: Returns the cleaned and sorted string.

2.  **`areAnagramsSorted(stringA, stringB)` Function:**
    *   `cleanString(stringA) === cleanString(stringB)`: It calls `cleanString` on both `stringA` and `stringB` to get their cleaned and sorted versions.
    *   It then directly compares the two cleaned and sorted strings using strict equality (`===`). If they are identical, it returns `true` (anagrams); otherwise, `false`.

This sorted string comparison approach is remarkably simple and effective. Sorting ensures that anagrams will have the same character order, making direct string comparison a valid anagram check.

## 7. Counting Vowels in a String

**Problem:** Write a function that returns the number of vowels (a, e, i, o, u) used in a given string.

**Examples:**

*   Input: "Coding Money"
    Output: 4 (o, i, o, e)
*   Input: "How are you?"
    Output: 5 (o, a, e, o, u)

### 7.1 Regular Expression Approach

The most concise way to count vowels is using regular expressions.

```javascript
function countVowelsRegex(str) {
  const matches = str.toLowerCase().match(/[aeiou]/gi);
  return matches ? matches.length : 0;
}

console.log(countVowelsRegex("Coding Money")); // Output: 4
console.log(countVowelsRegex("How are you?")); // Output: 5
```

Let's understand the `countVowelsRegex` function:

*   `str.toLowerCase()`: Converts the input string to lowercase for case-insensitive vowel counting.
*   `.match(/[aeiou]/gi)`:  Uses the `match()` method with a regular expression to find all vowels.

    > **Regular Expression**: `/[aeiou]/gi`
    >
    > *   `[...]`: Character set.
    > *   `aeiou`: Matches any of the vowels 'a', 'e', 'i', 'o', 'u'.
    > *   `/g`:  The global flag (find all matches).
    > *   `/i`:  The case-insensitive flag (match both uppercase and lowercase vowels).

*   `matches ? matches.length : 0`: This is a ternary operator to handle cases where no vowels are found.
    *   `matches`: If `match()` finds vowels, it returns an array of matches (stored in `matches`). In a conditional context, an array is truthy.
    *   `matches.length`: If `matches` is truthy (an array of matches), we return the `length` of the array, which is the count of vowels.
    *   `0`: If `match()` finds no vowels, it returns `null`. In a conditional context, `null` is falsy. If `matches` is falsy (null), we return 0 (no vowels found).

This regular expression approach is efficient and elegant for vowel counting.

### 7.2 Iterative Approach with `includes()`

An alternative approach without regular expressions is to iterate through the string and check if each character is a vowel using the `includes()` method on a vowel string.

```javascript
function countVowelsIterative(str) {
  const vowelSet = "aeiou";
  let count = 0;

  for (const char of str.toLowerCase()) {
    if (vowelSet.includes(char)) {
      count++;
    }
  }

  return count;
}

console.log(countVowelsIterative("Coding Money")); // Output: 4
console.log(countVowelsIterative("How are you?")); // Output: 5
```

Let's break down the `countVowelsIterative` function:

*   `const vowelSet = "aeiou"`:  Creates a string `vowelSet` containing all lowercase vowels.
*   `let count = 0`: Initializes a `count` variable to 0 to track the number of vowels.
*   `for (const char of str.toLowerCase())`: Iterates through each character in the lowercase version of the input string.
*   `if (vowelSet.includes(char))`:
    *   `vowelSet.includes(char)`: Checks if the current character `char` is present in the `vowelSet` string.

        > **`includes()`**: This JavaScript string method determines whether one string may be found within another string, returning `true` or `false` as appropriate.

    *   If `includes()` returns `true` (the character is a vowel), we increment the `count`.
*   `return count`: Returns the final vowel `count`.

This iterative approach, using `includes()`, provides a clear and understandable way to count vowels without relying on regular expressions.

## 8. FizzBuzz

**Problem:** Write a program that console logs the numbers from 1 to `n`. For multiples of 3, print "Fizz" instead of the number. For multiples of 5, print "Buzz". For multiples of both 3 and 5, print "FizzBuzz".

**Example (n = 15):**

```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
```

FizzBuzz is a classic programming problem often used in coding interviews to assess basic conditional logic and modulo operator understanding.

### 8.1 Solution with Modulo Operator and Conditional Logic

```javascript
function fizzBuzz(n) {
  for (let i = 1; i <= n; i++) {
    if (i % 3 === 0 && i % 5 === 0) {
      console.log("FizzBuzz");
    } else if (i % 3 === 0) {
      console.log("Fizz");
    } else if (i % 5 === 0) {
      console.log("Buzz");
    } else {
      console.log(i);
    }
  }
}

fizzBuzz(15); // Runs FizzBuzz for n = 15
```

Let's break down the `fizzBuzz` function:

1.  **`for` Loop for Numbers 1 to `n`:**
    *   `for (let i = 1; i <= n; i++)`: A `for` loop iterates through numbers from 1 to `n` (inclusive).

2.  **Conditional Logic (if/else if/else):**
    *   `if (i % 3 === 0 && i % 5 === 0)`: Checks if the current number `i` is divisible by both 3 and 5.
        *   `i % 3 === 0`: Checks if `i` is a multiple of 3 using the modulo operator.

            > **Modulo Operator (%)**: The modulo operator returns the remainder of a division. If `a % b === 0`, it means `a` is perfectly divisible by `b` with no remainder.

        *   `i % 5 === 0`: Checks if `i` is a multiple of 5.
        *   `&&`: Logical AND operator. The condition is true only if both `i % 3 === 0` and `i % 5 === 0` are true.
        *   If true, it `console.log("FizzBuzz")`.
    *   `else if (i % 3 === 0)`: If the previous condition is false, this checks if `i` is divisible by 3.
        *   If true, it `console.log("Fizz")`.
    *   `else if (i % 5 === 0)`: If both previous conditions are false, this checks if `i` is divisible by 5.
        *   If true, it `console.log("Buzz")`.
    *   `else`: If none of the above conditions are true (not divisible by 3 or 5), it `console.log(i)` (prints the number itself).

The order of the `if` and `else if` conditions is crucial. We must check for divisibility by both 3 and 5 *first* because a number divisible by both is also divisible by 3 and divisible by 5 individually. If we checked for divisibility by 3 or 5 first, we would never reach the "FizzBuzz" condition for numbers like 15.

## 9. Step Shape Pattern

**Problem:** Write a function that accepts a positive number `n` and console logs a step shape with `n` levels using the pound character (`#`). The step should have spaces on the right-hand side.

**Examples (n = 3):**

```
#
##
###
```

### 9.1 Nested Loop Approach

We can create the step shape using nested loops. The outer loop controls the rows (levels), and the inner loop handles the columns (characters in each row).

```javascript
function stepShape(n) {
  for (let row = 0; row < n; row++) {
    let line = '';
    for (let col = 0; col < n; col++) {
      if (col <= row) {
        line += '#';
      } else {
        line += ' ';
      }
    }
    console.log(line);
  }
}

stepShape(3); // Runs stepShape for n = 3
```

Let's analyze the `stepShape` function:

1.  **Outer Loop (Rows):**
    *   `for (let row = 0; row < n; row++)`: The outer `for` loop iterates `n` times, representing each row (level) of the step shape. `row` goes from 0 to `n-1`.

2.  **Inner Loop (Columns) and Character Building:**
    *   `let line = '';`: Inside the outer loop, we initialize an empty string `line` for each row. This string will store the characters for the current row.
    *   `for (let col = 0; col < n; col++)`: The inner `for` loop also iterates `n` times, representing each column position within a row. `col` also goes from 0 to `n-1`.
    *   `if (col <= row)`: This is the core logic to determine whether to place a `#` or a space.
        *   `col <= row`: For each row, we check if the current column index `col` is less than or equal to the current row index `row`.
        *   If `true`, it means we are in the step portion of the row, so we append a `#` to the `line`.
        *   `else`: If `col > row`, we are in the space portion of the row (to the right of the step), so we append a space `" "` to the `line`.
    *   `line += ...`:  We append either `#` or `" "` to the `line` string in each iteration of the inner loop.

3.  **Console Logging Each Row:**
    *   `console.log(line)`: After the inner loop completes (we have built the `line` string for the current row), we `console.log(line)` to print the entire row to the console.

This nested loop structure combined with the `col <= row` condition effectively generates the step shape pattern, placing `#` characters to form the step and spaces to fill in the right side.

## 10. Pyramid Shape Pattern

**Problem:** Write a function that accepts a positive number `n` and console logs a pyramid shape with `n` levels using the pound character (`#`). The pyramid should have spaces on both the left and right-hand sides.

**Examples (n = 3):**

```
  #
 ###
#####
```

### 10.1 Nested Loop Approach with Midpoint Calculation

Creating a pyramid shape with spaces on both sides requires a slightly more complex nested loop logic. We'll use a midpoint calculation to center the pyramid.

```javascript
function pyramidShape(n) {
  const midpoint = Math.floor((2 * n - 1) / 2);

  for (let row = 0; row < n; row++) {
    let line = '';
    for (let col = 0; col < 2 * n - 1; col++) {
      if (col >= midpoint - row && col <= midpoint + row) {
        line += '#';
      } else {
        line += ' ';
      }
    }
    console.log(line);
  }
}

pyramidShape(3); // Runs pyramidShape for n = 3
```

Let's break down the `pyramidShape` function:

1.  **Midpoint Calculation:**
    *   `const midpoint = Math.floor((2 * n - 1) / 2)`:
        *   `(2 * n - 1)`: Calculates the total number of columns needed for the widest row of the pyramid (bottom row). For a pyramid of height `n`, the bottom row has `2n - 1` characters.
        *   `/ 2`: Divides the total columns by 2 to find the middle column index (approximately).
        *   `Math.floor(...)`: Rounds down to the nearest integer to get the integer index of the midpoint column.

2.  **Outer Loop (Rows):**
    *   `for (let row = 0; row < n; row++)`: The outer loop iterates `n` times, representing each row (level) of the pyramid.

3.  **Inner Loop (Columns) and Character Building:**
    *   `let line = '';`: Initializes an empty string `line` for each row.
    *   `for (let col = 0; col < 2 * n - 1; col++)`: The inner loop iterates `2n - 1` times, covering all column positions in each row.
    *   `if (col >= midpoint - row && col <= midpoint + row)`: This is the key condition for placing `#` characters to form the pyramid.
        *   `midpoint - row`: Calculates the starting column index for `#` characters in the current `row`. As `row` increases, this starting index moves to the left, widening the pyramid base.
        *   `midpoint + row`: Calculates the ending column index for `#` characters in the current `row`. As `row` increases, this ending index moves to the right, also widening the base.
        *   `col >= midpoint - row && col <= midpoint + row`: Checks if the current column index `col` falls within the range defined by the starting and ending column indices.
        *   If `true`, it means we are within the pyramid shape for the current row, so we append a `#` to `line`.
        *   `else`: If `col` is outside the pyramid range, we append a space `" "` to `line`.

4.  **Console Logging Each Row:**
    *   `console.log(line)`: Prints the completed `line` string for the current row, forming the pyramid level.

This nested loop structure, combined with the midpoint calculation and the `col >= midpoint - row && col <= midpoint + row` condition, accurately generates the pyramid shape with spaces on both sides, centering the pyramid within the allocated column width.

## 11. Spiral Matrix

**Problem:** Write a function that accepts an integer `n` and returns an `n` x `n` spiral matrix.

**Examples (n = 3):**

```
[[1, 2, 3],
 [8, 9, 4],
 [7, 6, 5]]
```

This is a more complex problem involving matrix manipulation and requires a systematic approach to filling the matrix in a spiral pattern.

### 11.1 Layer-by-Layer Filling Approach

We can fill the spiral matrix layer by layer, moving in a clockwise spiral direction. We'll use variables to track the boundaries of the current layer and loops to fill each side of the layer.

```javascript
function spiralMatrix(n) {
  const result = [];
  for (let i = 0; i < n; i++) {
    result.push([]); // Initialize n x n matrix with empty arrays
  }

  let counter = 1;
  let startRow = 0;
  let endRow = n - 1;
  let startCol = 0;
  let endCol = n - 1;

  while (startRow <= endRow && startCol <= endCol) {
    // Top row (left to right)
    for (let i = startCol; i <= endCol; i++) {
      result[startRow][i] = counter;
      counter++;
    }
    startRow++; // Move to the next row

    // Right column (top to bottom)
    for (let i = startRow; i <= endRow; i++) {
      result[i][endCol] = counter;
      counter++;
    }
    endCol--; // Move to the previous column

    // Bottom row (right to left)
    if (startRow <= endRow) { // Prevent duplicate row in odd n cases
      for (let i = endCol; i >= startCol; i--) {
        result[endRow][i] = counter;
        counter++;
      }
      endRow--; // Move to the previous row
    }

    // Left column (bottom to top)
    if (startCol <= endCol) { // Prevent duplicate column in odd n cases
      for (let i = endRow; i >= startRow; i--) {
        result[i][startCol] = counter;
        counter++;
      }
      startCol++; // Move to the next column
    }
  }

  return result;
}

console.log(spiralMatrix(3));
// Output: [[1, 2, 3], [8, 9, 4], [7, 6, 5]]
console.log(spiralMatrix(4));
// Output: [[1, 2, 3, 4], [12, 13, 14, 5], [11, 16, 15, 6], [10, 9, 8, 7]]
```

Let's dissect the `spiralMatrix` function:

1.  **Matrix Initialization:**
    *   `const result = []`: Creates an empty array `result` to represent the matrix.
    *   `for (let i = 0; i < n; i++) { result.push([]); }`: Initializes `result` as an `n` x `n` matrix by pushing `n` empty arrays (rows) into it.

2.  **Boundary and Counter Variables:**
    *   `counter = 1`: Initializes a `counter` variable to 1. This will be used to fill the matrix with increasing numbers in a spiral.
    *   `startRow = 0`, `endRow = n - 1`, `startCol = 0`, `endCol = n - 1`: These variables define the boundaries of the current layer of the spiral we are filling. They initially encompass the entire matrix.

3.  **`while` Loop for Layer Processing:**
    *   `while (startRow <= endRow && startCol <= endCol)`: The `while` loop continues as long as the `startRow` is less than or equal to `endRow` and `startCol` is less than or equal to `endCol`. This condition ensures we process all layers of the spiral, moving inwards.

4.  **Four Loops for Each Side of a Layer:**

    *   **Top Row (Left to Right):**
        *   `for (let i = startCol; i <= endCol; i++)`: Iterates through columns from `startCol` to `endCol` in the current `startRow` (top row).
        *   `result[startRow][i] = counter`: Fills the matrix elements in the top row with increasing `counter` values.
        *   `counter++`: Increments the `counter`.
        *   `startRow++`: After filling the top row, we increment `startRow` to move the top boundary down for the next inner layer.

    *   **Right Column (Top to Bottom):**
        *   `for (let i = startRow; i <= endRow; i++)`: Iterates through rows from `startRow` to `endRow` in the current `endCol` (right column).
        *   `result[i][endCol] = counter`: Fills the matrix elements in the right column with increasing `counter` values.
        *   `counter++`: Increments the `counter`.
        *   `endCol--`: After filling the right column, we decrement `endCol` to move the right boundary left for the next inner layer.

    *   **Bottom Row (Right to Left):**
        *   `if (startRow <= endRow)`: This condition prevents processing a duplicate row in cases where `n` is odd. If `startRow` becomes greater than `endRow`, it means we have reached the center row in an odd-sized matrix, and we should not process the bottom row again.
        *   `for (let i = endCol; i >= startCol; i--)`: Iterates through columns from `endCol` down to `startCol` in the current `endRow` (bottom row).
        *   `result[endRow][i] = counter`: Fills the matrix elements in the bottom row with increasing `counter` values.
        *   `counter++`: Increments the `counter`.
        *   `endRow--`: After filling the bottom row, we decrement `endRow` to move the bottom boundary up for the next inner layer.

    *   **Left Column (Bottom to Top):**
        *   `if (startCol <= endCol)`: Similar to the bottom row condition, this prevents processing a duplicate column in odd `n` cases.
        *   `for (let i = endRow; i >= startRow; i--)`: Iterates through rows from `endRow` down to `startRow` in the current `startCol` (left column).
        *   `result[i][startCol] = counter`: Fills the matrix elements in the left column with increasing `counter` values.
        *   `counter++`: Increments the `counter`.
        *   `startCol++`: After filling the left column, we increment `startCol` to move the left boundary right for the next inner layer.

5.  **Returning the Spiral Matrix:**
    *   `return result`: After the `while` loop completes (all layers are filled), we return the `result` matrix, which now contains the spiral pattern.

This layer-by-layer filling approach, using boundary variables and four loops per layer, systematically constructs the spiral matrix. The `while` loop ensures that we process all layers until we reach the center of the matrix.

This concludes our exploration of ten essential JavaScript algorithm problems for beginners.  By mastering these concepts and practicing similar challenges, you will build a strong foundation in algorithms and be well-prepared for coding interviews and more advanced programming tasks. Remember to explore the linked LeetCode playlist for further practice and more challenging problems!
