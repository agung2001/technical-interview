![](https://www.youtube.com/watch?v=H9nFFE5_VS4)

**`async` and `await`** are modern JavaScript features that provide a more readable and cleaner way to handle asynchronous operations, such as fetching data from an API, reading files, or performing time-based tasks. They make asynchronous code appear more like synchronous code, making it easier to write, read, and debug.

### Key Concepts of `async` and `await`:

1. **`async`**:
    
    - The `async` keyword is used to define a function as asynchronous. An **asynchronous function** is a function that implicitly returns a promise and allows the use of the `await` keyword inside it.
        
    - Any function marked as `async` automatically returns a promise, even if it doesn't explicitly return one.
        
    
    Example:
    
    ```javascript
    async function myFunction() {
      return 'Hello, world!';
    }
    
    myFunction().then(result => console.log(result)); // Outputs: "Hello, world!"
    ```
    
    In the example, the `async` function `myFunction` returns a promise that resolves to `'Hello, world!'`.
    
2. **`await`**:
    
    - The `await` keyword can only be used inside an `async` function. It pauses the execution of the `async` function until the Promise it is awaiting resolves or rejects.
        
    - `await` makes JavaScript wait for the promise to resolve and then returns the result. If the promise is rejected, `await` throws an error.
        
    
    Example:
    
    ```javascript
    async function fetchData() {
      const data = await fetch('https://api.example.com/data');
      const json = await data.json();
      return json;
    }
    
    fetchData().then(result => console.log(result)); // Outputs fetched data
    ```
    
    In the example, the `await` keyword pauses the function until the `fetch()` promise resolves and then waits for the `.json()` method to extract the JSON data from the response.
    

### How `async` and `await` Work:

- When an `async` function is called, it always returns a **promise**, which resolves to the function's return value. Even if you don't explicitly return a promise, the `async` function will wrap the return value in a resolved promise.
    
- Inside an `async` function, you can use `await` to wait for a promise to resolve. When `await` is used, it pauses the execution of the function until the promise is resolved, and then it returns the resolved value.
    

### Example with `async` and `await`:

Let's say you need to fetch data from an API. Traditionally, this is done using **callbacks** or **promises**, but with `async` and `await`, it becomes simpler and easier to understand.

```javascript
// Example of asynchronous code using async and await
async function getUserData(userId) {
  try {
    const response = await fetch(`https://api.example.com/user/${userId}`);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching user data:', error);
  }
}

// Usage
getUserData(1).then(data => console.log(data));
```

#### Explanation:

1. `getUserData` is an `async` function that fetches user data from the API.
    
2. `await` pauses the execution of `getUserData` until the `fetch()` promise resolves.
    
3. After the response is received, `await` is used again to resolve the `.json()` method and extract the JSON data.
    
4. If there’s an error during the process, it’s caught by the `try...catch` block.
    

### Error Handling with `async` and `await`:

When working with promises, errors can occur, so it’s important to handle them. The `try...catch` statement is used to catch any errors in an `async` function.

```javascript
async function getUserData(userId) {
  try {
    const response = await fetch(`https://api.example.com/user/${userId}`);
    if (!response.ok) { // Check if the response was successful
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching user data:', error);
  }
}
```

#### Explanation:

- `try...catch` allows you to handle any errors that may occur in the `async` function.
    
- If the `fetch()` call fails or the response is not okay, the error is thrown and caught in the `catch` block.
    

### Benefits of `async` and `await`:

1. **Readable and Synchronous-Like Code**:
    
    - `async` and `await` make asynchronous code look and behave more like **synchronous code**, making it easier to read, understand, and debug.
        
    - Without `async` and `await`, you'd need to chain `.then()` and `.catch()` for promises, which can lead to callback hell or cumbersome promise chains.
        
2. **Avoid Callback Hell**:
    
    - Traditional asynchronous code using callbacks can get complex and nested, resulting in **callback hell** (or **pyramid of doom**), where the callbacks are deeply nested, making the code difficult to maintain. `async` and `await` make the code cleaner by flattening out the structure.
        
    
    Example of callback hell:
    
    ```javascript
    someAsyncFunction(function(err, result) {
      if (err) {
        console.log(err);
      } else {
        anotherAsyncFunction(result, function(err, anotherResult) {
          if (err) {
            console.log(err);
          } else {
            // Continue chaining...
          }
        });
      }
    });
    ```
    
    Using `async` and `await`, the same logic can be written as:
    
    ```javascript
    try {
      const result = await someAsyncFunction();
      const anotherResult = await anotherAsyncFunction(result);
    } catch (err) {
      console.error(err);
    }
    ```
    
3. **Error Handling is Simpler**:
    
    - With traditional promises, you need to chain `.catch()` for error handling. With `async` and `await`, you can use `try...catch`, which is more familiar to developers and easier to handle, especially in complex scenarios.
        
4. **Cleaner Syntax**:
    
    - `async` and `await` provide a cleaner syntax for handling asynchronous operations without requiring chaining, callbacks, or promise constructors, reducing the complexity of your code.
        

### Example: Multiple Asynchronous Calls with `async` and `await`:

If you need to perform multiple asynchronous operations that depend on each other, you can use `async` and `await` to handle them sequentially or in parallel.

#### Sequential Execution:

```javascript
async function getData() {
  const data1 = await fetch('https://api.example.com/data1');
  const data2 = await fetch('https://api.example.com/data2');
  return { data1, data2 };
}
```

In this example, `data2` is fetched **only after** `data1` is successfully fetched, making the requests sequential.

#### Parallel Execution:

You can run multiple asynchronous tasks in parallel using `Promise.all` to improve performance.

```javascript
async function getData() {
  const [data1, data2] = await Promise.all([
    fetch('https://api.example.com/data1'),
    fetch('https://api.example.com/data2')
  ]);
  return { data1, data2 };
}
```

In this example, both `data1` and `data2` are fetched **in parallel**, speeding up the process compared to sequential execution.

### Conclusion:

**`async` and `await`** provide a modern, clean, and more readable way to work with asynchronous code in JavaScript. They allow asynchronous code to be written in a **synchronous style**, eliminating the need for deeply nested callback functions or promise chaining. By using `async` functions and the `await` keyword, you can handle asynchronous operations more naturally and reduce the complexity of your code, while still maintaining robust error handling through `try...catch`.