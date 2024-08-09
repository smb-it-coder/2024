In JavaScript, cloning refers to creating a copy of an object or array. The key distinction between deep cloning and shallow cloning lies in how the nested structures within the original object or array are copied.

### Shallow Clone

A **shallow clone** creates a new object or array but does not create copies of nested objects or arrays. Instead, it copies references to these nested structures. This means that if you modify a nested object in the clone, the change will also reflect in the original object.

#### Methods for Shallow Cloning:

1. **Object.assign()**:

   ```javascript
   const original = { a: 1, b: { c: 2 } };
   const shallowCopy = Object.assign({}, original);
   shallowCopy.b.c = 3;

   console.log(original.b.c); // Output: 3
   ```

2. **Spread Operator (for objects)**:

   ```javascript
   const original = { a: 1, b: { c: 2 } };
   const shallowCopy = { ...original };
   shallowCopy.b.c = 3;

   console.log(original.b.c); // Output: 3
   ```

3. **Array's slice() method or spread operator (for arrays)**:

   ```javascript
   const original = [1, 2, [3, 4]];
   const shallowCopy = [...original];
   shallowCopy[2][0] = 99;

   console.log(original[2][0]); // Output: 99
   ```

### Deep Clone

A **deep clone** creates a new object or array and recursively copies all nested objects or arrays. Changes to the nested structures in the clone do not affect the original object or array.

#### Methods for Deep Cloning:

1. **Using JSON Methods**:

   ```javascript
   const original = { a: 1, b: { c: 2 } };
   const deepCopy = JSON.parse(JSON.stringify(original));
   deepCopy.b.c = 3;

   console.log(original.b.c); // Output: 2
   ```

   **Note:** This method has limitations, such as not handling functions, `undefined`, `Symbol`, and special object types like `Date`, `RegExp`, `Map`, `Set`, etc.

2. **Using a Library**:

   Libraries like `Lodash` provide deep cloning functions that handle more complex scenarios.

   ```javascript
   // Using Lodash's cloneDeep function
   const _ = require('lodash');
   const original = { a: 1, b: { c: 2 } };
   const deepCopy = _.cloneDeep(original);
   deepCopy.b.c = 3;

   console.log(original.b.c); // Output: 2
   ```

3. **Custom Recursive Function**:

   You can also write your own deep cloning function, but it requires handling various data types and edge cases.

   ```javascript
   function deepClone(obj) {
       if (obj === null || typeof obj !== 'object') {
           return obj;
       }

       if (Array.isArray(obj)) {
           return obj.map(deepClone);
       }

       const clone = {};
       for (const key in obj) {
           if (obj.hasOwnProperty(key)) {
               clone[key] = deepClone(obj[key]);
           }
       }
       return clone;
   }

   const original = { a: 1, b: { c: 2 } };
   const deepCopy = deepClone(original);
   deepCopy.b.c = 3;

   console.log(original.b.c); // Output: 2
   ```

### Summary

- **Shallow Clone**: Copies the top-level properties and keeps references to nested objects. Changes in nested structures affect both the original and the clone.
- **Deep Clone**: Recursively copies all levels of nested structures, creating independent clones of the nested objects. Changes in the clone do not affect the original object.

Choose the cloning method based on your specific needs, especially when dealing with complex objects and arrays.