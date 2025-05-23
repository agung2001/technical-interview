WordPress uses the **$wpdb** global variable to interact with the WordPress database. This variable gives you access to the `wpdb` class, which provides a set of methods for executing SQL queries safely. It helps prevent SQL injection attacks and ensures that queries are compatible with different database types (such as MySQL and MariaDB).

Here are some **sample WordPress SQL queries** using `$wpdb`:

### **Basic Select Query**
A simple query to retrieve data from the database. For example, retrieving the titles of all published posts.

```php
global $wpdb;

$query = "SELECT post_title FROM {$wpdb->posts} WHERE post_status = 'publish'";

$results = $wpdb->get_results($query);

foreach ($results as $post) {
    echo $post->post_title . "<br>";
}
```

**Explanation**:
- `{$wpdb->posts}` refers to the `wp_posts` table (prefix `wp_` is dynamic).
- `get_results()` retrieves all rows from the query.
- The results are looped through to display the post titles.

### **Using Prepared Statements (Secure Query)**
To prevent SQL injection, always use prepared statements when dealing with user input. Here's an example of selecting posts by a specific author:

```php
global $wpdb;

$author_id = 1; // Example author ID
$query = $wpdb->prepare(
    "SELECT post_title FROM {$wpdb->posts} WHERE post_author = %d AND post_status = 'publish'",
    $author_id
);

$results = $wpdb->get_results($query);

foreach ($results as $post) {
    echo $post->post_title . "<br>";
}
```

**Explanation**:
- `prepare()` safely prepares the SQL query by binding the `$author_id` variable to the query, ensuring no malicious input is executed.
- `%d` is a placeholder for integers, and `$wpdb->prepare()` automatically escapes and sanitizes the input.
    
### **Insert Data into the Database**
Inserting a new post into the database:

```php
global $wpdb;

$wpdb->insert(
    $wpdb->posts,
    array(
        'post_title'   => 'Sample Post Title',
        'post_content' => 'This is a sample content.',
        'post_status'  => 'publish',
        'post_author'  => 1, // Author ID
        'post_date'    => current_time('mysql')
    )
);

echo 'Post inserted successfully!';
```

**Explanation**:
- `$wpdb->insert()` is a safe method to insert data into a table. It accepts the table name, an associative array of data to insert, and optionally an array of data types (defaults to `%s` for strings, `%d` for integers, etc.).
- This inserts a new post into the `wp_posts` table.

### **Update Data in the Database**
Updating an existing post:

```php
global $wpdb;

$post_id = 123; // The ID of the post to update
$new_content = 'This is the updated content.';

$wpdb->update(
    $wpdb->posts,
    array('post_content' => $new_content),
    array('ID' => $post_id),
    array('%s'), // Data type for post_content
    array('%d')  // Data type for post ID
);

echo 'Post updated successfully!';
```

**Explanation**:
- `$wpdb->update()` is used to update existing records. It takes the table name, an associative array of columns to update, the `WHERE` condition (in this case, post ID), and optional data types for the columns.
- The `post_content` of the post with ID `123` is updated.

### **Delete Data from the Database**
Deleting a post by its ID:

```php
global $wpdb;

$post_id = 123; // The ID of the post to delete

$wpdb->delete(
    $wpdb->posts,
    array('ID' => $post_id),
    array('%d') // Data type for post ID
);

echo 'Post deleted successfully!';
```

**Explanation**:
- `$wpdb->delete()` is used to delete records from the database. It accepts the table name, the `WHERE` condition, and optionally the data types.
- This example deletes the post with ID `123`.

### **Count Rows in a Table**
Counting the number of published posts:

```php
global $wpdb;

$query = "SELECT COUNT(*) FROM {$wpdb->posts} WHERE post_status = 'publish'";

$post_count = $wpdb->get_var($query);

echo "Number of published posts: " . $post_count;
```

**Explanation**:
- `$wpdb->get_var()` is used to return a single variable, which in this case is the count of published posts.
- `COUNT(*)` is a SQL aggregate function that returns the number of rows.

### **Complex Join Query**
A more complex query using a `JOIN` to fetch post titles and categories:

```php
global $wpdb;

$query = "
    SELECT p.post_title, t.name AS category_name
    FROM {$wpdb->posts} p
    JOIN {$wpdb->term_relationships} tr ON p.ID = tr.object_id
    JOIN {$wpdb->term_taxonomy} tt ON tr.term_taxonomy_id = tt.term_taxonomy_id
    JOIN {$wpdb->terms} t ON tt.term_id = t.term_id
    WHERE p.post_status = 'publish' AND tt.taxonomy = 'category'
";

$results = $wpdb->get_results($query);

foreach ($results as $row) {
    echo $row->post_title . ' - ' . $row->category_name . "<br>";
}
```

**Explanation**:
- This query joins the `wp_posts`, `wp_term_relationships`, `wp_term_taxonomy`, and `wp_terms` tables to fetch post titles and their associated category names.
- This example demonstrates how to work with WordPress taxonomies and relationships between posts and terms.

### **Searching with LIKE**
Searching for posts with a specific keyword in the title:

```php
global $wpdb;

$keyword = 'example'; // The keyword to search for
$query = $wpdb->prepare(
    "SELECT post_title FROM {$wpdb->posts} WHERE post_title LIKE %s AND post_status = 'publish'",
    '%' . $wpdb->esc_like($keyword) . '%'
);

$results = $wpdb->get_results($query);

foreach ($results as $post) {
    echo $post->post_title . "<br>";
}
```

**Explanation**:
- The `LIKE` operator is used for pattern matching in SQL. The `esc_like()` method is used to escape the keyword before using it in a query to prevent SQL injection.
- The `%` symbols are wildcards, meaning that any title containing the keyword `example` will be returned.

## Resource
- [WordPress Developer - class wpdb](https://developer.wordpress.org/reference/classes/wpdb/)