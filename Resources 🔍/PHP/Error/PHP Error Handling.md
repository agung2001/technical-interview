**PHP Error Handling** refers to the way PHP manages and handles errors that occur during the execution of a script. Proper error handling allows developers to identify, manage, and fix issues in the code more efficiently, improving the overall user experience and maintaining the stability of the application.

Here’s an overview of how PHP error handling works:

## **Types of PHP Errors**
PHP errors are categorized into several types, each indicating different issues that may arise:
- **Parse Errors**: These occur when there’s a syntax error in the PHP code, such as missing semicolons or unmatched parentheses.
- **Fatal Errors**: These are critical errors that halt script execution. They may occur due to problems like calling a non-existent function or class.
- **Warning Errors**: These are non-fatal errors, meaning the script will continue running. An example is including a file that doesn’t exist.
- **Notice Errors**: These are minor errors or alerts, such as trying to use an undefined variable. The script will still continue running.
- **Deprecated Errors**: These occur when using a feature or function that is no longer supported in the current version of PHP.

## **Error Reporting**
PHP provides several constants to specify the types of errors you want to report. You can configure the error reporting level using the `error_reporting()` function or the `php.ini` settings. These constants define different levels of errors that can be reported.

```php
// Report all errors except notices
error_reporting(E_ALL & ~E_NOTICE);

// Report all errors including notices
error_reporting(E_ALL);

// Report only critical errors
error_reporting(E_ERROR | E_WARNING);
```

### Common Error Report Levels

| Error Level         | Description                                     | Example Scenario                   | Severity |
| ------------------- | ----------------------------------------------- | ---------------------------------- | -------- |
| `E_ERROR`           | Fatal run-time errors                           | Call to undefined function         | High     |
| `E_WARNING`         | Non-fatal run-time warnings                     | Missing file include               | Medium   |
| `E_PARSE`           | Compile-time parse errors                       | Missing parentheses                | High     |
| `E_NOTICE`          | Run-time notices                                | Undefined variable                 | Low      |
| `E_DEPRECATED`      | Notices about deprecated features               | Deprecated MySQL functions         | Low      |
| `E_USER_ERROR`      | User-generated fatal error                      | Triggering a custom error          | High     |
| `E_USER_WARNING`    | User-generated warning                          | Triggering a custom warning        | Medium   |
| `E_USER_NOTICE`     | User-generated notice                           | Triggering a custom notice         | Low      |
| `E_ALL`             | All errors, warnings, notices, and deprecations | Reports all types of errors        | High     |

Read more about PHP error level here : https://www.php.net/manual/en/errorfunc.constants.php

Here’s a breakdown of the available error report levels:

### **E_ERROR (Fatal run-time errors)**
- **Description**: These errors are critical and cause the script to halt immediately. For example, calling a function that doesn’t exist or requiring a file that cannot be found.
    
- **Example**:
    ```php
    echo $undefined_variable; // Will cause an E_NOTICE error
    ```
    
- **Severity**: High (script stops executing).
    
### **E_WARNING (Run-time warnings)**
- **Description**: These are non-fatal errors that allow the script to continue running. They are used for warnings such as calling a non-existent function or including a file that doesn’t exist.
    
- **Example**:
    ```php
    include("nonexistent_file.php"); // Will cause an E_WARNING error
    ```
    
- **Severity**: Medium (script continues executing but with warnings).
    
### **E_PARSE (Compile-time parse errors)**
- **Description**: These errors occur during the compilation phase (before the script is executed). They are caused by syntax errors such as missing parentheses, semicolons, or incorrect PHP tags.
    
- **Example**:
    ```php
    echo "Hello World; // Missing closing quote
    ```
    
- **Severity**: High (compilation stops, the script will not run).
    
### **E_NOTICE (Run-time notices)**
- **Description**: These are minor errors or notices indicating that something might be wrong in the code, like accessing an undefined variable or array element.
    
- **Example**:
    ```php
    echo $undefined_variable; // Will cause an E_NOTICE error
    ```
    
- **Severity**: Low (script continues, but provides a notice).

### **E_DEPRECATED (Run-time notices about deprecated features)**
- **Description**: These errors indicate that a feature or function used in the script is deprecated and may be removed in future versions of PHP. This helps developers stay updated on deprecated features.
    
- **Example**:
    ```php
    mysql_connect('localhost', 'user', 'password'); // Deprecated in PHP 5.5.0
    ```
    
- **Severity**: Low (encourages updating code for future compatibility).

### **E_USER_ERROR (User-generated error)**
- **Description**: This type of error is triggered by the `trigger_error()` function within the script. It behaves like an `E_ERROR`, meaning the script halts on encountering this error.
    
- **Example**:
    ```php
    trigger_error("Custom error message", E_USER_ERROR); // Triggers an E_USER_ERROR
    ```
    
- **Severity**: High (similar to `E_ERROR`).
    
### **E_USER_WARNING (User-generated warning)**
- **Description**: This error is triggered by the `trigger_error()` function and behaves like an `E_WARNING`. It allows the script to continue running after the warning is triggered.
    
- **Example**:
    ```php
    trigger_error("This is a custom warning", E_USER_WARNING); // Triggers an E_USER_WARNING
    ```
    
- **Severity**: Medium (script continues, but with a warning).

### **E_USER_NOTICE (User-generated notice)**
- **Description**: Similar to `E_USER_WARNING`, but less severe. It is triggered by `trigger_error()` and is used to generate a custom notice.
    
- **Example**:
    ```php
    trigger_error("This is a custom notice", E_USER_NOTICE); // Triggers an E_USER_NOTICE
    ```
    
- **Severity**: Low (script continues, but with a custom notice).


## **Displaying Errors**
The `ini_set()` function in PHP allows developers to control whether errors will be displayed or hidden in the output. This is useful for production environments where exposing detailed error messages could lead to security issues.

- **Example**:
    ```php
    ini_set('display_errors', 1); // Show errors on screen
    ini_set('display_errors', 0); // Hide errors from screen
    ```

## **Logging Errors**
PHP also allows errors to be logged to a file for future reference and debugging. The `log_errors` directive can be used to enable or disable error logging.

- **Example**:
    ```php
    ini_set('log_errors', 1); // Enable error logging
    ini_set('error_log', '/path/to/error_log.txt'); // Specify the log file
    ```

## **Custom Error Handling**
Developers can create custom error handlers using the `set_error_handler()` function. This allows you to specify a custom function that will handle specific types of errors.

- **Example**:
    ```php
    function customError($errno, $errstr, $errfile, $errline) {
        echo "Error [$errno]: $errstr in $errfile on line $errline";
    }
    
    set_error_handler("customError");
    ```

## **Exception Handling**
PHP 5 introduced the concept of exceptions, which are more powerful than traditional error handling. You can use `try`, `catch`, and `throw` blocks to catch and handle exceptions.

- **Example**:
    ```php
    try {
        $file = fopen("testfile.txt", "r");
        if (!$file) {
            throw new Exception("File not found!");
        }
    } catch (Exception $e) {
        echo 'Caught exception: ',  $e->getMessage(), "\n";
    }
    ```

## **Error Handling in Production**
In production environments, it's best practice to disable error displaying (`display_errors`) and log errors to a file for debugging purposes. This ensures that sensitive information is not exposed to users while still capturing errors for developers.

- **Example**:
    ```php
    ini_set('display_errors', 0);  // Hide errors in production
    ini_set('log_errors', 1);      // Log errors to a file
    ini_set('error_log', '/var/log/php_errors.log'); // Path to error log
    ```

## Resource
- [W3Schools - PHP Error](https://www.w3schools.com/php/php_ref_error.asp)
- [W3Schools - PHP Error Handling](https://www.w3schools.com/php/php_error.asp)