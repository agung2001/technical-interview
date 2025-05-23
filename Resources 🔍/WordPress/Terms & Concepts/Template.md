A **WordPress template** refers to the structure and layout of a website or a specific page on a WordPress-powered website. Templates in WordPress are made up of **template files**, which control the design and content rendering of the website. These files are written in PHP and HTML and are used to display content, styles, and interactive elements on your site.

WordPress templates are responsible for presenting the data in the most user-friendly way, and each template file has a specific function, such as displaying the homepage, individual posts, or archives.

### **WordPress Template Files**
A **template file** is a PHP file that WordPress uses to control the appearance of different types of content. Template files are organized in the **theme directory** of your WordPress site (usually located in `wp-content/themes/your-theme-name/`).

Some of the key template files include:
1. **index.php**: The fallback template file. If no other template file matches a request, WordPress will use `index.php` to display the page.
2. **single.php**: This template is used to display a single blog post or any single piece of content. It’s used when a user views a specific post or article.
3. **page.php**: Used for displaying static pages like "About Us," "Contact," or "Privacy Policy."
4. **archive.php**: Used for displaying archives, such as category, tag, date, and author archives.
5. **category.php**: Used for displaying posts in a specific category.
6. **tag.php**: Used for displaying posts associated with a specific tag.
7. **search.php**: Displays search results when a user performs a search query on your website.
8. **404.php**: This template is displayed when a user navigates to a page that doesn't exist (404 error).
9. **sidebar.php**: Contains the structure for displaying sidebars, such as widget areas, on various pages.
10. **footer.php**: Contains the HTML for the footer section of the website.
11. **header.php**: Contains the HTML for the header section of the website, such as the site’s title, logo, and navigation menu.

### **Template Tags**
WordPress uses **template tags** within template files to dynamically display content and information. Template tags are PHP functions that can be placed inside template files to output content like post titles, categories, custom fields, and much more.

Examples of common template tags:
- `the_title()`: Displays the title of the post or page.
- `the_content()`: Displays the content of a post or page.
- `the_permalink()`: Outputs the URL of a post.
- `get_header()`: Includes the header template file.
- `get_footer()`: Includes the footer template file.
- `get_sidebar()`: Includes the sidebar template file.
- `wp_head()`: Outputs essential HTML code to the head section (e.g., for plugins or theme settings).

### **WordPress Template Hierarchy**
![](https://i0.wp.com/developer.wordpress.org/files/2014/10/Screenshot-2019-01-23-00.20.04.png?resize=1024%2C639&ssl=1)

The **template hierarchy** defines the order in which WordPress looks for template files to render a specific type of content. If WordPress cannot find the requested template file, it will use a more general file. The template hierarchy is very important because it helps WordPress determine which file to use for each request.

Here’s a simplified overview of how the WordPress template hierarchy works:

1. **Home Page**:
    - `home.php` (if it exists)
    - `index.php` (fallback)
2. **Single Post**:
    - `single-{post_type}.php` (for custom post types)
    - `single.php`
    - `index.php` (fallback)
3. **Page**:
    - `page-{slug}.php` (if the page has a specific template for its slug)
    - `page.php`
    - `index.php` (fallback)
4. **Category Archive**:
    - `category-{slug}.php` (for specific category slug)
    - `category-{id}.php` (for specific category ID)
    - `category.php`
    - `archive.php`
    - `index.php` (fallback)
5. **Tag Archive**:
    - `tag-{slug}.php`
    - `tag.php`
    - `archive.php`
    - `index.php` (fallback)
6. **Search Results**:
    - `search.php`
    - `index.php` (fallback)
7. **404 Page**:
    - `404.php` (if it exists)
    - `index.php` (fallback)
8. **Custom Post Types**:
    - `single-{custom_post_type}.php`
    - `archive-{custom_post_type}.php`
    - `single.php`
    - `archive.php`
    - `index.php` (fallback)

### **How the Template Hierarchy Works in Practice**
Let’s say a user navigates to a blog post on your WordPress site. Here’s what happens:
1. WordPress first looks for a template file for the post. It checks if a `single.php` file exists in your theme.
2. If `single.php` is not found, WordPress checks for a more specific file, like `single-{post_type}.php` (e.g., `single-post.php` or `single-book.php`).
3. If neither of these files exists, WordPress will fall back to the `index.php` file as the final fallback template.

### **Template Hierarchy for Different Views**
- **For a single blog post**:
    - `single-{post_type}.php`
    - `single.php`
    - `index.php`
- **For a category archive page**:
    - `category-{slug}.php`
    - `category-{id}.php`
    - `category.php`
    - `archive.php`
    - `index.php`
- **For a page with the slug “about”**:
    - `page-about.php`
    - `page.php`
    - `index.php`
- **For a 404 error page**:
    - `404.php`
    - `index.php`

## Resource
- WordPress Developer
	- [Template Files](https://developer.wordpress.org/themes/basics/template-files/)
	- [Template Hierarchy](https://developer.wordpress.org/themes/basics/template-hierarchy/)
	- [Template Tags](https://codex.wordpress.org/Template_Tags)