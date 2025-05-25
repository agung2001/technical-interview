<iframe width="560" height="315" src="https://www.youtube.com/embed/akDIJa0AP5c" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**SASS (Syntactically Awesome Stylesheets)** is a powerful, **CSS preprocessor** that extends the capabilities of traditional CSS. It introduces advanced features like **variables**, **nesting**, **mixins**, and **functions** to make writing and maintaining CSS easier, faster, and more maintainable, especially for large-scale web projects.

SASS is written in a syntax that is **more dynamic** than regular CSS. It compiles down to standard CSS, meaning that it can be used alongside existing CSS code. The features offered by SASS make it a popular choice for developers working on modern web applications, especially for large, complex stylesheets.

### Key Features of SASS:

1. **Variables**:
    
    - **Variables** allow you to store values (such as colors, font sizes, margins, etc.) and reuse them throughout your stylesheet. This helps avoid repetition and makes it easier to manage changes in the style of a website.
        
    
    **Example:**
    
    ```scss
    $primary-color: #3498db;
    $font-size: 16px;
    
    body {
      font-size: $font-size;
      background-color: $primary-color;
    }
    ```
    
    - In the example, `$primary-color` and `$font-size` are variables that can be reused throughout the stylesheet.
        
2. **Nesting**:
    
    - SASS allows you to **nest** CSS selectors inside one another to mirror the HTML structure. This makes it easier to read and maintain CSS, especially for complex layouts.
        
    
    **Example:**
    
    ```scss
    .nav {
      background-color: #333;
    
      ul {
        list-style: none;
      }
    
      li {
        display: inline-block;
      }
    
      a {
        color: white;
        text-decoration: none;
      }
    }
    ```
    
    - In this example, the styles are nested inside `.nav`, which makes it clear that the styles belong to the elements inside the navigation bar.
        
3. **Partials and `@import`**:
    
    - SASS allows you to break up your CSS into smaller **partials** and import them into a main stylesheet. This helps with organization and scalability.
        
    - Partials are individual SASS files that begin with an underscore (`_`), and they are meant to be imported into other SASS files.
        
    
    **Example:**
    
    ```scss
    // _variables.scss
    $primary-color: #3498db;
    
    // _base.scss
    body {
      background-color: $primary-color;
    }
    
    // main.scss
    @import 'variables';
    @import 'base';
    ```
    
    - The `@import` directive pulls in the partials and combines them into a single CSS file after compilation.
        
4. **Mixins**:
    
    - **Mixins** are reusable blocks of code that can be included in multiple places in your stylesheet. They can accept parameters to make them flexible and dynamic.
        
    
    **Example:**
    
    ```scss
    @mixin border-radius($radius) {
      -webkit-border-radius: $radius;
      -moz-border-radius: $radius;
      border-radius: $radius;
    }
    
    .box {
      @include border-radius(10px);
    }
    ```
    
    - In this example, the `border-radius` mixin is reusable and accepts a parameter (`$radius`) to set the border radius for any element.
        
5. **Inheritance** (`@extend`):
    
    - **Inheritance** allows one class to inherit styles from another. This can be useful for reducing repetition and making the code more maintainable. The `@extend` directive lets one selector inherit the styles of another.
        
    
    **Example:**
    
    ```scss
    .btn {
      padding: 10px;
      background-color: blue;
    }
    
    .btn-primary {
      @extend .btn;
      background-color: green;
    }
    
    .btn-secondary {
      @extend .btn;
      background-color: red;
    }
    ```
    
    - In this example, `.btn-primary` and `.btn-secondary` inherit the properties of `.btn` but override the background color.
        
6. **Mathematical Operations**:
    
    - SASS allows you to perform **mathematical operations** such as addition, subtraction, multiplication, and division directly in your stylesheets.
        
    
    **Example:**
    
    ```scss
    $base-size: 16px;
    $width: $base-size * 2;
    
    .container {
      width: $width;
    }
    ```
    
    - In this case, the `$width` is calculated as twice the `$base-size`, and this value is then used in the `.container` class.
        
7. **Functions**:
    
    - SASS allows you to create custom functions to perform tasks like manipulating colors or values.
        
    
    **Example:**
    
    ```scss
    @function calculate-rem($px) {
      @return $px / 16px * 1rem;
    }
    
    .container {
      font-size: calculate-rem(18px);
    }
    ```
    
    - This custom function `calculate-rem` converts pixel values into `rem` units for consistent typography scaling.
        
8. **Color Functions**:
    
    - SASS provides built-in **color functions** to manipulate colors, such as adjusting brightness or transparency, or mixing colors.
        
    
    **Example:**
    
    ```scss
    $primary-color: #3498db;
    
    .button {
      background-color: lighten($primary-color, 20%);
    }
    ```
    
    - In this example, the `lighten()` function lightens the `$primary-color` by 20%, making the button background color slightly lighter.
        

---

### How to Use SASS:

#### 1. **Installing SASS**:

- You need to install SASS on your development environment to use it. If you have **npm** (Node Package Manager) installed, you can install SASS globally with the following command:
    

```bash
npm install -g sass
```

#### 2. **Compiling SASS to CSS**:

- Once you write your SASS code, you need to compile it into regular CSS using the `sass` command. For example:
    

```bash
sass input.scss output.css
```

- You can also watch for changes in your SASS files and automatically recompile them:
    

```bash
sass --watch input.scss:output.css
```

---

### Advantages of Using SASS:

1. **Cleaner Code**:
    
    - SASS allows you to use variables, mixins, and functions to avoid redundancy in your code. This results in cleaner and more maintainable stylesheets.
        
2. **Modularization**:
    
    - By breaking your styles into partials and importing them, you can organize your CSS better and make it more manageable.
        
3. **Enhanced Features**:
    
    - With features like mixins, inheritance, and mathematical operations, SASS makes it easier to create dynamic, reusable styles.
        
4. **Faster Development**:
    
    - The use of mixins, functions, and inheritance speeds up the development process and makes changes easier to implement.
        
5. **Better Maintenance**:
    
    - With **variables** and **mixins**, you can easily make changes to your design globally, such as adjusting color schemes or spacing values, without having to manually edit every instance in your stylesheet.
        
6. **CSS Compatibility**:
    
    - SASS compiles down to regular CSS, so it works with any web framework or browser that supports CSS.
        

---

### Conclusion:

**SASS** is a highly useful **CSS preprocessor** that extends the capabilities of traditional CSS, providing developers with more advanced features such as **variables**, **mixins**, **functions**, and **nesting**. These features make it easier to manage complex stylesheets, reduce repetition, and create cleaner, more maintainable code. SASS is especially beneficial for large projects where scalability and code organization are essential. By using SASS, you can streamline your CSS workflow and enhance your development productivity.


## Resources
- [Official Website](https://sass-lang.com)
	- Youtube
		- freeCodeCamp.org 
			- [Sass Tutorial for Beginners - CSS With Superpowers](https://www.youtube.com/watch?v=_a5j7KoflTs)

## Contributors
- [[Muhammad Agung Sundoro]]