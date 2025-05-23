`WP_User_Query` is a powerful class in WordPress that allows you to retrieve user data from the WordPress database based on various query parameters. It is particularly useful when you need to retrieve specific users or groups of users with custom conditions, such as finding all users who have a particular role, are active, or meet other criteria.

Using `WP_User_Query`, you can filter, sort, and display user information without needing to write custom SQL queries. This class abstracts away the complexities of database queries and provides a clean and efficient way to interact with user data.

### **Basic Syntax**

The basic syntax for using `WP_User_Query` is as follows:

```php
$user_query = new WP_User_Query( $args );
```

Where `$args` is an associative array of arguments used to filter the users based on your requirements. After running the query, you can access the results via the `$user_query->results` property.

### **Common Arguments for WP_User_Query**

Here are some of the most commonly used arguments you can pass to the `WP_User_Query` constructor to customize your user query:

1. **`role`**:
    - Filters users by their role.
    - Example: Get all users with the role "subscriber".
    
    ```php
    $args = array(
      'role' => 'subscriber'
    );
    ```
    
2. **`role__in`**:
    - Filters users by multiple roles (array of roles).
    - Example: Get users who are either "editor" or "author".
    
    ```php
    $args = array(
      'role__in' => array( 'editor', 'author' )
    );
    ```
    
3. **`role__not_in`**:
    - Excludes users from certain roles.
    - Example: Get all users who are not "administrator" or "editor".
    
    ```php
    $args = array(
      'role__not_in' => array( 'administrator', 'editor' )
    );
    ```
    
4. **`meta_key` and `meta_value`**:
    - Filter users based on user meta data.
    - Example: Get users who have a custom meta key (`user_age`) with a specific value.
    
    ```php
    $args = array(
      'meta_key' => 'user_age',
      'meta_value' => 25
    );
    ```
    
5. **`meta_query`**:
    - Allows for complex meta queries, such as filtering users based on multiple custom fields.
    - Example: Get users whose `user_age` is greater than 20.
    
    ```php
    $args = array(
      'meta_query' => array(
        array(
          'key' => 'user_age',
          'value' => 20,
          'compare' => '>'
        )
      )
    );
    ```
    
6. **`include`**:
    - Filter users by specific user IDs.
    - Example: Get users with IDs 1, 2, and 3.
    
    ```php
    $args = array(
      'include' => array(1, 2, 3)
    );
    ```
    
7. **`exclude`**:
    - Exclude users by their user IDs.
    - Example: Exclude users with IDs 1, 2, and 3.
    
    ```php
    $args = array(
      'exclude' => array(1, 2, 3)
    );
    ```
    
8. **`orderby`**:
    - Controls how the results are ordered.
    - Common values: `ID`, `login`, `email`, `url`, `registered`, `display_name`, etc.
    - Example: Order users by their registration date.
    
    ```php
    $args = array(
      'orderby' => 'registered'
    );
    ```
    
9. **`order`**:
    - Defines whether the query results should be in ascending (`ASC`) or descending (`DESC`) order.
    - Example: Order users by their registration date in descending order.
    
    ```php
    $args = array(
      'orderby' => 'registered',
      'order' => 'DESC'
    );
    ```
    
10. **`number`**:
    - Limits the number of results returned.
    - Example: Get only 10 users.
    
    ```php
    $args = array(
      'number' => 10
    );
    ```
    
11. **`paged`**:
    - Used for pagination. It specifies which page of results to retrieve.
    - Example: Get users on page 2, with 10 users per page.
    
    ```php
    $args = array(
      'number' => 10,
      'paged' => 2
    );
    ```

### **Example Usage of WP_User_Query**

Here’s an example of how to use `WP_User_Query` to retrieve a list of users with specific conditions:

```php
$args = array(
  'role' => 'subscriber',  // Filter users with the 'subscriber' role
  'orderby' => 'registered', // Order users by their registration date
  'order' => 'DESC',         // Descending order
  'number' => 5,             // Limit results to 5 users
);

$user_query = new WP_User_Query( $args );

if ( ! empty( $user_query->results ) ) {
  foreach ( $user_query->results as $user ) {
    echo 'User ID: ' . $user->ID . '<br>';
    echo 'Username: ' . $user->user_login . '<br>';
    echo 'Email: ' . $user->user_email . '<br>';
    echo 'Registration Date: ' . $user->user_registered . '<br><br>';
  }
} else {
  echo 'No users found.';
}
```

In this example:
- We retrieve users with the role "subscriber."
- We order the users by their registration date in descending order.
- We limit the results to 5 users.
- We then loop through the results and display the user's ID, username, email, and registration date.

### **Accessing User Data with WP_User_Query**

The `WP_User_Query` object returns a list of users in the `results` property. Each user object contains various properties such as:
- `ID`: User's unique ID.
- `user_login`: Username.
- `user_email`: User's email address.
- `user_registered`: User's registration date.
- `display_name`: The name displayed publicly.
- `roles`: An array of the user's roles (e.g., `subscriber`, `administrator`).

You can access these properties directly from the `WP_User` object inside the `results` array.

Example:

```php
foreach ( $user_query->results as $user ) {
  echo 'Username: ' . $user->user_login . '<br>';
  echo 'Roles: ' . implode( ', ', $user->roles ) . '<br>';
}
```

### **Advanced Usage**

#### **Complex Meta Query**

You can use `meta_query` to filter users based on custom user meta fields. For example, if you have a custom field like `user_age`, you can query users whose age is above a certain threshold:

```php
$args = array(
  'meta_query' => array(
    array(
      'key' => 'user_age',
      'value' => 30,
      'compare' => '>',
      'type' => 'NUMERIC'
    )
  )
);

$user_query = new WP_User_Query( $args );
```

#### **Pagination with WP_User_Query**

For large datasets, you may want to paginate the user results. You can use the `paged` argument to manage pagination:

```php
$args = array(
  'number' => 10,  // Show 10 users per page
  'paged' => 2,    // Show users on page 2
);

$user_query = new WP_User_Query( $args );
```

### **Performance Considerations**

`WP_User_Query` can be resource-intensive, especially on sites with large user bases. Here are some tips for improving performance:
- **Limit the number of results**: Always use the `number` argument to limit the number of users returned.
- **Use `meta_query` wisely**: If querying by custom fields, ensure proper indexing is in place and limit the number of fields involved in the query.
- **Use caching**: For frequently requested user data, consider caching the results to reduce database load.

## Resource
- [WordPress Developer - WP_User_Query](https://developer.wordpress.org/reference/classes/wp_user_query/)