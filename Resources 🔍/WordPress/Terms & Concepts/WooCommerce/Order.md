In WooCommerce, an order represents a customer's purchase transaction made on an online store. It is a crucial part of the e-commerce process, as it tracks the details of the customer's purchase, including the products bought, shipping and billing information, payment method, and any applied discounts or coupons.

Each order in WooCommerce is uniquely identified by an order ID, and it contains various data fields, such as:
1. Order Status: The current status of the order, such as "pending," "processing," "completed," "on-hold," "cancelled," etc.
2. Customer Information: Details about the customer who placed the order, such as name, email address, billing and shipping addresses.
3. Order Items: A list of products or services that the customer purchased, along with their quantities, prices, and any applied taxes.
4. Order Total: The total amount the customer needs to pay, including product prices, shipping costs, taxes, and discounts.
5. Payment Information: The payment method used by the customer for the order, such as credit card, PayPal, bank transfer, etc.
6. Shipping Method: The chosen shipping method for delivering the order to the customer.
7. Order Notes: Any additional notes or comments added to the order by the customer or store admin.
8. Date and Time: The date and time when the order was placed and when it was last updated.

WooCommerce provides extensive features to manage orders, including the ability to view, process, edit, and fulfill orders from the WooCommerce admin panel. Store owners can also generate invoices, packing slips, and shipping labels for orders, as well as track and manage inventory levels.

## High-Performance Order Storage (HPOS)
For those developer who are working WooCommerce you might want to check [[High-Performance Order Storage (HPOS)|High-Performance Order Storage (HPOS)]] because effectively WooCommerce will set this feature as default storage for order on the next release of the plugin.

## Order Status
![](https://woo.com/wp-content/uploads/2013/05/woocommerce-order-process-diagram.png)
- **Pending payment** — Order received, no payment initiated. Awaiting payment (unpaid).
- **Failed** — Payment failed or was declined (unpaid) or requires authentication (SCA). Note that this status may not show immediately and instead show as **Pending** until verified (e.g., PayPal). Here is a [helpful article](https://woo.com/posts/understand-and-fix-failed-order-status-in-woocommerce/) for a better understanding and how to fix failed orders in WooCommerce.
- **Processing** — Payment received (paid) and stock has been reduced; order is awaiting fulfillment. All product orders require processing, except those that only contain products which are both [Virtual and Downloadable](https://woo.com/document/digitaldownloadable-product-handling/).
- **Completed** — Order fulfilled and complete – requires no further action.
- **On hold** — Awaiting payment – stock is reduced, but you need to confirm payment.
- **Cancelled** — Cancelled by an admin or the customer – stock is increased, no further action required.  
    Please note: _This status **does not** refund the customer._  
    An example use case: The merchant wants to cancel the order because the customer has become unresponsive and they do not know where to ship the product. The customer is not eligible for a refund in this case.  
    _To issue a refund please follow the [**Manage refunds**](https://href.li/?https://woo.com/document/woocommerce-refunds/) documentation._
- **Refunded** — Refunded by an admin – no further action required.
- **Authentication required** — Awaiting action by the customer to authenticate the transaction and/or complete SCA requirements.
- **Checkout draft** — Draft order created when customers start the checkout process with [WooCommerce Blocks](https://woo.com/document/woocommerce-blocks/#section-9) checkout block enabled.
## Resource
- [Code Reference](https://woocommerce.github.io/code-reference/)
	- [WC_Order](https://woocommerce.github.io/code-reference/classes/WC-Order.html)
- WooCommerce Documentation
	- [Managing Orders](https://woo.com/document/managing-orders/)

## Contributors
- [[Muhammad Agung Sundoro]]