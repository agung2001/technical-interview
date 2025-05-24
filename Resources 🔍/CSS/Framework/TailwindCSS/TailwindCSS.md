<iframe width="560" height="315" src="https://www.youtube.com/embed/mr15Xzb1Ook" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

**Tailwind CSS** is a **utility-first CSS framework** that provides a set of low-level, atomic CSS classes that you can combine to create custom designs directly in your HTML markup. Unlike traditional CSS frameworks like Bootstrap or Foundation, which offer pre-styled components (buttons, cards, modals, etc.), **Tailwind CSS** focuses on providing **utility classes** to control the layout, spacing, colors, typography, and other aspects of design, giving developers complete control over their design without needing to write custom CSS for each component.

### Key Features of Tailwind CSS:

1. **Utility-First**:
    
    - Tailwind uses **utility-first** classes that are single-purpose and describe specific design properties, such as margin, padding, font size, colors, borders, etc.
        
    - You apply these utility classes directly in your HTML elements to style them, rather than writing custom CSS rules or relying on pre-designed components.
        
    
    **Example:**
    
    ```html
    <div class="bg-blue-500 text-white p-4 rounded-lg">
      This is a styled box.
    </div>
    ```
    
    - In this example, the div element has multiple utility classes applied:
        
        - `bg-blue-500`: Set the background color to a shade of blue.
            
        - `text-white`: Set the text color to white.
            
        - `p-4`: Apply padding to all sides of the element.
            
        - `rounded-lg`: Apply a large border-radius to round the corners.
            
2. **Customizable**:
    
    - Tailwind CSS is **highly customizable**. You can modify the default theme, such as colors, font sizes, spacing, breakpoints, and more, through a configuration file (`tailwind.config.js`).
        
    - You can extend Tailwind’s built-in utility classes to fit your project's specific needs.
        
    
    **Example of custom configuration (`tailwind.config.js`)**:
    
    ```javascript
    module.exports = {
      theme: {
        extend: {
          colors: {
            'brand-blue': '#1D4ED8',
          },
          spacing: {
            '128': '32rem',
          },
        },
      },
    };
    ```
    
3. **Responsive Design**:
    
    - Tailwind makes building **responsive websites** easy. It provides built-in **responsive design utilities** using **breakpoints** for different screen sizes. These breakpoints are mobile-first, and you can apply specific styles for different screen sizes directly in your markup.
        
    
    **Example:**
    
    ```html
    <div class="text-sm md:text-lg lg:text-xl">
      This text changes size based on the screen width.
    </div>
    ```
    
    - In this example:
        
        - `text-sm`: Text size for small screens (mobile).
            
        - `md:text-lg`: Text size for medium screens (tablets).
            
        - `lg:text-xl`: Text size for large screens (desktops).
            
4. **No Opinionated Design**:
    
    - Tailwind doesn’t provide pre-built UI components. Instead, it gives you the flexibility to build your custom design from the ground up using utility classes.
        
    - This results in a **clean and unique design** without being constrained by the default component styles that other CSS frameworks provide.
        
5. **PurgeCSS Integration**:
    
    - Tailwind integrates **PurgeCSS** to remove unused CSS classes from your production builds, keeping the final CSS file size small. This is particularly useful because Tailwind generates a large number of utility classes, and PurgeCSS ensures that only the classes used in your HTML are included in the final CSS.
        
6. **Design Consistency**:
    
    - With Tailwind, you can ensure **design consistency** across your website by using a common set of utility classes. Since Tailwind enforces the use of predefined classes (like `text-gray-800` for gray text, `bg-blue-500` for blue backgrounds), you can maintain a uniform design language throughout your site.
        
7. **JIT Mode (Just-in-Time Mode)**:
    
    - Tailwind’s **JIT (Just-in-Time)** mode compiles CSS on-demand. Instead of generating a huge CSS file with all possible utilities, it only generates the CSS for the classes that you actually use in your HTML files. This results in smaller, more efficient CSS files and faster build times.
        

---

### Benefits of Using Tailwind CSS:

1. **Faster Development**:
    
    - Tailwind’s utility-first approach allows you to rapidly build custom UIs without having to write custom CSS for each component. You can create complex layouts by simply combining utility classes in the HTML.
        
2. **High Customization**:
    
    - You have full control over your design by customizing the utility classes to match your brand or project requirements. You can easily modify the default configuration, add custom colors, spacing, and breakpoints, and more.
        
3. **No More Context-Switching**:
    
    - With Tailwind, you can build the entire UI directly in your HTML, which reduces the need to switch between HTML and CSS files. This can improve workflow and make it easier to see how styles are applied directly in the HTML structure.
        
4. **Responsive and Mobile-First**:
    
    - Tailwind makes it easy to build responsive websites with its built-in mobile-first approach. The utility classes allow you to target different screen sizes using media queries directly in the HTML, without writing custom media queries.
        
5. **Cleaner HTML with Utility Classes**:
    
    - Instead of creating custom CSS classes for every component, you can apply Tailwind’s pre-defined utility classes directly in your HTML, which results in cleaner, more readable code. You don’t need to worry about creating additional CSS rules for each element.
        
6. **Works Well with Frameworks**:
    
    - Tailwind integrates seamlessly with front-end frameworks like **React**, **Vue**, **Angular**, and even static site generators. It can be used in single-page applications (SPAs) or multi-page applications (MPAs) alike.
        

---

### Tailwind CSS Workflow:

1. **Installation**:
    
    - You can add Tailwind to your project by installing it via **npm** (Node Package Manager) or **yarn** and configuring it with a **PostCSS** setup. Alternatively, you can use the CDN version for quick prototyping.
        
    
    **Using npm**:
    
    ```bash
    npm install tailwindcss
    ```
    
2. **Setting Up Tailwind**:
    
    - After installing Tailwind, you'll need to create a `tailwind.config.js` file to customize your theme (optional) and configure purge options.
        
    - You'll also need to import Tailwind’s base styles, components, and utilities in your main CSS file.
        
    
    **Example (CSS file)**:
    
    ```css
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```
    
3. **Building the Final CSS**:
    
    - When building your project for production, run a build script that compiles the Tailwind CSS file, removes unused CSS classes using **PurgeCSS**, and generates an optimized, smaller CSS file for deployment.
        
    
    ```bash
    npx tailwindcss build input.css -o output.css
    ```
    

---

### Example: Creating a Simple Card Component with Tailwind CSS:

```html
<div class="max-w-sm mx-auto bg-white rounded-lg shadow-md overflow-hidden">
  <img class="w-full h-48 object-cover" src="https://via.placeholder.com/300" alt="Image">
  <div class="p-4">
    <h2 class="text-xl font-semibold text-gray-800">Card Title</h2>
    <p class="text-gray-600 mt-2">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla quam velit, vulputate eu pharetra nec, mattis ac neque.</p>
    <a href="#" class="mt-4 inline-block px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600">Read More</a>
  </div>
</div>
```

In this example:

- **Utility classes** like `bg-white`, `rounded-lg`, `shadow-md`, `text-gray-800`, `text-xl`, etc., are applied directly to the HTML elements.
    
- Tailwind CSS provides pre-designed utilities for background colors, text sizes, spacing, and more, making it quick to build a card component.
    

---

### Conclusion:

**Tailwind CSS** is a **utility-first** CSS framework that empowers developers to build custom, responsive, and visually appealing designs by using a set of low-level utility classes. It offers a highly **customizable** approach, allowing you to create unique designs without being constrained by pre-designed components. Tailwind makes it easy to build modern web applications faster and more efficiently, with built-in support for responsive design, animations, and modularity. Whether you are building a small prototype or a large-scale web application, Tailwind CSS provides flexibility and speed for web development.

## Resources
- [Official Website](https://tailwindcss.com/)
- [Tailwind Labs](https://www.youtube.com/c/TailwindLabs)

## Tutorial
- [Adam Wathan - Building a Kanban Board with Tailwind CSS](https://www.youtube.com/watch?v=_H38A6E8Nsg)
- [David Levai - Glassmorphism with Tailwind CSS Under 60 seconds](https://www.youtube.com/watch?v=sIRbiNKJ0Cc&list=WL)
- [Gravin Joyce - Building Intercom's Inbox UI with Tailwind CSS](https://www.youtube.com/watch?v=cg1qbkG0KRI)
- [Learn TailwindCSS in 30 minutes](https://medium.com/@mhdnauvalazhar/mempelajari-tailwindcss-dalam-30-menit-673742056e0c)
- Tailwind Labs
	- [Building a command palette with Tailwind CSS, React, and Headless UI](https://www.youtube.com/watch?v=-jix4KyxLuQ&list=WL)

## Contributors
- [[Muhammad Agung Sundoro]]