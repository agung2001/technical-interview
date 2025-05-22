In WordPress, an action is a specific event that occurs at a certain point in the execution of WordPress code. Actions are used to trigger functions or code blocks that perform specific tasks, such as modifying the content of a post, sending an email notification, or adding data to a database.

Actions are defined using the `add_action()` function in WordPress, which registers a callback function to be executed when the specified action occurs. The callback function can be a built-in WordPress function or a custom function defined by a plugin or theme.

For example, the `init` action is a very common WordPress action that occurs during the initialization of the WordPress environment. A plugin or theme can register a callback function to be executed when the `init` action occurs using the following code:

```php
add_action( 'init', 'my_custom_function' );
function my_custom_function(){
	// do something.
}
```

In this example, `my_custom_function` is the name of the callback function that will be executed when the `init` action occurs. The function can contain any code or task that needs to be performed at this point in the execution of WordPress.

WordPress core comes with dozens of predefined actions. However, you can also create your own. Either way, when developing your WordPress plugin, you’ll use do_action to set values for your hooked function. The **add_action** function will then be used to connect that function up to a specific action. Here are the sample code :

```
// The action callback function.
function example_callback( $arg1, $arg2 ) {
    // (maybe) do something with the args.
}
add_action( 'example_action', 'example_callback', 10, 2 );

/*
 * Trigger the actions by calling the 'example_callback()' function
 * that's hooked onto `example_action` above.
 *
 * - 'example_action' is the action hook.
 * - $arg1 and $arg2 are the additional arguments passed to the callback.
$value = do_action( 'example_action', $arg1, $arg2 );
```

