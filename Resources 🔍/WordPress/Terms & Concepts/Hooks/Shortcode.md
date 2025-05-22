Put simply, shortcodes are user-facing bits of code that give users a quick and easy way to create and display custom functionality to their sites. Shortcodes can be placed in posts and pages via the editor, in menus and widgets, and so on.

Many plugins make use of shortcodes. You can create your own shortcode by using the add_shortcode function. Here is a sample of the shortcode :

```

add_shortcode( 'myshortcode', 'myshortcode_function' );
function myshortcode_function( $atts ) {
    $atts = shortcode_atts( array(
        'text' => 'My Shortcode is Awesome!',
    ), $atts, 'myshortcode' );
 
    return $atts['text'];
}
```

To integrate your shortcode into your page you can simply add this code :

```
[myshortcode]
```