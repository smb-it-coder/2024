In JavaScript, `map`, `filter`, and `reduce` are array methods that help you transform and process arrays. Each has a distinct purpose:

### 1. `map`

**Purpose:** To transform each element in an array and return a new array with the transformed elements.

**Usage:**
- It iterates over each element in the array.
- Applies a callback function to each element.
- Returns a new array containing the results of applying the callback.

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]
```

**Key Points:**
- The length of the new array is the same as the original.
- It does not mutate the original array.

### 2. `filter`

**Purpose:** To create a new array with all elements that pass a test defined by a callback function.

**Usage:**
- It iterates over each element in the array.
- Applies a callback function that returns a boolean value.
- Returns a new array containing only the elements for which the callback returned `true`.

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4]
```

**Key Points:**
- The length of the new array may be less than or equal to the original.
- It does not mutate the original array.

### 3. `reduce`

**Purpose:** To accumulate values into a single result based on the array’s elements and a callback function.

**Usage:**
- It iterates over each element in the array.
- Applies a callback function that takes an accumulator and the current element.
- Returns a single value that is the result of the accumulation.

**Example:**

```javascript
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((accumulator, num) => accumulator + num, 0);
console.log(sum); // 15
```

**Key Points:**
- It can return any type of value (number, string, object, etc.).
- It requires an initial value for the accumulator (unless you use the first element of the array).
- It does not mutate the original array.

### Summary

- **`map`**: Transforms each element of the array and returns a new array with the transformed elements.
- **`filter`**: Selects elements based on a condition and returns a new array with only the elements that pass the condition.
- **`reduce`**: Accumulates values into a single result based on a callback function, returning a single value.

Each method is powerful for handling different array processing needs and can often be combined to perform complex transformations and calculations.