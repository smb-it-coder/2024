## sum(4)(8)
To create a function in JavaScript that can be called like `sum(4)(8)` and returns the sum of 4 and 8, you need to use a technique known as **currying**. Currying is a functional programming concept where a function that takes multiple arguments is transformed into a sequence of functions each taking a single argument.

Here’s how you can implement this in JavaScript:

```javascript
function sum(a) {
  return function(b) {
    return a + b;
  };
}

// Example usage:
console.log(sum(4)(8)); // Output: 12
```

### Explanation:

1. **`sum(a)`**: This is a function that takes a single argument `a`.
2. **`return function(b)`**: Inside this function, another function is returned that takes a single argument `b`.
3. **`return a + b`**: The inner function returns the sum of `a` and `b`.

In this implementation:
- When you call `sum(4)`, it returns a new function that expects another argument.
- When you then call this returned function with `8` (i.e., `sum(4)(8)`), it computes and returns the result of `4 + 8`, which is `12`.