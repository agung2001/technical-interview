### **Creating Custom Widgets**

While WordPress comes with a lot of built-in widgets, sometimes you might need a widget tailored to your site's specific needs. You can create custom widgets by writing your own widget class in your theme or plugin.

Here’s how to create a simple custom widget:

#### **Step-by-Step Example to Create a Custom Widget in WordPress**
1. **Create a Widget Class**:
    - Define a class that extends the `WP_Widget` class provided by WordPress. The class will have methods for displaying the widget form, handling widget settings, and outputting the widget content.
    
    Example:
    
    ```php
    class My_Custom_Widget extends WP_Widget {
    
      // Constructor
      public function __construct() {
        parent::__construct(
          'my_custom_widget',  // Base ID
          'My Custom Widget',   // Widget Name
          array('description' => 'A custom widget example')  // Widget options
        );
      }
    
      // Front-end display of widget
      public function widget($args, $instance) {
        echo $args['before_widget'];
        echo '<h2>' . $instance['title'] . '</h2>';
        echo '<p>' . $instance['content'] . '</p>';
        echo $args['after_widget'];
      }
    
      // Back-end widget form
      public function form($instance) {
        $title = !empty($instance['title']) ? $instance['title'] : 'Default Title';
        $content = !empty($instance['content']) ? $instance['content'] : 'Default content';
        ?>
        <p>
          <label for="<?php echo $this->get_field_id('title'); ?>">Title:</label>
          <input class="widefat" id="<?php echo $this->get_field_id('title'); ?>" name="<?php echo $this->get_field_name('title'); ?>" type="text" value="<?php echo esc_attr($title); ?>" />
        </p>
        <p>
          <label for="<?php echo $this->get_field_id('content'); ?>">Content:</label>
          <textarea class="widefat" id="<?php echo $this->get_field_id('content'); ?>" name="<?php echo $this->get_field_name('content'); ?>"><?php echo esc_attr($content); ?></textarea>
        </p>
        <?php
      }
    
      // Updating widget settings
      public function update($new_instance, $old_instance) {
        $instance = $old_instance;
        $instance['title'] = strip_tags($new_instance['title']);
        $instance['content'] = strip_tags($new_instance['content']);
        return $instance;
      }
    }
    ```
    
2. **Register the Widget**:
    - Once you’ve created the widget class, register it with WordPress using the `widgets_init` action hook.
    
    Example:
    
    ```php
    function register_my_custom_widget() {
      register_widget('My_Custom_Widget');
    }
    add_action('widgets_init', 'register_my_custom_widget');
    ```
    
3. **Use the Custom Widget**:
    - After registering your widget, you can add it to your widget areas just like any other widget through the **Appearance > Widgets** section.


## Resource
- [WordPress Codex - Widgets_API](https://codex.wordpress.org/Widgets_API#Widgets_API)