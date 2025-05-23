<iframe width="560" height="315" src="https://www.youtube.com/embed/Orrn9f-L0mI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

WordPress custom post types are a way to define new types of content in WordPress. By default, WordPress comes with two post types: posts and pages. Custom post types allow you to define new types of content that are specific to your website.

For example, if you have a website about recipes, you might want to define a custom post type called "recipes" that has its own set of custom fields and taxonomies. This would allow you to create a separate section of your website for recipes that is distinct from your posts and pages.

To create a custom post type in WordPress, you can use the `register_post_type()` function, which allows you to specify various parameters such as the name, labels, and capabilities of the post type. Once you have registered a custom post type, you can create and manage posts of that type just like you would with the built-in post types.

Custom post types are a powerful feature of WordPress that allows you to create complex websites with diverse content types. They are often used in conjunction with custom taxonomies, custom fields, and other advanced features to create fully customized WordPress websites.

## Custom Post Statuses
```php
<?php
function my_custom_post_statuses() {
    register_post_status( 'awaiting_review', array(
        'label'                     => _x( 'Awaiting Review', 'Post Status General', 'your-text-domain' ),
        'label_count'               => _n_noop( 'Awaiting Review <span class="count">(%s)</span>', 'Awaiting Reviews <span class="count">(%s)</span>', 'your-text-domain' ),
        'public'                    => false, // Not publicly viewable on the front end
        'exclude_from_search'       => true,
        'show_in_admin_all_list'    => true, // Show in 'All' count in admin
        'show_in_admin_status_list' => true, // Show in status filter list at the top
        'post_type'                 => array( 'post', 'my_custom_post_type' ), // Limit to specific post types
    ) );

    register_post_status( 'approved', array(
        'label'                     => _x( 'Approved', 'Post Status General', 'your-text-domain' ),
        'label_count'               => _n_noop( 'Approved <span class="count">(%s)</span>', 'Approved <span class="count">(%s)</span>', 'your-text-domain' ),
        'public'                    => false,
        'exclude_from_search'       => true,
        'show_in_admin_all_list'    => true,
        'show_in_admin_status_list' => true,
        'post_type'                 => array( 'post', 'my_custom_post_type' ),
    ) );
}
add_action( 'init', 'my_custom_post_statuses' );
?>
```

## Resource
- [WP Developer Resources - Custom Post Types](https://developer.wordpress.org/plugins/post-types/)