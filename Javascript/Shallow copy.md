In JavaScript, a shallow copy of an object or array means creating a new object or array with the same top-level properties as the original, but not creating deep copies of nested objects or arrays. Modifications to nested properties will still affect the original object or array.

### Shallow Copy of Objects

You can create a shallow copy of an object using several methods:

1. **Object.assign()**

   ```javascript
   const original = { name: 'Alice', age: 25, address: { city: 'Wonderland' } };
   const copy = Object.assign({}, original);
   
   copy.name = 'Bob'; // Modify a top-level property
   copy.address.city = 'New City'; // Modify a nested property

   console.log(original); // { name: 'Alice', age: 25, address: { city: 'New City' } }
   console.log(copy);     // { name: 'Bob', age: 25, address: { city: 'New City' } }
   ```

2. **Spread Operator**

   ```javascript
   const original = { name: 'Alice', age: 25, address: { city: 'Wonderland' } };
   const copy = { ...original };

   copy.name = 'Bob'; // Modify a top-level property
   copy.address.city = 'New City'; // Modify a nested property

   console.log(original); // { name: 'Alice', age: 25, address: { city: 'New City' } }
   console.log(copy);     // { name: 'Bob', age: 25, address: { city: 'New City' } }
   ```

3. **Object.fromEntries()** (when combined with `Object.entries()`)

   ```javascript
   const original = { name: 'Alice', age: 25, address: { city: 'Wonderland' } };
   const copy = Object.fromEntries(Object.entries(original));

   copy.name = 'Bob'; // Modify a top-level property
   copy.address.city = 'New City'; // Modify a nested property

   console.log(original); // { name: 'Alice', age: 25, address: { city: 'New City' } }
   console.log(copy);     // { name: 'Bob', age: 25, address: { city: 'New City' } }
   ```

### Shallow Copy of Arrays

For arrays, you can use:

1. **Array.slice()**

   ```javascript
   const original = [1, 2, { foo: 'bar' }];
   const copy = original.slice();

   copy[0] = 99; // Modify a top-level element
   copy[2].foo = 'baz'; // Modify a nested object

   console.log(original); // [1, 2, { foo: 'baz' }]
   console.log(copy);     // [99, 2, { foo: 'baz' }]
   ```

2. **Spread Operator**

   ```javascript
   const original = [1, 2, { foo: 'bar' }];
   const copy = [...original];

   copy[0] = 99; // Modify a top-level element
   copy[2].foo = 'baz'; // Modify a nested object

   console.log(original); // [1, 2, { foo: 'baz' }]
   console.log(copy);     // [99, 2, { foo: 'baz' }]
   ```

### Key Points

- **Shallow Copy**: Only the top level is copied; nested objects/arrays are shared between the original and the copy.
- **Deep Copy**: Requires creating copies of nested objects/arrays recursively, which can be achieved using libraries like `lodash` with `cloneDeep()` or custom recursive functions.

For deep cloning, you might consider:

```javascript
const _ = require('lodash');
const original = { name: 'Alice', age: 25, address: { city: 'Wonderland' } };
const deepCopy = _.cloneDeep(original);

deepCopy.address.city = 'New City';

console.log(original); // { name: 'Alice', age: 25, address: { city: 'Wonderland' } }
console.log(deepCopy); // { name: 'Alice', age: 25, address: { city: 'New City' } }
```

Understanding shallow and deep copying is crucial for managing state and data integrity in JavaScript applications.