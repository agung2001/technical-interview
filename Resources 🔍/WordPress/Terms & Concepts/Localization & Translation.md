In WordPress, `__()`, `_e()`, and `_x()` are **translation functions** used to handle **localization** (translation of content into different languages) and **internationalization** (making your website ready for translation). These functions allow you to prepare your WordPress themes and plugins for translation, enabling non-English speakers to use your site in their preferred language.

Let's dive into each function and understand their purpose and usage:

### **1. `__()` - Translation Function (Returns Translated String)**
The `__()` function is used to **retrieve a translated string** from the WordPress language files (`.mo` and `.po`). It allows you to get a string in a specific language based on the current site language set in the WordPress settings.

#### **Syntax**:
```php
__($text, $domain);
```

- **$text**: The string to be translated.
- **$domain**: The text domain, which helps WordPress identify which translation files to use (usually your theme or plugin’s name).

#### **Example Usage**:
```php
// English string
$translated_string = __('Hello, World!', 'my-theme');

// Output the translated string
echo $translated_string;
```

In this example:
- `__('Hello, World!', 'my-theme')` will return the translated string for "Hello, World!" based on the current language set on the site (e.g., if the site is set to French, it will return the French translation of "Hello, World!").
- `'my-theme'` is the **text domain**, which links the string to your theme or plugin’s translation files.

### **2. `_e()` - Translation Function (Echoes Translated String)**

The `_e()` function is very similar to `__()`, but instead of returning the translated string, it directly **echoes the translated string** to the page. This function is useful when you want to print the translated string directly within the HTML output.

#### **Syntax**:
```php
_e($text, $domain);
```

- **$text**: The string to be translated and printed.
- **$domain**: The text domain for your theme or plugin.

#### **Example Usage**:

```php
// English string
_e('Hello, World!', 'my-theme');
```

In this example:
- `_e('Hello, World!', 'my-theme')` will directly echo the translated string for "Hello, World!" based on the current language.
- It eliminates the need to assign the translated string to a variable and then echo it manually.

### **3. `_x()` - Translation Function (With Context)**

The `_x()` function is similar to `__()` but allows you to provide **context** for the translation. Context is useful when the same string might have different meanings depending on where or how it’s used. For example, the word "close" can mean "to shut" or "nearby," and providing context helps translators understand how to translate the word appropriately.

#### **Syntax**:

```php
_x($text, $context, $domain);
```

- **$text**: The string to be translated.
- **$context**: A short description of the context in which the string is used.
- **$domain**: The text domain, like in `__()` and `_e()`.

#### **Example Usage**:

```php
// For the context "close" as in "nearby"
$translated_string = _x('Close', 'close to something', 'my-theme');

// Output the translated string
echo $translated_string;
```

In this example:
- `_x('Close', 'close to something', 'my-theme')` helps translators understand that "Close" in this context means "nearby," rather than the action "to close something."
- The **context** (`'close to something'`) is passed as a second argument to clarify how the string is used.

Context is particularly helpful for languages that may have multiple translations for the same word based on context.

### **Summary of Differences**

|Function|Purpose|
|---|---|
|**`__()`**|Retrieves a translated string. Returns the translation based on the current language.|
|**`_e()`**|Echoes (prints) the translated string. Useful when you want to directly display the translation.|
|**`_x()`**|Retrieves a translated string with **context**. Used when the same string has different meanings in different contexts.|

### **Best Practices for Using Translation Functions**

1. **Always use `__()`, `_e()`, and `_x()`** for any user-facing text in your theme or plugin. This ensures that your content is translatable, making it accessible for non-English speakers.
2. **Set the text domain**: Make sure you specify the correct **text domain** for your theme or plugin, so WordPress knows where to find the translation files (`.po` and `.mo` files).
3. **Provide context with `_x()`**: When using strings that have different meanings based on context, use `_x()` to provide context for translators. This improves translation accuracy.
4. **Use `__()` and `_e()` for consistency**: `__()` is useful when you need to use the string programmatically, and `_e()` is ideal when you want to output the string directly.

### **Example Use Case in a Theme or Plugin**
Let’s say you have a theme that displays a button that says “Click Here.” Here’s how you can make it translatable:

#### **1. Define the String Using `__()` or `_e()`**:

```php
// Using __() to retrieve the string
$button_text = __('Click Here', 'my-theme');

// Or using _e() to directly echo the string
_e('Click Here', 'my-theme');
```

#### **2. Add the Context Using `_x()`**:

If "Click Here" can have different meanings in your theme (like for a button or a link), use `_x()` for clarity:

```php
// Providing context for the string
$button_text = _x('Click Here', 'Button text', 'my-theme');

// Or echoing directly with _e()
_e('Click Here', 'my-theme');
```

#### **3. Ensure Translation Files Exist**

- Ensure you have translation files (`.po` and `.mo`) in your theme’s `/languages/` folder. These files should contain the appropriate translations for the strings used in your theme.

Example:
- **English (`en_US.po`)**:  
    `msgid "Click Here" msgstr "Click Here"`
- **French (`fr_FR.po`)**:  
    `msgid "Click Here" msgstr "Cliquez ici"`

## Resource
- [WordPress Developer - Localization](https://developer.wordpress.org/apis/internationalization/localization/)