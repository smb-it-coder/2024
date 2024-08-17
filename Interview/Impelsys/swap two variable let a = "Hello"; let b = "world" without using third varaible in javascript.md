Swapping two variables in JavaScript without using a third variable can be done using several techniques. Here are a few methods you can use:

### **1. Using Arithmetic Operations**

This method is typically used for numeric values, but can be adapted for string values as well. It works by leveraging the arithmetic properties of numbers.

```javascript
let a = "Hello";
let b = "world";

// Convert strings to numbers to perform arithmetic swap
a = a + b;       // Concatenate strings: "Hello" + "world" = "Helloworld"
b = a.substring(0, a.length - b.length); // Extract the original value of 'a': "Hello"
a = a.substring(b.length); // Extract the original value of 'b': "world"

console.log(a); // Output: "world"
console.log(b); // Output: "Hello"
```

### **2. Using Array Destructuring (ES6+ Syntax)**

Array destructuring is a modern and concise way to swap variables, leveraging JavaScript's ability to destructure arrays.

```javascript
let a = "Hello";
let b = "world";

// Swap using array destructuring
[a, b] = [b, a];

console.log(a); // Output: "world"
console.log(b); // Output: "Hello"
```

### **3. Using XOR Bitwise Operation**

The XOR bitwise operation is a classic method for swapping numeric values without a temporary variable. However, it's generally not used for strings because it is not meaningful for non-numeric types.

```javascript
let a = "Hello";
let b = "world";

// XOR swap is not directly applicable to strings, but here is how it works with numbers
// let a = 5; 
// let b = 10;
// a = a ^ b; // XOR operation
// b = a ^ b; // b = (a ^ b) ^ b = a
// a = a ^ b; // a = (a ^ b) ^ a = b

// For strings, the array destructuring method is preferred
```

### **4. Using Template Literals**

Template literals can also be used to swap variables by creating a temporary combined string.

```javascript
let a = "Hello";
let b = "world";

// Swap using template literals
a = `${a}${b}`;   // Combine both values
b = a.substring(0, a.length - b.length); // Extract the original 'a' value
a = a.substring(b.length); // Extract the original 'b' value

console.log(a); // Output: "world"
console.log(b); // Output: "Hello"
```

### **Summary**

- **Arithmetic Operations**: Concatenate and then extract values. Suitable for strings but a bit complex.
- **Array Destructuring**: Concise and modern, recommended for swapping variables.
- **XOR Bitwise Operation**: Mainly for numbers; not recommended for strings.
- **Template Literals**: Similar to arithmetic operations but with string operations.

**Array destructuring** is generally the most straightforward and modern approach in JavaScript for swapping variables without using a temporary variable.