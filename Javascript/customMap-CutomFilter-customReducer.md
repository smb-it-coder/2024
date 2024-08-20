Sure! It sounds like you want to implement custom versions of the common functional programming operations: `map`, `filter`, and `reduce`. I'll provide implementations for these operations, which will work similarly to the built-in JavaScript methods but will be written from scratch.

Here's how you can write `OwnCustomMap`, `OwnCustomFilter`, and `OwnCustomReducer` functions in JavaScript:

```javascript
// Custom map function
function OwnCustomMap(array, callback) {
    let result = []; // Create an empty array to store the results
    for (let i = 0; i < array.length; i++) {
        // Call the callback function with the current element and its index
        result.push(callback(array[i], i, array));
    }
    return result; // Return the new array with mapped values
}

// Custom filter function
function OwnCustomFilter(array, callback) {
    let result = []; // Create an empty array to store the filtered results
    for (let i = 0; i < array.length; i++) {
        // Call the callback function with the current element and its index
        if (callback(array[i], i, array)) {
            result.push(array[i]); // Include the element if the callback returns true
        }
    }
    return result; // Return the new array with filtered values
}

// Custom reduce function
function OwnCustomReduce(array, callback, initialValue) {
    let accumulator = initialValue; // Initialize the accumulator
    let startIndex = 0; // Determine where to start based on whether an initial value is provided

    // If no initial value is provided, use the first element of the array
    if (initialValue === undefined) {
        accumulator = array[0];
        startIndex = 1; // Start from the second element
    }

    for (let i = startIndex; i < array.length; i++) {
        // Call the callback function with the accumulator, current element, and its index
        accumulator = callback(accumulator, array[i], i, array);
    }
    return accumulator; // Return the final accumulated result
}

// Example usage:

// Define a callback function for map
function double(x) {
    return x * 2;
}

// Define a callback function for filter
function isEven(x) {
    return x % 2 === 0;
}

// Define a callback function for reduce
function sum(acc, x) {
    return acc + x;
}

// Test the custom functions
let numbers = [1, 2, 3, 4, 5];

console.log(OwnCustomMap(numbers, double)); // Output: [2, 4, 6, 8, 10]
console.log(OwnCustomFilter(numbers, isEven)); // Output: [2, 4]
console.log(OwnCustomReduce(numbers, sum, 0)); // Output: 15
```

### Explanation:

1. **OwnCustomMap**:
   - Takes an array and a callback function.
   - Creates a new array by applying the callback function to each element of the input array.
   - Returns the new array.

2. **OwnCustomFilter**:
   - Takes an array and a callback function.
   - Creates a new array with elements that pass the condition defined in the callback function.
   - Returns the new array.

3. **OwnCustomReduce**:
   - Takes an array, a callback function, and an optional initial value.
   - Reduces the array to a single value based on the callback function.
   - If no initial value is provided, the first element of the array is used as the initial value, and reduction starts from the second element.

Feel free to test these functions with different callback functions and arrays to see how they work.