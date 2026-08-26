# Javascript Practice Questions


# UNIT 1

// function reverseString(str) {
//     let reversed = "";
//     for (let i = str.length-1; i >= 0; i--) {
//         // reversed += str[i];
//         reversed = reversed + str[i];
//     }
//     return reversed;
// }

// console.log(reverseString("hello"), "dd");

// Array reverse 
function reverseString() {
    let emp = ['PS', 'JK', 'NS', 'RN'];
    let reversed = "";
    for (let i = emp.length-1; i >= 0; i--) {
        // reversed += str[i];
        reversed = reversed + emp[i];
    }
    return reversed;
}

console.log(reverseString());


// Object with Numeric Keys (like an array substitute)
function reverseObjectValues() {
    let emp = {
        0: "PS",
        1: "JK",
        2: "NS",
        3: "RN"
    };

    let reversed = "";
    let keys = Object.keys(emp); // ["0","1","2","3"]

    for (let i = keys.length - 1; i >= 0; i--) {
        reversed = reversed + emp[keys[i]];
    }
    return reversed;
}

console.log(reverseObjectValues()); // Output: "RNNSJKPS"


// Object with Named keys 
function reverseObjectValues() {
    let emp = {
        first: "PS",
        second: "JK",
        third: "NS",
        fourth: "RN"
    };

    let values = Object.values(emp); // ["PS","JK","NS","RN"]
    let reversed = "";

    for (let i = values.length - 1; i >= 0; i--) {
        reversed = reversed + values[i];
    }
    return reversed;
}

console.log(reverseObjectValues()); // Output: "RNNSJKPS"


// Palindrome
function isPalindrome(str) {
  let reversed = str.split("").reverse().join("");
  return str === reversed;
}

console.log("Palindrome (madam)", isPalindrome("madam")); // true
console.log("Palindrome (hello)", isPalindrome("hello")); // false


// FIND LARGEST NUMBER IN AN ARRAY (without using Math.max)
function findLargest(arr) {
  let max = arr[0];

  for (let num of arr) {
    if (num > max) {
      max = num;
    }
  }

  return max;
}
console.log("findLargest", findLargest([5, 2, 8, 1, 9])); // 9


// FIND SMALLEST NUMBER IN AN ARRAY (without using Math.min)
function findSmallest(arr) {
  let min = arr[0];

  for (let num of arr) {
    if (num < min) {
      min = num;
    }
  }

  return min;
}
console.log("findSmallest", findSmallest([5, 2, 8, 1, 9])); // 1


// COUNT OCCURRENCES OF EACH ELEMENT
function countOccurrences(arr) {
  let count = {};

  for (let item of arr) {
    if (count[item]) {
      count[item]++;      // already exists → increase
    } else {
      count[item] = 1;    // first time → set to 1
    }
  }

  return count;
}

console.log(countOccurrences([1, 2,3, 2, 3, 3, 3]));
// Output: {1: 1, 2: 2, 3: 3}


// FIND MISSING NUMBER (1 to N)
// Easy Trick: Sum of 1..N = N*(N+1)/2
function missingNumber(arr) {
  let n = arr.length + 1;
  let actualSum = (n * (n + 1)) / 2;

  let arrSum = arr.reduce((acc, num) => acc + num, 0);

  return actualSum - arrSum;
}
console.log( "missingNumber", missingNumber([1, 2, 4, 5])); // 3


//REDUCE METHOD EXAMPLE
let arr = [1,2,4];
let arrRed = arr.reduce((a,b)=>a+b)
console.log("Reduce arr ", arrRed) // OUTPUT 7


// ⭐ PART 1 — SORTING (Easy Tricks + JS Code)

// 1. Bubble Sort
// Think of “bubbles” rising—big numbers move to the end.
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]; // swap
      }
    }
  }
  return arr;
}

console.log("BubbleSort", bubbleSort([5, 3, 8, 4, 2]));


// 2. Selection Sort
// Easy Trick: Find the smallest number → put it at the front.
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let minIndex = i;

    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }

    [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]]; // swap
  }

  return arr;
}
console.log("SelectionSort", selectionSort([5, 3, 8, 4, 2]));


// 3. Insertion Sort
// Easy Trick:
// Your hand arranges playing cards.
// Take a card → place it in correct spot.

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
console.log("InsertionSort",insertionSort([5, 3, 8, 4, 2]));


// ⭐ PART 2 — RECURSION (Easy Trick + Examples)
// What is recursion?
// A function calling itself.


// 1. Factorial (n!)
function factorial(n) {
  if (n === 1) return 1;  // base case
  return n * factorial(n - 1);
}
console.log('Factorial', factorial(5)); // 120


// 2. Fibonacci
// Definition: fib(n) = fib(n-1) + fib(n-2)
function fib(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
}
console.log('Fibonacci', fib(6)); // 8



