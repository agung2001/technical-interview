**Axios** is a popular **JavaScript library** used to make **HTTP requests** from a web browser or a Node.js environment. It provides a simple and easy-to-use API for sending HTTP requests, handling responses, and working with promises in JavaScript. Axios supports features like **Promise-based handling**, **request cancellation**, and **interceptors**.

### Key Features of Axios:

1. **Promise-Based**:
    
    - Axios uses **Promises** for handling asynchronous HTTP requests. This makes it easier to handle success and error responses using `.then()` and `.catch()` or with **`async/await`**.
        
2. **Supports HTTP Methods**:
    
    - Axios supports all HTTP methods, including **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, etc.
        
3. **Browser and Node.js Support**:
    
    - Axios can be used in both **browser-based** environments (such as web apps) and **server-side environments** (Node.js). It works on all modern browsers and can be integrated into front-end frameworks like **React**, **Vue**, or **Angular**.
        
4. **Request and Response Interceptors**:
    
    - Axios allows you to define **interceptors**, which enable you to modify the request or the response before they are sent or received. This is useful for tasks like adding authentication tokens or handling errors globally.
        
5. **Automatic JSON Data Transformation**:
    
    - Axios automatically transforms the response data into JSON format, making it easy to work with data from REST APIs. You can also configure it to handle other response types like `blob` or `text`.
        
6. **Canceling Requests**:
    
    - Axios supports **canceling requests** by using a `CancelToken`, allowing you to cancel requests that are no longer needed (e.g., when a user navigates away from a page).
        
7. **Configurable**:
    
    - Axios is highly configurable and provides options like **base URLs**, **headers**, **timeout settings**, and more.
        

---

### Installing Axios:

To use Axios in a project, you need to install it first.

If you are using **npm**, you can install it with:

```bash
npm install axios
```

Or, if you are using **yarn**:

```bash
yarn add axios
```

Alternatively, you can include Axios via a CDN in your HTML file:

```html
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
```

---

### Basic Usage of Axios:

#### 1. **GET Request**:

To fetch data from a server, you use the `axios.get()` method. This is typically used for **retrieving** data from a REST API.

```javascript
// Example: GET request to fetch data
axios.get('https://api.example.com/data')
  .then(response => {
    console.log(response.data); // The data returned from the server
  })
  .catch(error => {
    console.error('There was an error!', error);
  });
```

- **`get()`**: Sends an HTTP GET request to the specified URL.
    
- **`response.data`**: The data received in the response from the server.
    

#### 2. **POST Request**:

For sending data to the server (e.g., creating a new resource), you use the `axios.post()` method.

```javascript
// Example: POST request to send data
const user = {
  name: 'Alice',
  email: 'alice@example.com'
};

axios.post('https://api.example.com/users', user)
  .then(response => {
    console.log('User created:', response.data);
  })
  .catch(error => {
    console.error('There was an error!', error);
  });
```

- **`post()`**: Sends an HTTP POST request with the data you want to send (e.g., form data or JSON data).
    

#### 3. **PUT and DELETE Requests**:

You can use `axios.put()` to update data and `axios.delete()` to delete data.

```javascript
// Example: PUT request to update data
const updatedUser = {
  name: 'Alice Updated',
  email: 'alice_updated@example.com'
};

axios.put('https://api.example.com/users/1', updatedUser)
  .then(response => {
    console.log('User updated:', response.data);
  })
  .catch(error => {
    console.error('Error updating user:', error);
  });

// Example: DELETE request to delete data
axios.delete('https://api.example.com/users/1')
  .then(response => {
    console.log('User deleted:', response.data);
  })
  .catch(error => {
    console.error('Error deleting user:', error);
  });
```

---

### Handling HTTP Responses:

When Axios makes an HTTP request, the response is usually returned as a `Promise`. The response object contains useful information like:

- **`data`**: The response body data (usually the server's response data).
    
- **`status`**: The HTTP status code.
    
- **`statusText`**: The status text corresponding to the HTTP status code (e.g., "OK").
    
- **`headers`**: The response headers.
    
- **`config`**: The configuration object used for the request.
    

```javascript
axios.get('https://api.example.com/data')
  .then(response => {
    console.log('Status:', response.status);      // e.g., 200
    console.log('Response Data:', response.data);  // The data sent back by the server
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

---

### Using `async/await` with Axios:

Since Axios returns **Promises**, you can use the `async/await` syntax to handle asynchronous code in a more synchronous-like manner.

```javascript
async function fetchData() {
  try {
    const response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchData();
```

- **`async`**: Declares the function as asynchronous.
    
- **`await`**: Waits for the Promise to resolve and returns the result, making asynchronous code easier to read.
    

---

### Interceptors:

Axios allows you to define **interceptors**, which are functions that run before a request is sent or after a response is received. This can be useful for tasks like adding authorization tokens, logging requests, or modifying responses.

#### Example of a Request Interceptor:

```javascript
axios.interceptors.request.use(request => {
  // Modify request before sending (e.g., add an Authorization header)
  request.headers['Authorization'] = 'Bearer YOUR_TOKEN';
  return request;
}, error => {
  return Promise.reject(error);
});
```

#### Example of a Response Interceptor:

```javascript
axios.interceptors.response.use(response => {
  // Modify response before returning it
  console.log('Response:', response.data);
  return response;
}, error => {
  return Promise.reject(error);
});
```

- **Request Interceptor**: Allows you to modify the request before it is sent, such as adding authentication headers.
    
- **Response Interceptor**: Allows you to modify the response data, handle errors globally, or log the data.
    

---

### Request Cancellation:

Axios provides the ability to cancel requests using **`CancelToken`**, which can be useful for situations like **debouncing** or **cancelling outdated requests** (e.g., when a user navigates away before an API call finishes).

```javascript
const source = axios.CancelToken.source();

axios.get('https://api.example.com/data', {
  cancelToken: source.token
})
  .then(response => console.log(response.data))
  .catch(error => {
    if (axios.isCancel(error)) {
      console.log('Request canceled', error.message);
    } else {
      console.log('Error:', error);
    }
  });

// Cancel the request
source.cancel('Request was canceled');
```

- **CancelToken**: Allows you to cancel the request. You can pass the token to the request configuration and call `source.cancel()` when you want to abort the request.
    

---

### Conclusion:

**Axios** is a powerful and flexible library for making **HTTP requests** in JavaScript. It simplifies working with **Promises**, provides useful features like **request/response interceptors**, **cancellation**, and **automatic JSON parsing**, and works well in both **browser** and **Node.js** environments. Axios is highly favored by developers due to its **ease of use**, **advanced features**, and **better handling of HTTP requests** compared to the native `fetch()` API in JavaScript.

## Resource
- [Official Website](https://axios-http.com/)
- [Github Axios](https://github.com/axios/axios)
- [Documentation](https://axios-http.com/docs/intro)
