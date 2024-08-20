
# CASE 1 :- 
## swap the values of two variables in JavaScript without using a third variable by leveraging array destructuring.

let a = "Hello";
let b = "World";

console.log(a); // "Hello"
console.log(b); // "World"

// Swap using array destructuring
[a, b] = [b, a];

console.log(a); // "World"
console.log(b); // "Hello"

### OUTPUT 
Hello
World

World
Hello

# Case 2
##  alternative approch

let a = "Hello";
let b = "World";

// Swap using string concatenation and substring operations
a = a + b; // Concatenate strings: "HelloWorld"
b = a.substring(0, a.length - b.length); // Extract original `a` value: "Hello"
a = a.substring(b.length); // Extract original `b` value: "World"

console.log(a); // "World"
console.log(b); // "Hello"


