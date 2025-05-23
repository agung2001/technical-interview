<iframe width="560" height="315" src="https://www.youtube.com/embed/_IMtVON0AZk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

A **nonce** (a number used once) in WordPress is a security token used to protect URLs and forms from **cross-site request forgery (CSRF)** attacks. Nonces help ensure that a request to perform a specific action (like submitting a form, making a request to the server, or updating a piece of data) is legitimate and originated from your WordPress site, rather than a malicious external source.

In WordPress, nonces are used as a way to validate that the request made by a user is intended and not forged, ensuring the security of sensitive actions performed on your site.

### **What is a WordPress Nonce?**
A nonce is a **cryptographic token** that WordPress generates to ensure the validity of requests and to prevent unauthorized actions. Nonces are often used to verify requests that could potentially change the state of the system (such as deleting posts, changing settings, or submitting data) to confirm that the request originates from the current user and not from an external, potentially malicious source.

Nonces are commonly used in:
- Form submissions (e.g., submitting a comment, contact form, or user settings form).
- URL-based actions (e.g., deleting a post or changing a setting via a link).
- API requests and AJAX calls.

### **How Does a WordPress Nonce Work?**
1. **Generating a Nonce**:  
    Nonces are generated using the `wp_nonce_field()` or `wp_create_nonce()` functions in WordPress. The nonce is then passed along with a form, URL, or Ajax request.
2. **Validating a Nonce**:  
    When a request is made, WordPress checks the nonce to ensure it is valid and has not expired. This is done using the `check_admin_referer()` or `verify_nonce()` functions.
3. **Nonce Expiry**:  
    Nonces in WordPress have an expiration time, typically 24 hours. After this period, they become invalid, reducing the risk of replay attacks.

### **Generating a Nonce**
#### **1. Nonce in Forms (wp_nonce_field)**
When creating a form in WordPress that requires nonce validation (for example, when submitting a custom settings form), you can generate a nonce field using the `wp_nonce_field()` function. This function generates a hidden field containing the nonce, which you then include in the form.

Example of using `wp_nonce_field()` in a form:

```php
<form method="post" action="options.php">
  <?php
    // Generate a nonce field with a specific action name
    wp_nonce_field('my_nonce_action', 'my_nonce_field');
  ?>
  <input type="submit" value="Save Settings">
</form>
```

In this example:
- `'my_nonce_action'`: This is a unique string (nonce action) that is used to identify the nonce when validating.
- `'my_nonce_field'`: This is the name of the nonce field that will hold the nonce value.

When the form is submitted, the nonce value is sent along with the form data.

#### **2. Nonce for URL-Based Actions (wp_nonce_url)**
If you're adding a nonce to a URL (for example, for deleting a post or updating settings), you can use the `wp_nonce_url()` function. This function appends the nonce to the URL.

Example of generating a nonce for a URL:

```php
<?php
$nonce_url = wp_nonce_url( 'admin-post.php?action=my_action', 'my_nonce_action' );
echo '<a href="' . $nonce_url . '">Click here to perform the action</a>';
?>
```

This example:
- Adds a nonce to the URL, validating the action (`'my_nonce_action'`).
- When the link is clicked, the nonce is passed to `admin-post.php` to validate the request.

### **Validating a Nonce**
Once the form or URL with the nonce is submitted, you need to validate the nonce to ensure that the request is legitimate. WordPress provides several functions to check nonces:

#### **1. Validating a Nonce in Forms (check_admin_referer)**
When processing a form submission, use the `check_admin_referer()` function to validate the nonce. This function checks if the nonce is valid and prevents unauthorized requests.

Example:

```php
if (isset($_POST['my_nonce_field']) && check_admin_referer('my_nonce_action', 'my_nonce_field')) {
    // Nonce is valid, process the form data
    echo 'Form submission is valid!';
} else {
    // Invalid nonce, stop processing
    die('Security check failed!');
}
```

In this example:
- `check_admin_referer()` validates the nonce sent from the form (`'my_nonce_action'`).
- If the nonce is invalid or missing, it stops further processing and displays a security error message.

#### **2. Validating a Nonce for URL-Based Actions (check_admin_referer or wp_verify_nonce)**
If the nonce is attached to a URL (like for deletion or an action), you can validate the nonce using the `check_admin_referer()` function as well.

Example for URL action:

```php
if (isset($_GET['my_nonce_field']) && check_admin_referer('my_nonce_action', 'my_nonce_field')) {
    // Valid nonce, perform the action
    echo 'Action is valid!';
} else {
    // Invalid nonce, stop processing
    die('Security check failed!');
}
```

Alternatively, for non-admin pages, you can use the `wp_verify_nonce()` function to validate the nonce.

Example:

```php
if (wp_verify_nonce($_GET['my_nonce_field'], 'my_nonce_action')) {
    // Nonce is valid, proceed with the action
} else {
    // Invalid nonce
    die('Security check failed!');
}
```

### **Security Considerations**
- **Nonce Expiry**: Nonces are valid for a limited time (usually 24 hours). This helps prevent replay attacks (where an attacker reuses a valid nonce after it has been used).
- **Nonces Are Not for User Authentication**: Nonces are used to validate actions and ensure they are legitimate, but they should not be used as the sole form of authentication. User authentication (such as login and roles) should still be handled with WordPress’s built-in authentication system.
- **Always Use Nonces in Sensitive Actions**: Whenever you're processing sensitive actions like updating user data, deleting content, or submitting forms, always use nonces to protect those actions from external attacks.

### **Example of Nonce in an Ajax Request**
WordPress also uses nonces for Ajax requests to ensure that requests sent via Ajax are valid and come from an authorized source.

Example:

1. **JavaScript (Enqueueing the Script with Nonce)**:
    
    ```javascript
    jQuery(document).ready(function($){
      var data = {
        action: 'my_ajax_action',
        nonce: my_ajax_obj.nonce // Nonce passed from PHP
      };
      
      $.post(my_ajax_obj.ajaxurl, data, function(response) {
        alert(response);
      });
    });
    ```
    
2. **PHP (Generating the Nonce and Handling the Ajax Request)**:
    
    ```php
    function enqueue_my_ajax_script() {
      wp_enqueue_script('my-ajax-script', get_template_directory_uri() . '/js/ajax.js', array('jquery'), null, true);
      
      // Localize script to pass the nonce and ajaxurl
      wp_localize_script('my-ajax-script', 'my_ajax_obj', array(
        'nonce' => wp_create_nonce('my_nonce_action'),
        'ajaxurl' => admin_url('admin-ajax.php')
      ));
    }
    add_action('wp_enqueue_scripts', 'enqueue_my_ajax_script');
    
    function handle_my_ajax_action() {
      if (!isset($_POST['nonce']) || !wp_verify_nonce($_POST['nonce'], 'my_nonce_action')) {
        die('Nonce verification failed');
      }
      
      // Your AJAX logic here
      echo 'AJAX request was successful!';
      wp_die();
    }
    add_action('wp_ajax_my_ajax_action', 'handle_my_ajax_action');
    ```
    
## Resource
- [WP Developer Resources - Nonces](https://developer.wordpress.org/apis/security/nonces/)