In JavaScript, a higher-order function is a function that either takes one or more functions as arguments or returns a function as its result. Higher-order functions are a key concept in functional programming and allow for more abstract and reusable code. They enable patterns like function composition, currying, and more.

### Examples of Higher-Order Functions

1. **Function that Takes a Function as an Argument**:

   Higher-order functions can accept functions as arguments. For example, the `Array.prototype.map` method is a higher-order function that takes a callback function to apply to each element of the array:

   ```javascript
   function multiplyByTwo(x) {
       return x * 2;
   }

   const numbers = [1, 2, 3, 4];
   const doubledNumbers = numbers.map(multiplyByTwo);

   console.log(doubledNumbers); // Output: [2, 4, 6, 8]
   ```

2. **Function that Returns a Function**:

   Higher-order functions can also return functions. For example, a function that returns a function for adding a specific number:

   ```javascript
   function createAdder(x) {
       return function(y) {
           return x + y;
       };
   }

   const addFive = createAdder(5);
   console.log(addFive(10)); // Output: 15
   ```

3. **Function Composition**:

   Higher-order functions are often used to compose other functions. For example, composing two functions:

   ```javascript
   function compose(f, g) {
       return function(x) {
           return f(g(x));
       };
   }

   function double(x) {
       return x * 2;
   }

   function square(x) {
       return x * x;
   }

   const doubleThenSquare = compose(square, double);
   console.log(doubleThenSquare(3)); // Output: 36
   ```

### Common Higher-Order Functions in JavaScript

1. **`Array.prototype.map`**:

   Transforms each element of an array based on the provided function.

   ```javascript
   const numbers = [1, 2, 3];
   const squares = numbers.map(num => num * num);
   console.log(squares); // Output: [1, 4, 9]
   ```

2. **`Array.prototype.filter`**:

   Filters elements of an array based on the provided function.

   ```javascript
   const numbers = [1, 2, 3, 4, 5];
   const evenNumbers = numbers.filter(num => num % 2 === 0);
   console.log(evenNumbers); // Output: [2, 4]
   ```

3. **`Array.prototype.reduce`**:

   Reduces an array to a single value based on the provided function.

   ```javascript
   const numbers = [1, 2, 3, 4];
   const sum = numbers.reduce((acc, num) => acc + num, 0);
   console.log(sum); // Output: 10
   ```

4. **`Function.prototype.bind`**:

   Returns a new function with a specified `this` context and initial arguments.

   ```javascript
   function greet(greeting, name) {
       return `${greeting}, ${name}!`;
   }

   const greetHello = greet.bind(null, 'Hello');
   console.log(greetHello('Alice')); // Output: Hello, Alice!
   ```

### Benefits of Higher-Order Functions

- **Abstraction**: Higher-order functions help abstract common patterns of code into reusable functions.
- **Composability**: Functions can be composed and combined in flexible ways to build complex functionality from simpler functions.
- **Declarative Style**: Higher-order functions often promote a declarative style of programming, where you describe what you want to achieve rather than how to achieve it.

### Summary

Higher-order functions are a powerful feature in JavaScript that enable more abstract, concise, and flexible coding patterns. By leveraging these functions, you can write more modular and reusable code, making your programs more expressive and easier to maintain.