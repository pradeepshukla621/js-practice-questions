# JavaScript Interview Questions

A collection of common **JavaScript interview questions** with simple and easy-to-understand solutions.

These problems cover strings, arrays, objects, `Set`, `Map`, sorting, and common problem-solving techniques.

---

## 1. Reverse Words in a Sentence

Reverse the order of words in a sentence.

### Example

```text
Input:
"I love JavaScript"

Output:
"JavaScript love I"
```

### Solution

```javascript
function reverseWords(str) {
  return str.split(" ").reverse().join(" ");
}

console.log(reverseWords("I love JavaScript"));

// Output:
// JavaScript love I
```

### How it works

```text
"I love JavaScript"

        ↓ split(" ")

["I", "love", "JavaScript"]

        ↓ reverse()

["JavaScript", "love", "I"]

        ↓ join(" ")

"JavaScript love I"
```

---

## 2. Check Anagram

Two strings are **anagrams** if they contain the same letters in a different order.

### Example

```text
"listen"
"silent"

Both contain:
l, i, s, t, e, n

Result:
true
```

### Solution

```javascript
function isAnagram(a, b) {
  return (
    a.split("").sort().join("") ===
    b.split("").sort().join("")
  );
}

console.log(isAnagram("listen", "silent"));

// Output:
// true
```

### How it works

```text
"listen"
    ↓ split("")
["l", "i", "s", "t", "e", "n"]
    ↓ sort()
["e", "i", "l", "n", "s", "t"]
    ↓ join("")
"eilnst"
```

The same process happens for `"silent"`.

If both results are equal, the strings are anagrams.

---

## 3. Remove Duplicates from Array

Remove duplicate values from an array.

### Example

```text
Input:
[1, 2, 2, 3, 4, 4, 5]

Output:
[1, 2, 3, 4, 5]
```

### Solution

```javascript
function removeDuplicates(arr) {
  return [...new Set(arr)];
}

console.log(
  removeDuplicates([1, 2, 2, 3, 4, 4, 5])
);

// Output:
// [1, 2, 3, 4, 5]
```

### How it works

`Set` automatically stores only unique values.

```javascript
new Set([1, 2, 2, 3, 4, 4, 5]);

// Set { 1, 2, 3, 4, 5 }
```

The spread operator `...` converts the `Set` back into an array.

```javascript
[...new Set([1, 2, 2, 3, 4, 4, 5])];

// [1, 2, 3, 4, 5]
```

---

## 4. Find Missing Number

Find the missing number from a sequence starting from `1` to `N`.

### Example

```text
Input:
[1, 2, 4, 5]

Missing:
3
```

### Formula

```text
Sum of 1 to N = N × (N + 1) / 2
```

### Solution

```javascript
function missingNumber(arr) {
  let n = arr.length + 1;

  let sum = (n * (n + 1)) / 2;

  let arrSum = arr.reduce(
    (a, b) => a + b,
    0
  );

  return sum - arrSum;
}

console.log(missingNumber([1, 2, 4, 5]));

// Output:
// 3
```

### How it works

For:

```text
[1, 2, 4, 5]
```

The expected numbers are:

```text
1 + 2 + 3 + 4 + 5 = 15
```

Actual array sum:

```text
1 + 2 + 4 + 5 = 12
```

Difference:

```text
15 - 12 = 3
```

Therefore, the missing number is:

```text
3
```

---

## 5. Two Sum Problem

### Goal

Find two numbers in an array whose sum equals the target.

Return their indexes.

### Example

```text
Array:
[2, 7, 11, 15]

Target:
9

2 + 7 = 9

Indexes:
[0, 1]
```

### Solution

```javascript
function twoSum(arr, target) {
  let map = {};

  for (let i = 0; i < arr.length; i++) {
    let diff = target - arr[i];

    if (map[diff] !== undefined) {
      return [map[diff], i];
    }

    map[arr[i]] = i;
  }
}

console.log(twoSum([2, 7, 11, 15], 9));

// Output:
// [0, 1]
```

### How it works

For:

```text
arr = [2, 7, 11, 15]
target = 9
```

First number:

```text
2

9 - 2 = 7

7 is not in the map.
Store:

2 → index 0
```

Second number:

```text
7

9 - 7 = 2

2 exists in the map.

Return:

[0, 1]
```

### Visual

```text
Index:   0   1   2   3
Array:   2   7  11  15

         ↑   ↑
         2 + 7 = 9

Result:
[0, 1]
```

---

# Quick Revision

| # | Question | Main Concept |
|---|---|---|
| 1 | Reverse Words | `split()`, `reverse()`, `join()` |
| 2 | Check Anagram | `split()`, `sort()`, `join()` |
| 3 | Remove Duplicates | `Set` |
| 4 | Missing Number | Formula + `reduce()` |
| 5 | Two Sum | Object / Hash Map |

---

# JavaScript Concepts Covered

- Strings
- Arrays
- Objects
- `split()`
- `reverse()`
- `join()`
- `sort()`
- `Set`
- Spread operator `...`
- `reduce()`
- Loops
- Hash Map concept
- Array indexes
- Mathematical formulas
- Problem-solving techniques

---

# Interview Tips

When solving JavaScript interview problems:

1. Understand the problem first.
2. Start with a simple solution.
3. Think about edge cases.
4. Consider time and space complexity.
5. Try to optimize the solution.
6. Explain your approach clearly.
7. Write clean and readable code.

---

## Goal

Practice these problems regularly to improve **JavaScript fundamentals, problem-solving skills, and interview preparation**.
