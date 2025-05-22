![](https://photos.artistudio.xyz/uploads/original/c6/84/847e92fab3b9338fe56a34bb04ee.png)

PHP (Hypertext Preprocessor) is a widely-used open-source server-side scripting language primarily designed for web development. It was created by Rasmus Lerdorf in 1994 and is now maintained by the PHP development team.

Key features and characteristics of PHP include:
1. **Server-Side Scripting:** PHP is executed on the server-side, meaning that the PHP code is processed on the web server before sending the HTML output to the client's browser.
2. **Embedded Code:** PHP code can be embedded directly within HTML documents, allowing developers to mix PHP and HTML seamlessly.
3. **Open Source:** PHP is an open-source language, which means it is free to use, modify, and distribute.
4. **Cross-Platform:** PHP is platform-independent and can run on various operating systems, including Windows, macOS, Linux, and others.
5. **Extensive Community and Library Support:** PHP has a large and active community, offering a wide range of libraries, frameworks, and plugins that developers can use to speed up development and extend functionality.
6. **Database Connectivity:** PHP provides built-in support for interacting with various databases, making it easy to connect and work with databases like MySQL, PostgreSQL, SQLite, etc.
7. **Object-Oriented Programming (OOP):** PHP supports object-oriented programming, allowing developers to create reusable code and organize their applications more efficiently.
8. **Fast and Efficient:** PHP is designed to be fast and efficient, making it suitable for handling web traffic and processing dynamic web pages.
9. **Wide Adoption:** PHP is one of the most popular programming languages for web development and is used by many large websites and applications.
10. **Versatility:** PHP can handle various tasks, including form processing, file handling, session management, authentication, and more.

PHP is commonly used for creating dynamic and interactive web applications, content management systems (e.g., WordPress), e-commerce platforms, and web services. It is known for its ease of use, rapid development capabilities, and wide community support, making it a preferred choice for web developers worldwide.

## Interfaces vs Abstract Class
Interface are similar to abstract classes. The difference between interfaces and abstract classes are:

- Interfaces cannot have properties, while abstract classes can
- All interface methods must be public, while abstract class methods is public or protected
- All methods in an interface are abstract, so they cannot be implemented in code and the abstract keyword is not necessary
- Classes can implement an interface while inheriting from another class at the same time

## Library
- [[PHP Code Sniffer (PHPCS)]]
	- [[WordPress Coding Standard (WPCS)]]

## Unit Test
Installation `composer require --dev phpunit/phpunit`

Sample Unit Test
```php
<?php
use PHPUnit\Framework\TestCase;

class MathTest extends TestCase
{
    public function testAdd()
    {
        $result = add(1, 2);
        $this->assertEquals(3, $result);
    }
}
```

Run code by : `phpunit MathTest.php`

## Resource
-   [Official Website](https://www.php.net/)
-   [Other References](https://www.w3schools.com/php/)
