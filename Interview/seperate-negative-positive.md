## Input: -12, 11, -13, -5, 6, -7, 5, -3, -6
## Output: -12 -13 -5 -7 -3 -6 11 6 5

const numbers = [-12, 11, -13, -5, 6, -7, 5, -3, -6];

// Separate negative and positive numbers
const negatives = numbers.filter(num => num < 0);
const positives = numbers.filter(num => num > 0);

// Combine the results
const sortedNumbers = negatives.concat(positives);

// Output the result
console.log(sortedNumbers.join(' '));
