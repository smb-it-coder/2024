React 18, released in March 2022, introduced several significant features aimed at improving performance and enhancing the development experience. Here’s a rundown of some of the key new features:

1. **Concurrent Rendering**:
   - **Concurrent Mode**: This feature enables React to prepare multiple versions of the UI at the same time, allowing for smoother, more responsive user experiences. It helps in making updates more predictable and ensures that the UI remains interactive even during large state changes or data fetching.

2. **Automatic Batching**:
   - This feature allows React to batch multiple state updates into a single re-render, reducing the number of re-renders and improving performance. Automatic batching extends to updates inside `setTimeout`, `Promise`, and other asynchronous events.

3. **Suspense for Data Fetching**:
   - React 18 improves the Suspense feature, making it easier to handle asynchronous data fetching. This allows components to wait for data to be loaded before rendering, providing a more controlled way of handling loading states.

4. **Streaming Server-Side Rendering (SSR)**:
   - React 18 introduces support for streaming server-side rendering, which allows HTML to be sent to the client incrementally. This improves the time-to-first-byte and overall performance of server-rendered pages.

5. **Transition API**:
   - The Transition API enables you to mark certain updates as transitions, which can be deferred to avoid blocking user interactions. This helps to keep the application responsive during large state updates or navigations.

6. **`useId` Hook**:
   - The `useId` hook provides a way to generate unique IDs on the client and server, ensuring that IDs are consistent across server and client renders. This is useful for managing accessibility attributes and ensuring that IDs remain consistent during hydration.

7. **Improved Strict Mode**:
   - React 18’s Strict Mode helps with identifying potential problems in applications by activating additional checks and warnings. It includes features like detecting unsafe lifecycle methods and verifying the resilience of components against future changes.

8. **New Root API**:
   - React 18 introduces a new `createRoot` API for initializing your application, replacing the old `ReactDOM.render`. This new API is designed to work with the new features of React 18, such as Concurrent Mode and Automatic Batching.
Sure, I'll provide a set of examples demonstrating how the new features in React 18 can be applied to an e-commerce application. These examples will illustrate key features such as Concurrent Rendering, Automatic Batching, Suspense, Streaming SSR, Transition API, `useId`, and the new Root API.

### 1. **Concurrent Rendering**

Concurrent Rendering helps to keep your application responsive by rendering multiple versions of your UI simultaneously. For an e-commerce app, let's assume we have a product listing page that updates frequently. 

```jsx
import React, { Suspense, useState, useTransition } from 'react';
import ReactDOM from 'react-dom/client';

const ProductList = React.lazy(() => import('./ProductList'));
const Cart = React.lazy(() => import('./Cart'));

function App() {
  const [isPending, startTransition] = useTransition();
  const [showCart, setShowCart] = useState(false);

  return (
    <div>
      <button onClick={() => startTransition(() => setShowCart(!showCart))}>
        {showCart ? 'Hide Cart' : 'Show Cart'}
      </button>
      <Suspense fallback={<div>Loading products...</div>}>
        <ProductList />
      </Suspense>
      {showCart && (
        <Suspense fallback={<div>Loading cart...</div>}>
          <Cart />
        </Suspense>
      )}
    </div>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

In this example, `useTransition` is used to manage the state transition of showing/hiding the cart, ensuring that the user experience remains smooth.

### 2. **Automatic Batching**

Automatic Batching allows multiple state updates to be batched together, reducing the number of re-renders. For instance, updating the product quantity and cart total at the same time.

```jsx
import React, { useState } from 'react';
import ReactDOM from 'react-dom/client';

function Product({ id, price }) {
  const [quantity, setQuantity] = useState(1);
  const [cartTotal, setCartTotal] = useState(price);

  const handleQuantityChange = (event) => {
    const newQuantity = parseInt(event.target.value, 10);
    setQuantity(newQuantity);
    setCartTotal(newQuantity * price);
  };

  return (
    <div>
      <input type="number" value={quantity} onChange={handleQuantityChange} />
      <p>Total: ${cartTotal}</p>
    </div>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Product id={1} price={100} />);
```

Here, updating the quantity will also automatically update the cart total in a single re-render.

### 3. **Suspense for Data Fetching**

Suspense helps in handling asynchronous data fetching. For example, fetching product details:

```jsx
import React, { Suspense } from 'react';
import ReactDOM from 'react-dom/client';

// Simulating a data fetch
const fetchProductData = () =>
  new Promise((resolve) =>
    setTimeout(() => resolve({ name: 'Product A', price: 100 }), 1000)
  );

const ProductDetail = () => {
  const productData = fetchProductData();
  if (!productData) throw new Promise(() => {}); // Simulate loading state
  return (
    <div>
      <h1>{productData.name}</h1>
      <p>Price: ${productData.price}</p>
    </div>
  );
};

function App() {
  return (
    <div>
      <Suspense fallback={<div>Loading product details...</div>}>
        <ProductDetail />
      </Suspense>
    </div>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

In this example, `Suspense` handles the loading state while the product details are being fetched.

### 4. **Streaming Server-Side Rendering (SSR)**

Streaming SSR is more complex to demonstrate in a short example, but it essentially involves using React’s new SSR APIs to stream content to the client. Here's a simplified example:

```jsx
// server.js (Node.js server)

import express from 'express';
import React from 'react';
import ReactDOMServer from 'react-dom/server';
import App from './App'; // Your main App component

const app = express();

app.use(express.static('public'));

app.get('/', (req, res) => {
  const html = ReactDOMServer.renderToPipeableStream(<App />);
  res.write('<!DOCTYPE html><html><body>');
  html.pipe(res, { end: false });
  res.write('</body></html>');
  html.on('end', () => res.end());
});

app.listen(3000, () => console.log('Server listening on port 3000'));
```

This code shows how to use streaming SSR with `renderToPipeableStream` for a smoother initial load.

### 5. **Transition API**

The Transition API helps in managing state transitions without blocking user interactions:

```jsx
import React, { useState, useTransition } from 'react';
import ReactDOM from 'react-dom/client';

function ProductList() {
  const [products, setProducts] = useState([]);
  const [isPending, startTransition] = useTransition();

  const fetchProducts = () => {
    startTransition(() => {
      // Simulate a slow network request
      setTimeout(() => {
        setProducts(['Product A', 'Product B', 'Product C']);
      }, 2000);
    });
  };

  return (
    <div>
      <button onClick={fetchProducts}>Load Products</button>
      {isPending && <p>Loading products...</p>}
      <ul>
        {products.map((product, index) => (
          <li key={index}>{product}</li>
        ))}
      </ul>
    </div>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<ProductList />);
```

Here, `useTransition` is used to handle the state update of fetching products, ensuring the UI remains responsive.

### 6. **`useId` Hook**

The `useId` hook provides unique IDs for accessibility attributes:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';

function ProductForm() {
  const productId = React.useId();

  return (
    <form>
      <label htmlFor={productId}>Product Name</label>
      <input id={productId} name="productName" type="text" />
    </form>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<ProductForm />);
```

In this example, `useId` generates a unique ID for the input element, ensuring proper accessibility.

### 7. **New Root API**

The new Root API is used to create and render the root of your application:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

This new API is used to initialize the React application and supports all the new features introduced in React 18.

These examples should give you a good starting point on how to utilize React 18 features in an e-commerce application.