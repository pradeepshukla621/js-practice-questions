# Javascript Practice Questions


# UNIT 1

JavaScript DSA Practice

A collection of JavaScript examples covering common DSA concepts, array operations, sorting algorithms, recursion, and problem-solving patterns.

1. Reverse String

Reverse a string without using built-in reverse methods.

function reverseString(str) {
  let reversed = "";

  for (let i = str.length - 1; i >= 0; i--) {
    reversed = reversed + str[i];
  }

  return reversed;
}

console.log(reverseString("hello"));
// Output: "olleh"

2. Reverse Array

Reverse an array by iterating from the last element to the first.

function reverseArray() {
  let emp = ["PS", "JK", "NS", "RN"];
  let reversed = "";

  for (let i = emp.length - 1; i >= 0; i--) {
    reversed = reversed + emp[i];
  }

  return reversed;
}

console.log(reverseArray());
// Output: "RNNSJKPS"

3. Reverse Object Values — Numeric Keys

An object with numeric keys can be treated similarly to an array.

function reverseObjectValues() {
  let emp = {
    0: "PS",
    1: "JK",
    2: "NS",
    3: "RN"
  };

  let reversed = "";
  let keys = Object.keys(emp);

  for (let i = keys.length - 1; i >= 0; i--) {
    reversed = reversed + emp[keys[i]];
  }

  return reversed;
}

console.log(reverseObjectValues());
// Output: "RNNSJKPS"

Object.keys()
Object.keys(emp);
// ["0", "1", "2", "3"]

4. Reverse Object Values — Named Keys

Using Object.values() to get all values and then iterating in reverse.

function reverseObjectValues() {
  let emp = {
    first: "PS",
    second: "JK",
    third: "NS",
    fourth: "RN"
  };

  let values = Object.values(emp);
  let reversed = "";

  for (let i = values.length - 1; i >= 0; i--) {
    reversed = reversed + values[i];
  }

  return reversed;
}

console.log(reverseObjectValues());
// Output: "RNNSJKPS"

Object.values()
Object.values(emp);
// ["PS", "JK", "NS", "RN"]

5. Palindrome

A palindrome is a word that reads the same forward and backward.

Examples:

madam → Palindrome
hello → Not a palindrome
function isPalindrome(str) {
  let reversed = str.split("").reverse().join("");

  return str === reversed;
}

console.log("Palindrome (madam)", isPalindrome("madam"));
// true

console.log("Palindrome (hello)", isPalindrome("hello"));
// false

6. Find Largest Number in an Array

Find the largest number without using Math.max().

function findLargest(arr) {
  let max = arr[0];

  for (let num of arr) {
    if (num > max) {
      max = num;
    }
  }

  return max;
}

console.log("findLargest", findLargest([5, 2, 8, 1, 9]));
// Output: 9

7. Find Smallest Number in an Array

Find the smallest number without using Math.min().

function findSmallest(arr) {
  let min = arr[0];

  for (let num of arr) {
    if (num < min) {
      min = num;
    }
  }

  return min;
}

console.log("findSmallest", findSmallest([5, 2, 8, 1, 9]));
// Output: 1

8. Count Occurrences of Each Element

Count how many times each element appears in an array.

function countOccurrences(arr) {
  let count = {};

  for (let item of arr) {
    if (count[item]) {
      count[item]++;
    } else {
      count[item] = 1;
    }
  }

  return count;
}

console.log(
  countOccurrences([1, 2, 3, 2, 3, 3, 3])
);

// Output:
// { 1: 1, 2: 2, 3: 4 }

Logic
First occurrence → set value to 1
Existing value   → increase count by 1

9. Find Missing Number

Find the missing number from a sequence from 1 to N.

Formula
Sum of 1 to N = N × (N + 1) / 2

function missingNumber(arr) {
  let n = arr.length + 1;

  let actualSum = (n * (n + 1)) / 2;

  let arrSum = arr.reduce(
    (acc, num) => acc + num,
    0
  );

  return actualSum - arrSum;
}

console.log(
  "missingNumber",
  missingNumber([1, 2, 4, 5])
);

// Output: 3

10. Reduce Method

The reduce() method can be used to calculate the sum of array elements.

let arr = [1, 2, 4];

let arrRed = arr.reduce((a, b) => a + b);

console.log("Reduce arr", arrRed);

// Output: 7

How it works
1 + 2 = 3
3 + 4 = 7

⭐ Part 1 — Sorting Algorithms
11. Bubble Sort
Easy Trick

Think of bubbles rising — bigger numbers gradually move to the end.

function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [
          arr[j + 1],
          arr[j]
        ];
      }
    }
  }

  return arr;
}

console.log(
  "BubbleSort",
  bubbleSort([5, 3, 8, 4, 2])
);

// Output:
// [2, 3, 4, 5, 8]

Time Complexity
Best Case:    O(n)
Average Case: O(n²)
Worst Case:   O(n²)
Space:        O(1)

12. Selection Sort
Easy Trick

Find the smallest number → put it at the front.

function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let minIndex = i;

    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    [arr[i], arr[minIndex]] = [
      arr[minIndex],
      arr[i]
    ];
  }

  return arr;
}

console.log(
  "SelectionSort",
  selectionSort([5, 3, 8, 4, 2])
);

// Output:
// [2, 3, 4, 5, 8]

Time Complexity
Best Case:    O(n²)
Average Case: O(n²)
Worst Case:   O(n²)
Space:        O(1)

13. Insertion Sort
Easy Trick

Think about arranging playing cards in your hand.

Take one card → find its correct position → insert it.

function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let current = arr[i];
    let j = i - 1;

    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }

    arr[j + 1] = current;
  }

  return arr;
}

console.log(
  "InsertionSort",
  insertionSort([5, 3, 8, 4, 2])
);

// Output:
// [2, 3, 4, 5, 8]

Time Complexity
Best Case:    O(n)
Average Case: O(n²)
Worst Case:   O(n²)
Space:        O(1)

⭐ Part 2 — Recursion
What is Recursion?

Recursion is when a function calls itself.

A recursive function generally has:

Base Case — stops the recursion.
Recursive Case — calls the function again with a smaller/simpler input.
14. Factorial
Formula
5! = 5 × 4 × 3 × 2 × 1
   = 120

function factorial(n) {
  if (n === 1) {
    return 1;
  }

  return n * factorial(n - 1);
}

console.log("Factorial", factorial(5));

// Output: 120

Execution
factorial(5)
5 × factorial(4)
5 × 4 × factorial(3)
5 × 4 × 3 × factorial(2)
5 × 4 × 3 × 2 × factorial(1)
5 × 4 × 3 × 2 × 1
= 120

15. Fibonacci
Definition
fib(n) = fib(n - 1) + fib(n - 2)

function fib(n) {
  if (n <= 1) {
    return n;
  }

  return fib(n - 1) + fib(n - 2);
}

console.log("Fibonacci", fib(6));

// Output: 8

Fibonacci Sequence
0, 1, 1, 2, 3, 5, 8, 13, ...


For example:

fib(6) = 8

Quick Revision
Problem	Main Concept
Reverse String	Loop
Reverse Array	Array + Loop
Reverse Object	Object.keys() / Object.values()
Palindrome	String manipulation
Largest Number	Loop
Smallest Number	Loop
Count Occurrences	Object / Hash Map
Missing Number	Mathematical formula
Array Sum	reduce()
Bubble Sort	Sorting
Selection Sort	Sorting
Insertion Sort	Sorting
Factorial	Recursion
Fibonacci	Recursion
JavaScript Concepts Covered
for loops
for...of
Arrays
Objects
Object.keys()
Object.values()
reduce()
String manipulation
Array destructuring
Sorting algorithms
Recursion
Time complexity basics
Problem-solving patterns
