An exception is an object that is thrown when an error occurs during the execution of a script. When an exception is thrown, it can be caught and handled using `try-catch` blocks. Exceptions are particularly useful when you want to **handle errors in specific parts of your program without halting the entire script**, unlike fatal errors which stop execution.

## **Key Concepts of Exception Handling**

1. **Throwing Exceptions**:
    - You can throw exceptions using the `throw` keyword. This triggers the exception and passes it to the nearest `catch` block to handle it.
        
    - **Example**:
        ```php
        throw new Exception("Something went wrong!");
        ```
        
2. **Catching Exceptions**:
    - The `try-catch` block is used to catch exceptions. Code that may throw an exception is placed inside the `try` block, and any exceptions thrown are caught by the `catch` block.
        
    - **Example**:
        ```php
        try {
            // Code that may throw an exception
            throw new Exception("An error occurred.");
        } catch (Exception $e) {
            // Handling the exception
            echo 'Caught exception: ',  $e->getMessage(), "\n";
        }
        ```
        
3. **The `Exception` Class**:
    - PHP has a built-in `Exception` class from which all exception objects are derived. It contains several useful methods like:
        - `getMessage()`: Retrieves the message describing the exception.
        - `getCode()`: Returns the exception code (if any).
        - `getFile()`: The name of the file where the exception was thrown.
        - `getLine()`: The line number where the exception was thrown.
            
    - **Example**:
        ```php
        try {
            throw new Exception("This is a custom exception", 1);
        } catch (Exception $e) {
            echo "Message: " . $e->getMessage() . "\n";
            echo "Code: " . $e->getCode() . "\n";
            echo "File: " . $e->getFile() . "\n";
            echo "Line: " . $e->getLine() . "\n";
        }
        ```
        
4. **Multiple Catch Blocks**:
    - You can catch multiple exceptions of different types using multiple `catch` blocks. This is useful when you want to handle different exceptions differently.
        
    - **Example**:
        ```php
        try {
            // Code that may throw different exceptions
            throw new InvalidArgumentException("Invalid argument provided.");
        } catch (InvalidArgumentException $e) {
            echo "Caught an InvalidArgumentException: " . $e->getMessage();
        } catch (Exception $e) {
            echo "Caught a general exception: " . $e->getMessage();
        }
        ```
        
5. **Finally Block**:
    - The `finally` block is used to execute code regardless of whether an exception was thrown or not. It is typically used to perform cleanup operations, like closing files or database connections.
        
    - **Example**:
        ```php
        try {
            // Code that may throw an exception
            throw new Exception("An error occurred.");
        } catch (Exception $e) {
            // Handling the exception
            echo "Caught exception: " . $e->getMessage();
        } finally {
            echo "This block runs regardless of an exception.";
        }
        ```
        
## **Why Use Exceptions?**
1. **Separation of Concerns**:
    - Exceptions separate the error handling code from the normal program logic, making the code cleaner and easier to manage. By throwing exceptions in error-prone sections and catching them later, you can focus on the normal flow of the application.
2. **Graceful Error Handling**:
    - By catching exceptions, you can handle errors in a controlled manner. This prevents the application from crashing abruptly, allowing you to display a friendly message or log the error for debugging purposes.
3. **Propagation of Errors**:
    - Exceptions can be propagated across function calls. If an exception is thrown in a function, it can be caught and handled in a higher-level function. This allows errors to bubble up the call stack to the appropriate handler.
        
    - **Example**:
        ```php
        function firstFunction() {
            throw new Exception("Something went wrong in the first function.");
        }
        
        function secondFunction() {
            try {
                firstFunction(); // This throws an exception
            } catch (Exception $e) {
                echo "Caught exception in second function: " . $e->getMessage();
            }
        }
        
        secondFunction();
        ```
        
4. **Custom Exceptions**:
    - You can create your own exception classes that extend the base `Exception` class. This allows you to add custom properties and methods specific to your application's needs.
        
    - **Example**:
        ```php
        class CustomException extends Exception {
            public function errorMessage() {
                return "Error on line " . $this->getLine() . " in " . $this->getFile() . ": " . $this->getMessage();
            }
        }
        
        try {
            throw new CustomException("A custom error occurred.");
        } catch (CustomException $e) {
            echo $e->errorMessage();
        }
        ```

## Resource
- [PHP Manual - Exceptions](https://www.php.net/manual/en/language.exceptions.php)
- [W3Schools - PHP Exceptions](https://www.w3schools.com/php/php_exceptions.asp)