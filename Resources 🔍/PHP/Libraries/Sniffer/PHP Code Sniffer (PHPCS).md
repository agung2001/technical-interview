PHPCS stands for PHP CodeSniffer. It is a tool used to detect violations of coding standards in PHP code. It helps ensure that your PHP code follows consistent coding standards, making it easier to read, maintain, and collaborate with other developers.

PHP CodeSniffer analyzes PHP code based on a set of rules defined in coding standards like PSR-1, PSR-2, WordPress Coding Standards, and others. It scans the code and generates reports that highlight coding standard violations, such as incorrect indentation, improper spacing, missing docblocks, and more.

Using PHPCS in your development workflow can help maintain a high level of code quality and ensure that your codebase adheres to best practices and industry standards. It can be integrated into various development environments and build tools to automatically check your code as part of your development process.

## Commands
- Sniff `phpcs --standard=phpcs.xml --extensions=php src`  

## Integration with PHPStorm
- [PHPStorm - PHP CodeSniffer](https://www.jetbrains.com/help/phpstorm/using-php-code-sniffer.html)
- [Using PHPCBF in PHPSTORM using External Tools](https://www.youtube.com/watch?v=pkmT2QQPZiM)

When you do integration with PHPStorm you might want to enable this option : 
- `Show sniff name` : this will allows you to see specific rule applied to code so then if you want to do `phpcs:ignore` you can ignore that specific rule only.
## Resource
- [GitHub - squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)

## Contributors
- [[Muhammad Agung Sundoro]]: 2024-10-15