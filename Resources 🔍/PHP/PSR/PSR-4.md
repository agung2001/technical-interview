PSR-4 (PHP Standard Recommendation 4) is a coding standard defined by the PHP Framework Interop Group (PHP-FIG). It specifies the autoloading of PHP classes based on the file namespace and directory structure.

PSR-4 provides a standard way to organize and autoload PHP classes in a project, making it easier for developers to manage and load classes automatically without the need for manual includes or requires.

The main principles of PSR-4 are as follows:
1. Namespace and Class Mapping: PSR-4 defines a mapping between the namespace of a class and its file path. Each namespace segment corresponds to a directory in the file system.
2. PSR-4 Autoloading: Autoloading is achieved using the `spl_autoload_register` function in PHP. When a class is not found, the autoloader registered according to PSR-4 is triggered, and it automatically loads the corresponding class file based on the namespace-to-directory mapping.

Here's an example of how a PSR-4-compliant autoloader might look:
```php
spl_autoload_register(function ($class) {
    // Namespace prefix
    $prefix = 'MyApp\\';

    // Base directory for the namespace
    $baseDir = __DIR__ . '/src/';

    // Does the class use the namespace prefix?
    $len = strlen($prefix);
    if (strncmp($prefix, $class, $len) !== 0) {
        // Not part of the namespace, move to the next registered autoloader
        return;
    }

    // Get the relative class name
    $relativeClass = substr($class, $len);

    // Replace namespace separator with directory separator and load the class file
    $file = $baseDir . str_replace('\\', '/', $relativeClass) . '.php';

    if (file_exists($file)) {
        require $file;
    }
});
```

By adhering to the PSR-4 standard, PHP projects can be more organized, maintainable, and interoperable, as developers can easily include third-party libraries and components that follow the same autoloading convention.

## Resource
- [Official Docs - PSR-4](https://www.php-fig.org/psr/psr-4/)