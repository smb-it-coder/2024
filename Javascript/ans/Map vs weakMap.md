In JavaScript, `Map` and `WeakMap` are both data structures used for storing key-value pairs, but they have different properties and use cases. Here’s a detailed comparison of `Map` vs `WeakMap`:

### Map

**`Map`** is a built-in JavaScript object that stores key-value pairs. It has several key features:

- **Keys and Values**: Both keys and values in a `Map` can be of any data type (including objects and primitive values).
- **Ordering**: `Map` maintains the insertion order of keys. This means that when iterating over the map, the order of keys will be the same as the order in which they were added.
- **Size**: `Map` has a `size` property that returns the number of key-value pairs in the map.
- **Iteration**: `Map` provides methods to iterate over its keys, values, and entries in insertion order.

**Example of `Map`:**

```javascript
const map = new Map();

// Adding key-value pairs
map.set('name', 'Alice');
map.set(1, 'Number one');
map.set(true, 'Boolean true');

// Accessing values
console.log(map.get('name')); // Output: Alice

// Checking existence
console.log(map.has(1)); // Output: true

// Iterating over Map
map.forEach((value, key) => {
    console.log(`${key}: ${value}`);
});
// Output:
// name: Alice
// 1: Number one
// true: Boolean true

// Getting the size
console.log(map.size); // Output: 3

// Deleting a key
map.delete(1);
console.log(map.size); // Output: 2
```

### WeakMap

**`WeakMap`** is a special type of map that is designed to work with objects as keys and has unique characteristics:

- **Keys**: In a `WeakMap`, keys must be objects (not primitives). Non-object keys will throw a `TypeError`.
- **Garbage Collection**: `WeakMap` keys are weakly referenced. This means that if there are no other references to the key object, it can be garbage collected. Consequently, `WeakMap` does not prevent its keys from being garbage collected.
- **Size**: `WeakMap` does not have a `size` property. You cannot determine the number of entries.
- **Iteration**: `WeakMap` does not provide methods for iteration over its entries, as it is designed to not interfere with garbage collection.

**Example of `WeakMap`:**

```javascript
const weakMap = new WeakMap();
const obj1 = {};
const obj2 = {};

// Adding key-value pairs
weakMap.set(obj1, 'Value for obj1');
weakMap.set(obj2, 'Value for obj2');

// Accessing values
console.log(weakMap.get(obj1)); // Output: Value for obj1

// Checking existence
console.log(weakMap.has(obj2)); // Output: true

// Deleting a key
weakMap.delete(obj1);
console.log(weakMap.has(obj1)); // Output: false

// Key must be an object
// weakMap.set('key', 'value'); // Throws TypeError
```

### Key Differences

1. **Key Types**:
   - **`Map`**: Can use any data type as a key (e.g., strings, numbers, objects).
   - **`WeakMap`**: Can only use objects as keys.

2. **Garbage Collection**:
   - **`Map`**: Keeps a strong reference to keys and values, which prevents garbage collection as long as the map itself is referenced.
   - **`WeakMap`**: Keys are weakly referenced, allowing them to be garbage collected if there are no other references to the key object.

3. **Iteration**:
   - **`Map`**: Supports iteration methods such as `forEach`, `keys`, `values`, and `entries`.
   - **`WeakMap`**: Does not support iteration methods. This is intentional to avoid issues with garbage collection.

4. **Size**:
   - **`Map`**: Provides a `size` property to get the number of entries.
   - **`WeakMap`**: Does not provide a `size` property.

### Use Cases

- **`Map`**: Use `Map` when you need a general-purpose key-value store where keys can be of any type and you need to iterate over the entries or need to know the size.

- **`WeakMap`**: Use `WeakMap` when you need to associate data with objects but want to ensure that the data is automatically cleaned up when the object is no longer in use, without preventing garbage collection.

Understanding these differences helps you choose the right data structure based on your specific requirements for handling key-value pairs in JavaScript.