# Q1 

greetings();
var greetings = function(){
console.log("first greetings")
}
greetings();

function greetings(){
console.log("second greetings")
}
greetings();


In JavaScript, function declarations and function expressions behave differently, which is why your code produces specific results. Let’s break it down:

1. **Function Declaration Hoisting**:
   ```javascript
   function greetings(){
       console.log("second greetings");
   }
   ```
   This is a function declaration. In JavaScript, function declarations are hoisted to the top of their scope. This means the function `greetings` is available throughout the entire scope, including before its declaration in the code.

2. **Function Expression**:
   ```javascript
   var greetings = function(){
       console.log("first greetings");
   }
   ```
   This is a function expression assigned to a variable. Function expressions are not hoisted in the same way. The variable `greetings` is hoisted, but it is initially undefined until the function expression is evaluated.

Here’s what happens when you run your code:

```javascript
greetings(); // This calls the function expression, which is undefined at this point
var greetings = function(){
    console.log("first greetings");
}
greetings(); // This calls the function expression after it has been assigned
function greetings(){
    console.log("second greetings");
}
greetings(); // This calls the function declaration
```

        ### Output Breakdown

        1. **`greetings();`** (Before function expression assignment): 
        - At this point, the `greetings` variable has been hoisted but not yet assigned the function expression, so it is `undefined`. Calling `greetings()` results in a `TypeError` because `undefined` is not a function.

        2. **`var greetings = function() { console.log("first greetings"); }`**:
        - Now the `greetings` variable is assigned to a function expression that logs `"first greetings"`.

        3. **`greetings();`** (After function expression assignment):
        - This correctly logs `"first greetings"` because the `greetings` variable now holds the function expression.

        4. **Function Declaration (`function greetings() { console.log("second greetings"); }`)**:
        - This declaration is hoisted, so it overrides the previous `greetings` function expression. 

        5. **`greetings();`** (After function declaration):
        - This call logs `"second greetings"` because the function declaration takes precedence.

        ### Correct Output

        So, if the code is corrected to properly show the sequence of function calls and declarations, it will produce:

        1. **Error**: `TypeError: greetings is not a function` (or similar, depending on the environment) due to calling `greetings` before the function expression is defined.
        2. **`first greetings`**: After the function expression assignment.
        3. **`second greetings`**: After the function declaration, which overrides the previous function expression.

        To avoid confusion, it's good practice to keep function declarations and expressions separate and avoid naming conflicts.

# Q2 
WeakMap vs WeakSet 
# 3 
# 4 
How to validate props in reactJS
# 5 Abstract class vs Normal class in Javascript
# 6 What is the oops concept not supported by Javascript 
# collection vs capped collection
# How to dynamically loading module
# TypeInference
# Type Inference
# How to caching into mongodb
