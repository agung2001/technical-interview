In PHP, a trait is a language construct that allows you to reuse sets of methods in multiple classes. Traits are similar to classes, but they cannot be instantiated on their own. Instead, they are designed to be included in classes using the `use` keyword.

Traits are useful for sharing common functionality across multiple classes without the need for multiple inheritance, which PHP does not support. When a class uses a trait, it gains access to all the methods defined in that trait as if those methods were defined directly in the class itself.

Here's a simple example of a trait:
```php
trait Greet {
    public function sayHello() {
        echo 'Hello! ';
    }

    public function sayGoodbye() {
        echo 'Goodbye! ';
    }
}
```

Now, we can use the `Greet` trait in multiple classes:
```php
class Person {
    use Greet;

    public function introduce() {
        echo 'My name is John. ';
    }
}

class Animal {
    use Greet;

    public function sound() {
        echo 'Woof! ';
    }
}

```

In this example, both the `Person` and `Animal` classes use the `Greet` trait. As a result, they both have access to the `sayHello()` and `sayGoodbye()` methods defined in the trait. This allows us to share the common greeting functionality among different classes without having to duplicate the code.

Using traits can help to keep your code organized, promote code reusability, and reduce code duplication in PHP projects. However, it's important to use traits judiciously, as overusing them can lead to complex class hierarchies and make code harder to maintain.