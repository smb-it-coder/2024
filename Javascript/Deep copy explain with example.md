In JavaScript, deep copying an object means creating a new object that is a complete, independent copy of the original object, including all nested objects. This is different from a shallow copy, which only copies the top-level properties and shares references to nested objects.

### Example of Deep Copy in JavaScript

Let's go through an example to illustrate the difference between a shallow copy and a deep copy.

#### Original Object

```javascript
const originalObject = {
  name: 'Alice',
  age: 30,
  address: {
    street: '123 Main St',
    city: 'Wonderland'
  }
};
```

#### Shallow Copy

A shallow copy can be created using `Object.assign()` or the spread operator `{...}`. Both methods only perform a shallow copy:

```javascript
const shallowCopy = Object.assign({}, originalObject);
// or
const shallowCopy = {...originalObject};
```

If you modify a nested property in `shallowCopy`, it will also affect `originalObject` because the nested objects are shared between them.

```javascript
shallowCopy.address.street = '456 Elm St';

console.log(originalObject.address.street); // Output will be '456 Elm St'
console.log(shallowCopy.address.street);    // Output will be '456 Elm St'
```

#### Deep Copy

To perform a deep copy, you can use various methods. One common approach is to use JSON serialization and deserialization:

```javascript
const deepCopy = JSON.parse(JSON.stringify(originalObject));
```

With this method, `deepCopy` is a fully independent copy of `originalObject`, including all nested properties.

```javascript
deepCopy.address.street = '456 Elm St';

console.log(originalObject.address.street); // Output will be '123 Main St'
console.log(deepCopy.address.street);       // Output will be '456 Elm St'
```

### Important Notes

1. **JSON Method Limitations**:
   - **Non-JSON-compatible Values**: This method cannot handle non-JSON data types such as `undefined`, functions, symbols, or `Date` objects. It also loses prototype information.
   - **Circular References**: This method cannot handle objects with circular references and will throw an error.

2. **Using Libraries**:
   - For more robust deep copying, especially in complex scenarios, you might use libraries like Lodash which provide a `cloneDeep` function:
     ```javascript
     const _ = require('lodash');
     const deepCopy = _.cloneDeep(originalObject);
     ```

3. **Manual Deep Copy**:
   - You can also manually create a deep copy function, but this can be complex and error-prone depending on the structure of the objects.

### Summary

- **Shallow Copy**: Copies only the top level of the object. Nested objects are shared between the original and the copy.
- **Deep Copy**: Creates a completely independent copy of the original object, including all nested objects. This ensures that changes to the copied object do not affect the original object.

Using the JSON method is often the easiest way to achieve a deep copy for simple objects, but for more complex cases, consider using dedicated libraries or implementing a custom deep copy function.