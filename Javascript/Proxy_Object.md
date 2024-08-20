In JavaScript, a Proxy object is a powerful feature introduced in ECMAScript 2015 (ES6) that allows you to define custom behavior for fundamental operations on objects. Essentially, a Proxy acts as a wrapper around another object (called the target) and lets you intercept and customize operations like property access, assignment, and method calls.

Here's a basic overview of how Proxy works:

1. **Proxy Constructor**: You create a Proxy by passing two arguments:
   - The target object that you want to wrap.
   - A handler object that defines traps (methods) for intercepting operations on the target.

2. **Handler Object**: This object contains traps (methods) for intercepting operations such as `get`, `set`, `has`, `deleteProperty`, and others. Each trap is a function that can modify or replace the default behavior of the operation.

### Example of a Proxy Object

Let's create a simple example where we use a Proxy to intercept property access and modification on a target object.

```javascript
// The target object
const target = {
  message: "Hello, world!"
};

// The handler object with traps
const handler = {
  // Trap for getting a property value
  get(target, property, receiver) {
    console.log(`Getting property: ${property}`);
    return Reflect.get(target, property, receiver);
  },
  
  // Trap for setting a property value
  set(target, property, value, receiver) {
    console.log(`Setting property: ${property} to ${value}`);
    return Reflect.set(target, property, value, receiver);
  }
};

// Creating a Proxy object
const proxy = new Proxy(target, handler);

// Using the proxy
console.log(proxy.message);  // Triggers the get trap, logs "Getting property: message" and prints "Hello, world!"

proxy.message = "Hello, Proxy!";  // Triggers the set trap, logs "Setting property: message to Hello, Proxy!"
console.log(proxy.message);  // Prints "Hello, Proxy!"
```

### Explanation

1. **Target Object**: `target` is a simple object with a single property `message`.

2. **Handler Object**: `handler` contains two traps:
   - `get`: This trap logs a message when a property is accessed and then delegates the actual property retrieval to the `Reflect.get` method.
   - `set`: This trap logs a message when a property is set and then delegates the actual property modification to the `Reflect.set` method.

3. **Proxy Creation**: `new Proxy(target, handler)` creates a new Proxy object that wraps around the `target` object, allowing us to intercept and customize interactions with it.

4. **Proxy Usage**: When accessing or modifying properties on `proxy`, the respective traps in the `handler` object are triggered.

This basic example demonstrates how Proxies can be used to add custom behavior for fundamental operations. Proxies are particularly useful for scenarios like logging, validation, or implementing more complex patterns such as observables and virtualized objects.