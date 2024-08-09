
## How to test a function a() having dependency to other b() and  function c()
Testing a function that has dependencies on other functions can be approached in several ways, depending on the nature of the dependencies and the testing strategy you want to use. Here are some common strategies:

### 1. **Unit Testing with Mocking**

In unit testing, you test the function in isolation by replacing its dependencies with mock versions. This allows you to focus on the function you're testing without worrying about the actual implementations of its dependencies.

**Example Scenario:**

Assume you have a function `calculateTotal` that depends on two functions, `getDiscount` and `getTax`.

```javascript
function calculateTotal(price) {
  const discount = getDiscount(price);
  const tax = getTax(price);
  return price - discount + tax;
}
```

Here's how you could test `calculateTotal` using a testing framework like Jest and mocking `getDiscount` and `getTax`:

**1.1. Install Jest:**

If you haven't installed Jest, you can do so using npm:

```bash
npm install --save-dev jest
```

**1.2. Write the Test:**

Create a test file, e.g., `calculateTotal.test.js`:

```javascript
// calculateTotal.js
const { getDiscount, getTax } = require('./dependencies');

function calculateTotal(price) {
  const discount = getDiscount(price);
  const tax = getTax(price);
  return price - discount + tax;
}

module.exports = calculateTotal;

// calculateTotal.test.js
const calculateTotal = require('./calculateTotal');
const { getDiscount, getTax } = require('./dependencies');

jest.mock('./dependencies');

describe('calculateTotal', () => {
  it('should correctly calculate the total', () => {
    // Arrange
    const price = 100;
    getDiscount.mockReturnValue(10); // Mock discount to always return 10
    getTax.mockReturnValue(15);      // Mock tax to always return 15

    // Act
    const total = calculateTotal(price);

    // Assert
    expect(total).toBe(105); // 100 - 10 + 15
  });
});
```

### 2. **Integration Testing**

Integration tests check how different pieces of code work together. For testing functions with dependencies without mocking, you would test the whole system or a subset of it to ensure that it works correctly when all parts are in place.

**Example Scenario:**

If `getDiscount` and `getTax` are simple functions and you want to test `calculateTotal` with their real implementations:

```javascript
// dependencies.js
function getDiscount(price) {
  return price * 0.1; // 10% discount
}

function getTax(price) {
  return price * 0.2; // 20% tax
}

module.exports = { getDiscount, getTax };

// calculateTotal.test.js
const calculateTotal = require('./calculateTotal');
const { getDiscount, getTax } = require('./dependencies');

describe('calculateTotal with real dependencies', () => {
  it('should correctly calculate the total', () => {
    // Arrange
    const price = 100;

    // Act
    const total = calculateTotal(price);

    // Assert
    expect(total).toBe(110); // 100 - (100 * 0.1) + (100 * 0.2)
  });
});
```

### 3. **Dependency Injection**

Another approach is to refactor the function to accept its dependencies as parameters. This makes it easier to inject mock implementations for testing.

**Refactored Function:**

```javascript
function calculateTotal(price, getDiscount, getTax) {
  const discount = getDiscount(price);
  const tax = getTax(price);
  return price - discount + tax;
}
```

**Test with Dependency Injection:**

```javascript
const calculateTotal = require('./calculateTotal');

describe('calculateTotal with injected dependencies', () => {
  it('should correctly calculate the total', () => {
    // Arrange
    const price = 100;
    const mockGetDiscount = jest.fn().mockReturnValue(10);
    const mockGetTax = jest.fn().mockReturnValue(15);

    // Act
    const total = calculateTotal(price, mockGetDiscount, mockGetTax);

    // Assert
    expect(total).toBe(105); // 100 - 10 + 15
  });
});
```

### Summary

- **Unit Testing with Mocking:** Replace dependencies with mocks to test the function in isolation.
- **Integration Testing:** Test the function with its real dependencies to ensure the whole system works correctly.
- **Dependency Injection:** Refactor the function to accept dependencies as parameters, making it easier to test.

Choosing the right approach depends on your testing goals and the complexity of your code.



### Note - This question was asked into HCL interview of 1st Level
