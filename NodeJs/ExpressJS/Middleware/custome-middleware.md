Creating custom middleware in Express.js is straightforward. Custom middleware functions allow you to add functionality to the request-response cycle, such as logging, authentication, request modification, or error handling. Here’s a step-by-step guide on how to create and use custom middleware in Express.js:

### 1. Basic Structure of Middleware

A middleware function in Express is defined with the following signature:

```javascript
function myMiddleware(req, res, next) {
  // Middleware logic
  next(); // Pass control to the next middleware or route handler
}
```

- **`req`**: The request object, representing the HTTP request.
- **`res`**: The response object, representing the HTTP response.
- **`next`**: A function to pass control to the next middleware or route handler in the stack.

### 2. Adding Custom Middleware

You can add custom middleware to your Express application at the application level or router level. Here’s how to do both:

#### Application-Level Middleware

To apply middleware globally to all routes and HTTP methods, use the `app.use()` method:

```javascript
const express = require('express');
const app = express();

// Define custom middleware
function customMiddleware(req, res, next) {
  console.log('Custom middleware executed');
  next(); // Pass control to the next middleware or route handler
}

// Apply middleware globally
app.use(customMiddleware);

app.get('/', (req, res) => {
  res.send('Home Page');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

In this example, `customMiddleware` logs a message for every request to the server.

#### Router-Level Middleware

To apply middleware to a specific subset of routes, create a router and use middleware with `router.use()`:

```javascript
const express = require('express');
const app = express();
const router = express.Router();

// Define custom middleware
function customRouterMiddleware(req, res, next) {
  console.log('Router-level middleware executed');
  next(); // Pass control to the next middleware or route handler
}

// Apply middleware to the router
router.use(customRouterMiddleware);

router.get('/info', (req, res) => {
  res.send('Info Page');
});

// Mount the router at /api
app.use('/api', router);

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

In this example, `customRouterMiddleware` only logs messages for routes handled by the router mounted at `/api`.

### 3. Middleware with Parameters

You can also create middleware that accepts parameters by using a function that returns a middleware function:

```javascript
const express = require('express');
const app = express();

// Middleware factory function
function logRequestDetails(param) {
  return function (req, res, next) {
    console.log(`${param}: ${req.method} ${req.url}`);
    next(); // Pass control to the next middleware or route handler
  };
}

// Use middleware with parameters
app.use(logRequestDetails('Request details'));

app.get('/', (req, res) => {
  res.send('Home Page');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

In this example, `logRequestDetails` is a middleware factory function that accepts a parameter and returns a middleware function. The returned middleware logs request details with the provided parameter.

### 4. Error-Handling Middleware

Error-handling middleware has four parameters: `err`, `req`, `res`, and `next`. It’s used to catch and handle errors that occur during request processing:

```javascript
const express = require('express');
const app = express();

// Route that causes an error
app.get('/error', (req, res) => {
  throw new Error('Something went wrong!');
});

// Error-handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack); // Log the error
  res.status(500).send('Something broke!');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

In this example, the error-handling middleware catches errors thrown in any route handler and sends a generic error message as the response.

### Summary

- **Basic Middleware**: Functions that take `req`, `res`, and `next` and call `next()` to pass control.
- **Application-Level Middleware**: Applied globally using `app.use()`.
- **Router-Level Middleware**: Applied to specific routes using `router.use()`.
- **Middleware with Parameters**: Factory functions that return middleware functions.
- **Error-Handling Middleware**: Functions with four parameters to handle errors.

Custom middleware is a powerful way to manage various aspects of request handling in Express.js, making it easier to build flexible and maintainable applications.