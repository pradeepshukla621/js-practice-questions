# JavaScript Functions, Closures & `this`

This section contains JavaScript examples covering:

- Functions returning functions
- Function execution
- Nested functions
- Callback functions
- `this` keyword
- `bind()`
- `call()`
- `apply()`
- Function borrowing

---

# 1. Function Returning Another Function

A function can return another function.

```javascript
function A() {
  console.log("A is called");

  return function B() {
    return "sandeep";
  };
}

console.log(A());

let returnOfA = A();

console.log(returnOfA());
```

### Output

```text
A is called
[Function: B]

A is called
sandeep
```

### How it works

When we call:

```javascript
A();
```

Function `A` executes and returns function `B`.

```text
A()
 ↓
Returns function B
```

When we store the returned function:

```javascript
let returnOfA = A();
```

`returnOfA` now contains function `B`.

So:

```javascript
returnOfA();
```

executes function `B`.

```text
A()
 ↓
B()
 ↓
"sandeep"
```

---

# 2. Function Execution Order

This example demonstrates how JavaScript executes functions.

```javascript
function A() {

  function X() {
    console.log("X");
  }

  X();

  return function Y() {
    console.log("Y");
  };

  Y();

  function Z() {
    console.log("Z");
  }

  Z();
}

A();
```

### Output

```text
X
```

### Why?

The important point is:

```javascript
return function Y() {
  console.log("Y");
};
```

When JavaScript reaches `return`, the function immediately exits.

Everything after `return` is unreachable.

Therefore:

```javascript
Y();
```

and:

```javascript
Z();
```

will never execute.

### Execution Flow

```text
A()
 ↓
X()
 ↓
console.log("X")
 ↓
return Y
 ↓
Function A ends
```

### Important

```javascript
return something;

// Code below return will not execute
```

---

# 3. Passing a Function as an Argument

JavaScript functions can be passed as arguments to other functions.

This is commonly known as a **callback function**.

```javascript
function X() {
  console.log("X");
}

function Y() {
  console.log("Y");
}

function Z() {
  console.log("Z");
}

function A(fn) {
  console.log("A is called");

  fn();
}

A(X);
```

### Output

```text
A is called
X
```

### How it works

We pass function `X` to function `A`:

```javascript
A(X);
```

Inside `A`:

```javascript
function A(fn) {
  console.log("A is called");

  fn();
}
```

The parameter `fn` now refers to function `X`.

Therefore:

```javascript
fn();
```

is equivalent to:

```javascript
X();
```

### Execution Flow

```text
A(X)
 ↓
fn = X
 ↓
"A is called"
 ↓
fn()
 ↓
X()
 ↓
"X"
```

---

# 4. `this` Keyword

The `this` keyword refers to the object that is calling the function in this example.

```javascript
let userDetails = {
  name: "San",
  age: 20,
  role: "developer",

  calAmount: function () {
    console.log(this);
  }
};

userDetails.calAmount();
```

### Output

```text
{
  name: "San",
  age: 20,
  role: "developer",
  calAmount: [Function: calAmount]
}
```

### Why?

The function is called using:

```javascript
userDetails.calAmount();
```

So inside `calAmount`:

```javascript
this
```

refers to:

```javascript
userDetails
```

### Simple Rule

```text
object.function()

        ↓

this = object
```

For example:

```javascript
userDetails.calAmount();
```

means:

```text
this → userDetails
```

---

# 5. `bind()` Example

The `bind()` method creates a new function with a specific `this` value.

```javascript
let user = {
  name: "Pradeep",

  sayName: function () {
    console.log(this.name);
  }
};

let userDetails = {
  name: "SHYAM"
};

let fn = user.sayName.bind(userDetails);

fn();
```

### Output

```text
SHYAM
```

### How it works

Normally:

```javascript
user.sayName();
```

would make:

```text
this → user
```

But we use:

```javascript
bind(userDetails);
```

So:

```text
this → userDetails
```

Therefore:

```javascript
this.name
```

returns:

```text
"HGHGHGHGHG"
```

### Important

`bind()` does **not** immediately execute the function.

```javascript
let fn = user.sayName.bind(userDetails);
```

This creates a new function.

Then:

```javascript
fn();
```

executes it.

---

# 6. `call()`, `apply()`, and `bind()`

These methods are used to control the value of `this`.

```javascript
function ABC(age, fname) {
  console.log(
    `Age ${age} and fname ${fname} and ${this.school}`
  );
}

let userSchool = {
  school: "ABC"
};
```

---

## 6.1 `call()`

`call()` immediately invokes the function.

Arguments are passed individually.

```javascript
ABC.call(userSchool, 10, "Sandeep");
```

### Output

```text
Age 10 and fname Sandeep and ABC
```

### Syntax

```javascript
function.call(thisValue, arg1, arg2, arg3);
```

---

## 6.2 `apply()`

`apply()` also immediately invokes the function.

The difference is that arguments are passed as an array.

```javascript
ABC.apply(userSchool, [10, "Sandeep"]);
```

### Output

```text
Age 10 and fname Sandeep and ABC
```

### Syntax

```javascript
function.apply(thisValue, [arg1, arg2, arg3]);
```

---

## 6.3 `bind()`

`bind()` does not immediately execute the function.

It returns a new function.

```javascript
let fn = ABC.bind(
  userSchool,
  10,
  "Sandeep"
);

fn();
```

### Output

```text
Age 10 and fname Sandeep and ABC
```

### Or

You can call it directly:

```javascript
ABC.bind(
  userSchool,
  10,
  "Sandeep"
)();
```

---

# 7. `call()` vs `apply()` vs `bind()`

| Method | Executes Immediately | Arguments |
|---|---|---|
| `call()` | Yes | Individually |
| `apply()` | Yes | Array |
| `bind()` | No | Individually or partially |

### Example

```javascript
// call
ABC.call(userSchool, 10, "Sandeep");

// apply
ABC.apply(userSchool, [10, "Sandeep"]);

// bind
let fn = ABC.bind(userSchool, 10, "Sandeep");
fn();
```

---

# 8. Why This Doesn't Work

This code does not work:

```javascript
ABC(10, "Sandeep").bind(userSchool);
```

### Why?

First:

```javascript
ABC(10, "Sandeep")
```

executes `ABC()` immediately.

But `ABC()` does not return a function.

It returns:

```javascript
undefined
```

So this becomes:

```javascript
undefined.bind(userSchool);
```

which causes an error.

### Correct Approach

Use:

```javascript
ABC.bind(userSchool, 10, "Sandeep")();
```

Or:

```javascript
let fn = ABC.bind(userSchool, 10, "Sandeep");

fn();
```

---

# 9. Quick Revision

| Concept | Example | Purpose |
|---|---|---|
| Function Return | `return function B()` | Return another function |
| Callback | `A(X)` | Pass function as argument |
| `this` | `userDetails.calAmount()` | Refers to calling object |
| `bind()` | `fn = func.bind(obj)` | Create function with fixed `this` |
| `call()` | `func.call(obj, a, b)` | Execute immediately |
| `apply()` | `func.apply(obj, [a, b])` | Execute immediately |
| Function Borrowing | `call/apply/bind` | Use another object's context |

---

# 10. Important Interview Points

### Function Returning Function

```javascript
function A() {
  return function B() {};
}
```

`A()` returns another function.

---

### Callback Function

```javascript
function A(fn) {
  fn();
}

A(X);
```

`X` is passed as a function argument and executed inside `A`.

---

### `this`

```javascript
userDetails.calAmount();
```

In this method call:

```text
this → userDetails
```

---

### `call()`

```javascript
ABC.call(userSchool, 10, "Sandeep");
```

- Executes immediately
- Arguments passed individually

---

### `apply()`

```javascript
ABC.apply(userSchool, [10, "Sandeep"]);
```

- Executes immediately
- Arguments passed as an array

---

### `bind()`

```javascript
let fn = ABC.bind(userSchool, 10, "Sandeep");

fn();
```

- Does not execute immediately
- Returns a new function
- Can be executed later

---

# Final Cheat Sheet

```text
call()
  ↓
Execute now
Arguments → individually

apply()
  ↓
Execute now
Arguments → array

bind()
  ↓
Execute later
Returns → new function
```

---

## JavaScript Concepts Covered

- Functions
- Nested functions
- Function return
- Callback functions
- Function execution
- `this` keyword
- `bind()`
- `call()`
- `apply()`
- Function borrowing
- Function context
- Execution flow
