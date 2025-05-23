WooCommerce is a powerful eCommerce plugin for WordPress that allows you to create an online store. Like WordPress itself, WooCommerce uses object-oriented programming (OOP) and provides a variety of classes to facilitate the creation, management, and customization of your store. These classes are used for handling products, orders, customers, payments, and more. Below is an overview of some of the most commonly used **WooCommerce classes** and their functionality.

### **WC_Product**
- **Purpose**: Handles product-related data.
- **Description**: The `WC_Product` class is used to represent a product in WooCommerce. It provides methods for retrieving and managing product details like price, SKU, stock status, categories, attributes, etc.
- **Common Methods**:
    - `get_id()`: Gets the product ID.
    - `get_name()`: Gets the product name.
    - `get_price()`: Gets the product price.
    - `get_stock_status()`: Gets the stock status (e.g., in stock, out of stock).
    - `get_categories()`: Retrieves the categories of the product.

**Example**:
```php
$product = wc_get_product( 123 ); // Get product by ID
echo $product->get_name(); // Display product name
echo $product->get_price(); // Display product price
```

### **WC_Order**
- **Purpose**: Handles WooCommerce order data.
- **Description**: The `WC_Order` class is used for managing orders in WooCommerce. It provides methods to get order details, such as the products purchased, customer data, shipping and billing information, payment methods, and order status.
- **Common Methods**:
    - `get_id()`: Gets the order ID.
    - `get_items()`: Retrieves the items in the order.
    - `get_total()`: Gets the total amount of the order.
    - `get_billing_email()`: Retrieves the billing email of the customer.
    - `update_status()`: Updates the order status (e.g., processing, completed).

**Example**:
```php
$order = wc_get_order( 456 ); // Get order by ID
echo $order->get_total(); // Display total order amount
$items = $order->get_items();
foreach ($items as $item) {
    echo $item->get_name(); // Display product name in the order
}
```

### **WC_Cart**
- **Purpose**: Represents the customer's shopping cart.
- **Description**: The `WC_Cart` class is used to handle the cart contents, including adding/removing products, calculating totals, taxes, and shipping. It's automatically instantiated when a user adds items to their cart.
- **Common Methods**:
    - `add_to_cart()`: Adds a product to the cart.
    - `get_cart_contents()`: Retrieves all items currently in the cart.
    - `get_cart_total()`: Retrieves the total price of the cart.
    - `get_cart_subtotal()`: Retrieves the cart subtotal before taxes.

**Example**:
```php
$cart = WC()->cart;
$cart->add_to_cart( 123 ); // Add product ID 123 to the cart
echo $cart->get_cart_total(); // Display the total price of the cart
```

### **WC_Customer**
- **Purpose**: Represents a customer’s information.
- **Description**: The `WC_Customer` class is used to manage customer data, such as their personal details (name, email, billing/shipping address) and order history. This class is helpful for retrieving and updating user data.
- **Common Methods**:
    - `get_id()`: Gets the customer ID.
    - `get_email()`: Retrieves the customer's email address.
    - `get_billing_address()`: Retrieves the customer's billing address.
    - `get_shipping_address()`: Retrieves the customer's shipping address.

**Example**:
```php
$customer = new WC_Customer( get_current_user_id() ); // Get current logged-in customer
echo $customer->get_email(); // Display customer email
```

### **WC_Payment_Gateway**
- **Purpose**: Handles payment gateway integrations.
- **Description**: The `WC_Payment_Gateway` class is used by payment gateway plugins to integrate with WooCommerce. It defines methods to process payments, manage settings, and handle callbacks from payment providers.
- **Common Methods**:
    - `process_payment()`: Handles payment processing.
    - `is_available()`: Checks if the payment gateway is available.
    - `get_title()`: Gets the title of the payment method.

**Example**:
```php
// Example for adding a custom payment gateway
class WC_Gateway_Custom extends WC_Payment_Gateway {
    public function __construct() {
        $this->id = 'custom_gateway';
        $this->title = 'Custom Payment Gateway';
        $this->method_title = 'Custom Payment Gateway';
        // Define other settings...
    }

    public function process_payment( $order_id ) {
        $order = wc_get_order( $order_id );
        // Payment processing logic here
        return array(
            'result' => 'success',
            'redirect' => $order->get_checkout_payment_url( true )
        );
    }
}
```

### **WC_Product_Variable**
- **Purpose**: Represents a variable product (with variations).
- **Description**: The `WC_Product_Variable` class is a subclass of `WC_Product` and is used to represent variable products. Variable products have different variations (e.g., sizes, colors), and this class allows you to retrieve and manage those variations.
- **Common Methods**:
    - `get_variations()`: Retrieves all variations for the product.
    - `get_price()`: Retrieves the price of a specific variation.
    - `get_attribute()`: Retrieves the value of a product attribute (e.g., color or size).

**Example**:
```php
$product = wc_get_product( 789 ); // Get product by ID
$variations = $product->get_variations(); // Get all variations of the product
```

### **WC_Shipping_Method**
- **Purpose**: Handles shipping methods.
- **Description**: The `WC_Shipping_Method` class is used to define and handle shipping methods in WooCommerce. It allows you to add custom shipping methods or modify existing ones.
- **Common Methods**:
    - `calculate_shipping()`: Calculates the shipping cost for an order.
    - `is_available()`: Checks if the shipping method is available for the customer.

**Example**:
```php
class WC_Shipping_Method_Custom extends WC_Shipping_Method {
    public function __construct() {
        $this->id = 'custom_shipping';
        $this->title = 'Custom Shipping';
    }

    public function calculate_shipping( $package = array() ) {
        // Calculate shipping cost based on package
        $rate = array(
            'id' => $this->id,
            'label' => $this->title,
            'cost' => 10.00,
            'calc_tax' => 'per_order'
        );
        $this->add_rate( $rate );
    }
}
```

### **WC_Logger**
- **Purpose**: Handles logging for WooCommerce.
- **Description**: The `WC_Logger` class allows you to log messages to WooCommerce’s system log. This is useful for debugging and tracking various events in WooCommerce, such as payment processing or errors.
- **Common Methods**:
    - `log()`: Adds a message to the log file.

**Example**:
```php
$logger = wc_get_logger();
$logger->info( 'This is a log message.' );
```

## Resource
- [WooCommerce Developer - Classes in WooCommerce](https://developer.woocommerce.com/docs/classes-in-woocommerce/)
- [WooCommerce Code Reference - WooCommerce Classes](https://woocommerce.github.io/code-reference/packages/WooCommerce-Classes.html)