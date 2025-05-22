# WP-CLI - Just Another Awesome Tool for WordPress Development
![](https://avatars.githubusercontent.com/u/1570774?s=280&v=4)

WP-CLI is the command-line interface for WordPress. It allows you to manage your WordPress site from the command line, without using a web browser. WP-CLI is a powerful tool that can be used to perform a wide range of tasks, including:

-   Installing and uninstalling plugins
-   Activating and deactivating plugins
-   Managing themes
-   Managing users
-   Creating and editing posts
-   Managing comments
-   Backing up and restoring your site
-   And much more

WP-CLI is a great way to automate tasks and get more done with WordPress. It is also a great way to troubleshoot problems and fix errors. If you are a WordPress developer or administrator, then WP-CLI is a must-have tool.

To install WP-CLI, you can use the following steps:
1.  Download the WP-CLI installer from the WP-CLI website.
2.  Save the installer to your computer.
3.  Open a terminal window and navigate to the directory where you saved the installer.
4.  Run the following command: `php wp-cli.phar install`
5. WP-CLI will be installed. You can now use it to manage your WordPress site from the command line.

Here are some of the benefits of using WP-CLI:
- **Efficiency:** WP-CLI can help you automate tasks and get more done with WordPress.
- **Power:** WP-CLI is a powerful tool that can be used to perform a wide range of tasks.
- **Flexibility:** WP-CLI is highly flexible and can be customized to meet your specific needs.
- **Community:** There is a large and active community of WP-CLI users who can help you learn and use WP-CLI.

## Command

### Export Database
```shell
wp db export <file>.sql
```

### Perform Search Replace
```shell
wp search-replace 'http://website.com/' 'http://website-replace.com/' --all-tables-with-prefix --allow-root
```

### Scaffold Plugin
```shell
wp scaffold plugin PluginName --plugin_name=PluginName --plugin_description=Description --plugin_author=artistudio --plugin_author_uri=https://profiles.wordpress.org/artistudio
```

## WP Scaffold
Generates code for post types, taxonomies, plugins, child themes, etc. [Read More](https://developer.wordpress.org/cli/commands/scaffold/)
- [Scaffold Plugin](https://developer.wordpress.org/cli/commands/scaffold/plugin/)

## Resource
- [Official Website](https://wp-cli.org/)
- [WP-Kama - WP-CLI](https://wp-kama.com/handbook/wp-cli)
- [Contribution Guide Tutorials](https://www.youtube.com/playlist?list=PL_B8Y6K6MH2d6T7pYa6dloUgk67mfBT4K)

## Contributors
- [[Muhammad Agung Sundoro]]