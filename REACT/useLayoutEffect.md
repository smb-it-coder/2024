`useLayoutEffect` is a React hook that is similar to `useEffect`, but it runs synchronously after all DOM mutations. This means it runs immediately after the DOM has been updated but before the browser has painted the changes. It is useful when you need to perform side effects that require reading layout from the DOM and synchronously applying changes.

### Syntax

```javascript
useLayoutEffect(effect: () => void | (() => void), deps?: DependencyList): void
```

### Parameters

1. **effect**: A function that contains the code you want to run after the DOM updates. This function can optionally return a cleanup function to clean up any side effects.
2. **deps** (optional): An array of dependencies that determines when the `effect` should be run. If the dependencies change, the effect will be re-run.

### Examples

#### Basic Usage

```javascript
import React, { useLayoutEffect, useRef } from 'react';

function Example() {
  const divRef = useRef(null);

  useLayoutEffect(() => {
    if (divRef.current) {
      // This code runs synchronously after the DOM is updated
      console.log('Div width:', divRef.current.offsetWidth);
    }
  }, []); // Empty dependency array means this effect runs once after the initial render

  return <div ref={divRef}>Hello, World!</div>;
}
```

In this example:
- `useLayoutEffect` runs synchronously after the DOM has been updated.
- `divRef.current.offsetWidth` will give the width of the `div` element immediately after it has been rendered but before the browser paints.

#### Dependencies

If you have dependencies, `useLayoutEffect` will re-run whenever those dependencies change:

```javascript
import React, { useLayoutEffect, useRef, useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);
  const divRef = useRef(null);

  useLayoutEffect(() => {
    if (divRef.current) {
      console.log('Div width:', divRef.current.offsetWidth);
    }
  }, [count]); // This effect will run whenever `count` changes

  return (
    <div>
      <div ref={divRef}>Count: {count}</div>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

In this example:
- The effect depends on `count`.
- Each time `count` changes, the `useLayoutEffect` will run again, providing the updated width of the `div`.

#### Cleanup Function

If you need to clean up after the effect, you can return a cleanup function:

```javascript
import React, { useLayoutEffect, useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useLayoutEffect(() => {
    console.log('Effect ran');
    
    // Cleanup function
    return () => {
      console.log('Cleanup');
    };
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

In this example:
- When `count` changes, `useLayoutEffect` runs the effect.
- Before running the effect again (or when the component unmounts), React runs the cleanup function.

### Key Points

- **Synchronous Execution**: `useLayoutEffect` runs synchronously after the DOM has been updated, making it suitable for measuring layout or applying styles that need to happen immediately.
- **Avoid Blocking Paint**: Since it runs before the browser paints, be cautious not to include time-consuming operations in `useLayoutEffect` as it can affect rendering performance.
- **Usage vs. `useEffect`**: Use `useLayoutEffect` when you need to measure or make changes to the DOM before the browser paints; otherwise, `useEffect` is typically sufficient for most side effects.

Choosing between `useLayoutEffect` and `useEffect` usually depends on whether you need to measure DOM elements and adjust layout before the browser renders the changes.