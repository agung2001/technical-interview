For developers, the **Block API** in WordPress allows the creation of custom blocks with specific functionality tailored to the needs of the site. This involves working with **JavaScript** (primarily **React**) and **PHP** to register blocks in WordPress.

Here’s an outline of how to create a custom block:

1. **Block Registration**:  
    WordPress blocks are registered using the `registerBlockType()` function, which defines the block’s name, title, icon, category, attributes, and rendering function.
    
    Example:
    
    ```javascript
    const { registerBlockType } = wp.blocks;
    const { TextControl } = wp.components;
    
    registerBlockType('myplugin/custom-block', {
      title: 'Custom Block',
      icon: 'smiley',
      category: 'common',
      attributes: {
        content: {
          type: 'string',
          default: 'Hello World!',
        },
      },
      edit: function(props) {
        return (
          <div>
            <TextControl
              label="Block Content"
              value={props.attributes.content}
              onChange={(newContent) => props.setAttributes({ content: newContent })}
            />
          </div>
        );
      },
      save: function(props) {
        return <p>{props.attributes.content}</p>;
      },
    });
    ```
    
2. **Block Styling and Customization**:  
    Developers can define **custom styles** and interactions within the block. These can be implemented with JavaScript (React components), CSS, or inline styles.
    
3. **Dynamic Blocks**:  
    Some blocks need to be rendered on the server side (for example, displaying the latest posts). WordPress allows creating dynamic blocks, which render content on the server using PHP.
    
    Example of a dynamic block:
    
    ```javascript
    registerBlockType('myplugin/latest-posts', {
      title: 'Latest Posts',
      category: 'widgets',
      edit: function() {
        return <div className="loading">Loading latest posts...</div>;
      },
      save: function() {
        return null;  // Server-side rendering
      },
    });
    ```
    
    On the server, the PHP callback function will handle the rendering logic and send the data to the client-side.
    
4. **Block Patterns and Block Variations**:  
    Developers can also define **block patterns** (predefined block layouts) or **block variations** (different styles or configurations of an existing block) to further enhance the WordPress block ecosystem.

## Projects
- [GitHub - agung2001/hands-on-gutenberg-block](https://github.com/agung2001/hands-on-gutenberg-block)

## Resource
- [WordPress Developer - Block API Reference](https://developer.wordpress.org/block-editor/reference-guides/block-api/)
- [WP Developer Resource - Block Editor Handbook](https://developer.wordpress.org/block-editor/)
	- [Components](https://developer.wordpress.org/block-editor/reference-guides/components/)
	- [Modal](https://developer.wordpress.org/block-editor/reference-guides/components/modal/)
	- [Packages](https://developer.wordpress.org/block-editor/reference-guides/packages/)
- Documentation
	- [Tutorial: Build your first block](https://developer.wordpress.org/block-editor/getting-started/tutorial/)
	- [Registration](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-registration/)
- Article
	- [Human Made - Hot Module Replacement for Gutenberg Blocks](https://humanmade.com/engineering/hot-module-replacement-for-gutenberg-blocks/)

## Related
- [[Resources 🔍/WordPress/Terms & Concepts/Block|Block]]
- [[Gutenberg]]