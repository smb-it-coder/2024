To format an integer with thousands separators in JavaScript without using built-in functions, you can create a custom function. Here’s an example of how you could implement such a function:

```javascript
function formatNumber(num) {
    // Convert the number to a string
    let numStr = num.toString();

    // Initialize an empty string to hold the formatted result
    let formattedStr = '';
    
    // Determine the length of the string
    let length = numStr.length;
    
    // The index from which we start adding commas (i.e., every three digits from the end)
    let startIndex = length % 3;

    // If the startIndex is 0, we need to start with the first group of three digits
    if (startIndex === 0) {
        startIndex = 3;
    }
    
    // Append the initial group of digits to the result
    formattedStr += numStr.slice(0, startIndex);

    // Iterate over the rest of the string and add commas as needed
    for (let i = startIndex; i < length; i += 3) {
        formattedStr += ',' + numStr.slice(i, i + 3);
    }
    
    return formattedStr;
}

// Examples
console.log(formatNumber(10000));   // Output: 10,000
console.log(formatNumber(200000));  // Output: 200,000
console.log(formatNumber(1130000)); // Output: 1,130,000
```

### Explanation:

1. **Convert the Number to a String**: Convert the integer to a string so we can manipulate it easily.

2. **Initialize Variables**: Create an empty string to hold the result and determine the length of the number string.

3. **Determine the Starting Point**: Find out where the first comma should be placed. If the length is not a multiple of 3, `startIndex` will be set to the number of digits before the first comma.

4. **Build the Formatted String**: 
   - Add the initial group of digits to `formattedStr`.
   - Iterate through the remaining digits in chunks of three, appending a comma before each chunk.

5. **Return the Formatted String**: Output the final formatted string.

This approach ensures that numbers are formatted with commas as thousands separators, making them easier to read.