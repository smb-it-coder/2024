In JavaScript, both normal functions (also known as traditional functions) and arrow functions are used to define functions, but they have some important differences. Here's a comparison of the two:

### Normal Function

#### Syntax:
```javascript
function normalFunction(param1, param2) {
  // function body
}
```

#### Key Features:
1. **`this` Binding**: The value of `this` inside a normal function is determined by how the function is called. It can be the object that owns the function, or it can be explicitly set using `call()`, `apply()`, or `bind()`.

2. **`arguments` Object**: Normal functions have access to the `arguments` object, which is an array-like object representing the arguments passed to the function.

3. **Constructors**: Normal functions can be used as constructors with the `new` keyword to create instances of objects.

4. **`prototype` Property**: Normal functions have a `prototype` property that allows you to add methods or properties to the prototype of the function.

#### Example:
```javascript
function normalFunction(x, y) {
  console.log(this); // 'this' depends on how the function is called
  console.log(arguments); // access to 'arguments' object
}

const obj = {
  method: normalFunction
};

obj.method(1, 2); // 'this' is 'obj'
```

### Arrow Function

#### Syntax:
```javascript
const arrowFunction = (param1, param2) => {
  // function body
};
```

#### Key Features:
1. **`this` Binding**: Arrow functions do not have their own `this` context. Instead, they inherit `this` from the surrounding lexical scope (the context in which they were created). This is known as lexical scoping.

2. **No `arguments` Object**: Arrow functions do not have their own `arguments` object. If you need to access arguments, you would typically use rest parameters (`...args`).

3. **Not Constructible**: Arrow functions cannot be used as constructors and will throw an error if used with the `new` keyword.

4. **No `prototype` Property**: Arrow functions do not have a `prototype` property.

#### Example:
```javascript
const arrowFunction = (x, y) => {
  console.log(this); // 'this' is inherited from the surrounding context
  // console.log(arguments); // 'arguments' object is not available
};

const obj = {
  method: arrowFunction
};

obj.method(1, 2); // 'this' is the 'this' from where 'arrowFunction' was defined
```

### Summary

- **`this` Binding**: Normal functions have their own `this`, while arrow functions inherit `this` from their lexical scope.
- **`arguments` Object**: Normal functions have access to `arguments`, but arrow functions do not.
- **Constructors**: Normal functions can be constructors; arrow functions cannot.
- **`prototype`**: Normal functions have a `prototype` property; arrow functions do not.

Choosing between the two depends on your specific needs, such as whether you need a function to maintain its own `this` context or you want a more concise syntax without access to `arguments`.