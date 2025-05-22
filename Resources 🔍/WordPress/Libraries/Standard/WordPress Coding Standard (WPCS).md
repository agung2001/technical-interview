<iframe width="560" height="315" src="https://www.youtube.com/embed/sA7PLxTXBaQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

WordPress has its own coding standards called the "WordPress Coding Standards" (WPCS). These standards provide guidelines and best practices for writing code in a consistent and standardized manner to ensure readability, maintainability, and compatibility within the WordPress ecosystem.

The WordPress Coding Standards cover various aspects of coding, including:
1. PHP Coding Standards: These guidelines cover PHP syntax, naming conventions, indentation, spacing, commenting, and other coding practices specific to PHP code used in WordPress.
2. JavaScript Coding Standards: These guidelines cover JavaScript syntax, naming conventions, indentation, spacing, commenting, and best practices for writing JavaScript code in WordPress.
3. CSS Coding Standards: These guidelines cover CSS syntax, naming conventions, indentation, spacing, commenting, and best practices for writing CSS code in WordPress.
4. HTML Coding Standards: These guidelines cover HTML syntax, formatting, indentation, commenting, and best practices for writing HTML code in WordPress.

Following the WordPress Coding Standards is important as it helps maintain consistency across WordPress projects and improves code quality. It also makes it easier for other developers to read and understand your code.

To adhere to the WordPress Coding Standards, you can use tools like PHP_CodeSniffer with the WordPress Coding Standards ruleset. This tool automatically checks your code against the coding standards and provides suggestions or warnings for any violations.

By following the WordPress Coding Standards, you contribute to the overall quality and integrity of the WordPress ecosystem and ensure compatibility with other WordPress themes and plugins.

## phpcs.xml
```xml
<?xml version="1.0"?>
<ruleset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" name="WordPress Core" xsi:noNamespaceSchemaLocation="https://raw.githubusercontent.com/squizlabs/PHP_CodeSniffer/master/phpcs.xsd">

  <description>Non-controversial generally-agreed upon WordPress Coding Standards</description>

  <!--
  Included via WordPress-Extra.
  <rule ref="WordPress-Core"/>
  -->
  <rule ref="WordPress-Docs"/>
  <rule ref="WordPress-Extra">
    <!-- Prevent duplicate messages + deprecation notice from deprecated sniff. -->
    <exclude name="WordPress.WP.TimezoneChange.timezone_change_date_default_timezone_set"/>
    <exclude name="WordPress.WP.TimezoneChange.DeprecatedSniff"/>

    <exclude name="Generic.WhiteSpace.ScopeIndent"/>
    <exclude name="Generic.WhiteSpace.DisallowSpaceIndent"/>
    <exclude name="WordPress.NamingConventions.ValidVariableName"/>
    <exclude name="PSR2.Classes.PropertyDeclaration"/>
    <exclude name="WordPress.Files.FileName"/>
    <exclude name="PSR2.Methods.MethodDeclaration"/>

    <exclude name="Squiz.Commenting.FileComment"/>
    <exclude name="Squiz.Commenting.ClassComment.TagNotAllowed"/>
  </rule>

  <!-- Custom sanitization functions from WooCommerce. --> 
  <rule ref="WordPress.Security.ValidatedSanitizedInput">
    <properties>
      <property name="customSanitizingFunctions" type="array" value="wc_clean,wc_sanitize_tooltip,wc_format_decimal,wc_stock_amount,wc_sanitize_permalink,wc_sanitize_textarea" />
    </properties>
  </rule>

  <!-- Custom escaping functions from WooCommerce. --> 
  <rule ref="WordPress.Security.EscapeOutput">
    <properties>
      <property name="customEscapingFunctions" type="array" value="wc_help_tip,wc_sanitize_tooltip,wc_selected,wc_kses_notice,wc_esc_json,wc_query_string_form_fields,wc_make_phone_clickable,wc_price" />
    </properties>
  </rule>

  <!-- Custom capabilities from WooCommerce. --> 
  <rule ref="WordPress.WP.Capabilities">
    <properties>
      <property name="custom_capabilities" type="array" value="manage_woocommerce,edit_shop_coupons,edit_private_products,edit_shop_orders,edit_shop_orders" />
    </properties>
  </rule>

  <!-- Tests that the file name and the name of the class contained within the file match. -->
  <rule ref="Squiz.Classes.ClassFileName"/>

  <rule ref="WordPress.WP.I18n">
    <properties>
      <property name="text_domain" type="array">
        <element value="advanced-coupons-for-woocommerce-free"/> <!-- Change this value to your theme or plugin slug. -->
      </property>
    </properties>
  </rule>

  <!-- Disallow tabs for indentation -->
  <rule ref="Generic.WhiteSpace.DisallowTabIndent"/>

  <!-- Enforce 4 spaces for indentation -->
  <rule ref="Generic.WhiteSpace.ScopeIndent" />

</ruleset>
```

## Installation
- Clone `git glone https://github.com/WordPress/WordPress-Coding-Standards.git`
- Composer install `composer install`

## Resource
- [GitHub - WordPress/WordPress-Coding-Standards](https://github.com/WordPress/WordPress-Coding-Standards)
- [Tutorial : PHP Code Sniffer with WordPress Coding Standards and PHPStorm](https://www.youtube.com/watch?v=R4URxom9Kew&t=423s)