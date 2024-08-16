Hydration in React is the process of attaching React to server-rendered HTML. When a page is rendered on the server and sent to the client, React needs to "hydrate" the static HTML with interactive behavior by attaching event listeners and managing state.

In this detailed example, I’ll walk you through a basic setup of server-side rendering (SSR) with React and how hydration works. We’ll build a simple e-commerce app that utilizes SSR to render the initial HTML on the server and then hydrates it on the client.

### **1. Set Up the Server**

First, we’ll set up a server using Express to handle SSR.

#### **Server-Side Code (`server.js`)**

```javascript
import express from 'express';
import React from 'react';
import ReactDOMServer from 'react-dom/server';
import App from './src/App'; // Your main React component
import path from 'path';

const app = express();

// Serve static files from the "public" directory
app.use(express.static(path.resolve(__dirname, 'public')));

app.get('/', (req, res) => {
  // Render the app to a string
  const html = ReactDOMServer.renderToString(<App />);

  // Send the complete HTML page
  res.send(`
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>React Hydration Example</title>
    </head>
    <body>
      <div id="root">${html}</div>
      <script src="/client.js" type="module"></script>
    </body>
    </html>
  `);
});

// Start the server
app.listen(3000, () => {
  console.log('Server is listening on port 3000');
});
```

### **2. Create the React Application**

Create the React application that will be rendered and hydrated.

#### **Client-Side Code (`src/client.js`)**

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

// Hydrate the app on the client side
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

#### **Main React Component (`src/App.js`)**

```javascript
import React, { useState } from 'react';

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>React Hydration Example</h1>
      <p>Current Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default App;
```

### **3. HTML Template (`public/index.html`)**

This is the template that will be served to the client. Note that the client-side JavaScript (`client.js`) is included here.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>React Hydration Example</title>
</head>
<body>
  <div id="root"></div>
  <script src="/client.js" type="module"></script>
</body>
</html>
```

### **4. Build and Run**

Ensure you have all necessary dependencies installed (`express`, `react`, `react-dom`), and then build and run your application.

```bash
# Install dependencies
npm install express react react-dom

# Run the server
node server.js
```

### **How Hydration Works**

1. **Server-Side Rendering (SSR)**:
   - When a user requests a page, the server renders the React components into HTML using `ReactDOMServer.renderToString()`.
   - The generated HTML is sent to the client, which can be immediately displayed in the browser, providing a fast time-to-first-byte.

2. **Client-Side Hydration**:
   - Once the HTML is loaded in the browser, React takes over the static HTML. This is known as "hydration".
   - React attaches event listeners and reactivates the components so that they can manage state and handle user interactions.

   The `ReactDOM.createRoot` method is used to initialize the React application and attach it to the existing server-rendered HTML. 

### **Additional Details**

- **Data Fetching**: If your app needs to fetch data before rendering, you would typically fetch the data on the server and then pass it as props to your React components. This way, the server-rendered HTML includes the data, and React can seamlessly hydrate it on the client.

- **Matching HTML**: Ensure that the HTML generated on the server matches what React expects on the client. If there’s a mismatch, React will log warnings and may attempt to reconcile differences.

- **Performance**: Hydration is generally efficient, but ensure that your components are optimized for both SSR and client-side rendering. Avoid heavy computations or operations during hydration.

This example illustrates a basic setup for SSR and hydration in React. For more advanced use cases, you might integrate with frameworks like Next.js or Remix, which provide additional features and optimizations for SSR and hydration.