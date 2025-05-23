**oEmbed** is a web standard that allows websites to easily embed content from other websites (such as videos, images, or other media) by simply using a URL. It’s a form of **automatic embedding**, where you paste a URL, and the system automatically converts it into an embedded element, like an embedded video or image.

In WordPress, **oEmbed** is a feature that automatically converts supported URLs into embedded media, such as videos, audio, tweets, and other content, without the need for complex HTML code or iframe tags. It simplifies embedding external content and enhances the user experience by allowing you to embed media easily.

### **How oEmbed Works in WordPress**
oEmbed works by recognizing specific types of URLs and replacing them with a full embed code. When you paste a URL into the WordPress post editor, WordPress checks if the URL matches a supported oEmbed provider (e.g., YouTube, Vimeo, Twitter). If it does, WordPress automatically converts the URL into the proper embed code.

This feature saves time and simplifies the process of embedding media, eliminating the need to manually generate embed codes.

### **Supported oEmbed Providers in WordPress**
WordPress supports many popular oEmbed providers, meaning that URLs from these sites will automatically be converted into embedded content:
- **YouTube**: Automatically embeds YouTube videos.
- **Vimeo**: Automatically embeds Vimeo videos.
- **Twitter**: Automatically embeds tweets, timelines, and Twitter feeds.
- **Instagram**: Automatically embeds Instagram posts, including images and videos.
- **Facebook**: Automatically embeds posts, images, and videos from Facebook.
- **Flickr**: Automatically embeds images from Flickr.
- **SoundCloud**: Automatically embeds SoundCloud audio tracks.
- **Spotify**: Automatically embeds music tracks from Spotify.

Additionally, WordPress allows you to add custom oEmbed providers by extending the oEmbed functionality with plugins.

### **How to Use oEmbed in WordPress**

#### **1. Embedding Content Automatically**
To embed content from a supported provider, all you need to do is paste the URL of the content into the WordPress block editor or classic editor. WordPress will automatically detect the URL and embed it.

Example:
- **YouTube Video**: Simply paste the URL of a YouTube video into your post, and WordPress will automatically embed the video.
    
    ```text
    https://www.youtube.com/watch?v=dQw4w9WgXcQ
    ```
    
- **Tweet**: Paste the URL of a tweet, and WordPress will embed the tweet.
    
    ```text
    https://twitter.com/elonmusk/status/1363120484078724097
    ```
    
- **Instagram Post**: Paste the URL of an Instagram post, and WordPress will embed it.
    
    ```text
    https://www.instagram.com/p/CBVqG9sj7l2/
    ```

In the editor, when you paste the URL, WordPress automatically converts it into an embedded element and displays it as it would appear on the external website.

#### **2. Embedding via oEmbed Block (Block Editor)**
WordPress introduced the **oEmbed block** in the block editor (Gutenberg). This block allows you to easily embed content by using the specific block for external URLs.

- To use the **oEmbed block**:
    1. Click on the **+** button in the block editor to add a new block.
    2. Search for the **oEmbed** block and select it.
    3. Paste the URL into the block, and WordPress will automatically embed the content.

#### **3. Embedding via Classic Editor**

In the classic editor (TinyMCE), WordPress automatically converts supported URLs into embed code when you paste the URL directly into the editor. You do not need to do anything special; just paste the URL, and WordPress handles the rest.

---

### **oEmbed for Custom Providers**

While WordPress has built-in support for a wide range of oEmbed providers, you can add support for additional providers (like custom video services or media platforms) through plugins or custom code.

If you want to add a custom oEmbed provider to WordPress, you can use the `oembed_providers` filter to register new oEmbed providers.

Example of registering a custom oEmbed provider:

```php
function add_custom_oembed_provider( $providers ) {
    $providers['#https?://customprovider.com/media/.*#i'] = 'https://customprovider.com/oembed?url=$1';
    return $providers;
}
add_filter( 'oembed_providers', 'add_custom_oembed_provider' );
```

In this example:

- We add a new provider by matching a URL pattern (using a regular expression).
    
- When a matching URL is found, it will be passed through the custom oEmbed URL (the second part of the function).
    

### **Advanced Customization of oEmbed**

While oEmbed is largely automatic in WordPress, there are ways to customize the behavior:

- **oEmbed Filters**: WordPress provides filters to modify the way content is embedded. For instance, you can use the `oembed_dataparse` filter to modify the embed code before it’s displayed.
    
    Example:
    
    ```php
    function custom_oembed_dataparse( $html, $url, $args ) {
        if ( strpos( $url, 'youtube.com' ) !== false ) {
            $html = str_replace( 'width="560"', 'width="800"', $html );
            $html = str_replace( 'height="315"', 'height="600"', $html );
        }
        return $html;
    }
    add_filter( 'oembed_dataparse', 'custom_oembed_dataparse', 10, 3 );
    ```
    
- **Customizing Embed Appearance**: You can also modify the embedded content using JavaScript or CSS. For example, you can use custom styles to adjust how embedded content like videos, images, or social media posts appear on your website.

## Resource
- [WordPress Developer - oEmbed](https://developer.wordpress.org/advanced-administration/wordpress/oembed/)