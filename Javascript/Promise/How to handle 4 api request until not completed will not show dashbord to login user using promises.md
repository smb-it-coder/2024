# How to handle 4 api request until not completed will not show dashbord to login user using promises

To handle multiple API requests and ensure that a dashboard is not displayed until all requests are completed, you can use JavaScript promises. Promises are a powerful way to manage asynchronous operations. Here’s a step-by-step guide on how you can achieve this:

### **Scenario**

Assume you have four API requests that need to be completed before showing the dashboard to the logged-in user. You want to ensure that the dashboard is only shown when all four requests have successfully completed.

### **Steps**

1. **Create Functions for API Requests:**
   Each function should return a promise that resolves when the API request completes.

   ```javascript
   function apiRequest1() {
     return new Promise((resolve, reject) => {
       // Simulate an API request
       setTimeout(() => resolve('Response from API 1'), 1000);
     });
   }

   function apiRequest2() {
     return new Promise((resolve, reject) => {
       // Simulate an API request
       setTimeout(() => resolve('Response from API 2'), 1000);
     });
   }

   function apiRequest3() {
     return new Promise((resolve, reject) => {
       // Simulate an API request
       setTimeout(() => resolve('Response from API 3'), 1000);
     });
   }

   function apiRequest4() {
     return new Promise((resolve, reject) => {
       // Simulate an API request
       setTimeout(() => resolve('Response from API 4'), 1000);
     });
   }
   ```

2. **Use `Promise.all` to Handle Multiple Requests:**
   `Promise.all` is used to wait for all promises to resolve or for one to reject. It takes an array of promises and returns a new promise that resolves when all the input promises have resolved.

   ```javascript
   function fetchAllData() {
     return Promise.all([apiRequest1(), apiRequest2(), apiRequest3(), apiRequest4()])
       .then((responses) => {
         // All requests completed successfully
         console.log('All API requests completed:', responses);
         // Show dashboard here
         showDashboard();
       })
       .catch((error) => {
         // Handle any errors from any of the requests
         console.error('Error in API requests:', error);
         // Optionally, show an error message to the user
       });
   }
   ```

3. **Define the Function to Show the Dashboard:**

   ```javascript
   function showDashboard() {
     console.log('Showing the dashboard to the user');
     // Code to display the dashboard
   }
   ```

4. **Execute the Fetch and Handle UI:**

   Call the `fetchAllData` function when the user logs in or when appropriate.

   ```javascript
   // Example: Call fetchAllData when the user logs in
   document.getElementById('loginButton').addEventListener('click', () => {
     fetchAllData();
   });
   ```

### **Complete Example**

Here’s a complete example combining all the steps:

```javascript
// Define API request functions
function apiRequest1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve('Response from API 1'), 1000);
  });
}

function apiRequest2() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve('Response from API 2'), 1000);
  });
}

function apiRequest3() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve('Response from API 3'), 1000);
  });
}

function apiRequest4() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve('Response from API 4'), 1000);
  });
}

// Function to fetch all data
function fetchAllData() {
  return Promise.all([apiRequest1(), apiRequest2(), apiRequest3(), apiRequest4()])
    .then((responses) => {
      console.log('All API requests completed:', responses);
      showDashboard();
    })
    .catch((error) => {
      console.error('Error in API requests:', error);
      // Optionally, show an error message to the user
    });
}

// Function to show the dashboard
function showDashboard() {
  console.log('Showing the dashboard to the user');
  // Code to display the dashboard
}

// Example usage
document.getElementById('loginButton').addEventListener('click', () => {
  fetchAllData();
});
```

### **Explanation**

- **`Promise.all`**: Ensures that the dashboard is only shown when all API requests are completed. If any request fails, it will catch the error and handle it appropriately.
- **`fetchAllData` Function**: Manages the completion of all API requests and triggers the dashboard display only when all requests have been successful.
- **Error Handling**: Handles any errors that might occur during the API requests and logs them.

This approach ensures that your dashboard is only displayed once all necessary data has been fetched, providing a smoother and more reliable user experience.


## if one api failed then show partial operation using promised

If you want to handle multiple API requests and show partial operation results if any API request fails, you can achieve this using promises with a combination of `Promise.allSettled` and handling the results accordingly. Unlike `Promise.all`, which fails immediately if any promise rejects, `Promise.allSettled` waits for all promises to settle (either fulfilled or rejected) and provides an array of results.

Here’s how you can handle this scenario:

### **1. Define API Request Functions**

You’ll have functions that return promises for your API requests.

```javascript
function apiRequest1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 1') : reject('Error in API 1'), 1000);
  });
}

function apiRequest2() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 2') : reject('Error in API 2'), 1000);
  });
}

function apiRequest3() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 3') : reject('Error in API 3'), 1000);
  });
}

function apiRequest4() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 4') : reject('Error in API 4'), 1000);
  });
}
```

### **2. Handle Multiple Requests with `Promise.allSettled`**

Use `Promise.allSettled` to wait for all requests to complete, regardless of whether they succeed or fail.

```javascript
function fetchAllData() {
  return Promise.allSettled([apiRequest1(), apiRequest2(), apiRequest3(), apiRequest4()])
    .then((results) => {
      const successfulResponses = results.filter(result => result.status === 'fulfilled').map(result => result.value);
      const failedResponses = results.filter(result => result.status === 'rejected').map(result => result.reason);

      if (successfulResponses.length > 0) {
        console.log('Successful responses:', successfulResponses);
        showPartialOperation(successfulResponses);
      }

      if (failedResponses.length > 0) {
        console.error('Failed responses:', failedResponses);
        showError(failedResponses);
      }
    });
}
```

### **3. Define Functions to Show Results**

Define functions to handle the display of partial results and errors.

```javascript
function showPartialOperation(successfulResponses) {
  console.log('Showing partial results to the user:', successfulResponses);
  // Code to display partial results/dashboard
}

function showError(failedResponses) {
  console.error('Handling errors for failed requests:', failedResponses);
  // Code to display error messages to the user
}
```

### **4. Execute the Fetch and Handle UI**

Call the `fetchAllData` function as needed, such as when a user logs in.

```javascript
document.getElementById('loginButton').addEventListener('click', () => {
  fetchAllData();
});
```

### **Complete Example**

Here’s the complete code integrating all parts:

```javascript
// Define API request functions
function apiRequest1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 1') : reject('Error in API 1'), 1000);
  });
}

function apiRequest2() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 2') : reject('Error in API 2'), 1000);
  });
}

function apiRequest3() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 3') : reject('Error in API 3'), 1000);
  });
}

function apiRequest4() {
  return new Promise((resolve, reject) => {
    setTimeout(() => Math.random() > 0.5 ? resolve('Response from API 4') : reject('Error in API 4'), 1000);
  });
}

// Function to fetch all data
function fetchAllData() {
  return Promise.allSettled([apiRequest1(), apiRequest2(), apiRequest3(), apiRequest4()])
    .then((results) => {
      const successfulResponses = results.filter(result => result.status === 'fulfilled').map(result => result.value);
      const failedResponses = results.filter(result => result.status === 'rejected').map(result => result.reason);

      if (successfulResponses.length > 0) {
        console.log('Successful responses:', successfulResponses);
        showPartialOperation(successfulResponses);
      }

      if (failedResponses.length > 0) {
        console.error('Failed responses:', failedResponses);
        showError(failedResponses);
      }
    });
}

// Function to show partial operation
function showPartialOperation(successfulResponses) {
  console.log('Showing partial results to the user:', successfulResponses);
  // Code to display partial results/dashboard
}

// Function to handle errors
function showError(failedResponses) {
  console.error('Handling errors for failed requests:', failedResponses);
  // Code to display error messages to the user
}

// Example usage
document.getElementById('loginButton').addEventListener('click', () => {
  fetchAllData();
});
```

### **Explanation**

- **`Promise.allSettled`**: Waits for all the provided promises to settle, regardless of their outcomes. This means that even if some requests fail, you still receive the results of the ones that succeed.
- **Handling Results**: Separate successful and failed results to handle them appropriately.
- **UI Updates**: Show partial results and handle errors based on the results of the API requests.

This approach ensures that users can still see partial results and receive appropriate feedback if some API requests fail.