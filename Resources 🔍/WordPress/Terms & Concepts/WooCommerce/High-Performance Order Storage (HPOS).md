WooCommerce has stored order-related data in the post and postmeta tables in the database as a custom WordPress post type so far. This has allowed everyone working in the ecosystem to take advantage of extensive APIs provided by the WordPress core in managing orders as custom post types.

However, earlier this year, [we announced the plans to migrate to dedicated tables for orders](https://developer.woocommerce.com/2022/01/17/the-plan-for-the-woocommerce-custom-order-table/). Orders in their own tables will allow the shops to scale more easily, make the data storage simpler and increase reliability. For further details, please check out our [deep dive on the database structure on our dev blog](https://developer.woocommerce.com/2022/09/15/high-performance-order-storage-database-schema/).

Generally, WooCommerce has tried to be fully backward compatible with the older versions, but, as a result of this project, extension developers will be required to make some changes to their plugins to take advantage of the HPOS. This is because the underlying data structure has changed fundamentally.

More specifically, instead of using WordPress-provided APIs to access order data, developers will need to use WooCommerce-specific APIs. We [introduced these APIs in WooCommerce version 3.0](https://developer.woocommerce.com/2017/04/04/say-hello-to-woocommerce-3-0-bionic-butterfly/) to make the transition to HPOS easier.

You can speed up the initial synchronization by executing the sync in the WP CLI environment by running `wp wc cot sync` command.
```
> wp wc cot sync  
  
This feature is not production ready yet. Make sure you are not running these commands in your production environment.  
  
There are 22872 orders to be synced.  
  
Order Data Sync  100% [===========================================================================================================] 1:34 / 1:12  
  
Migration completed.  
  
Success: 22872 orders were migrated in 90.777226 seconds
```

## Resource
- [Official Docs](https://woocommerce.com/document/high-performance-order-storage/)
	- [High Performance Order Storage Upgrade Recipe Book](https://github.com/woocommerce/woocommerce/wiki/High-Performance-Order-Storage-Upgrade-Recipe-Book)
	- [Performance Benchmarking for WooCommerce HPOS](https://developer.woocommerce.com/2023/03/17/performance-benchmarking-for-woocommerce-hpos/)
	- [The Plan for the WooCommerce Custom Order Table](https://developer.woocommerce.com/2022/01/17/the-plan-for-the-woocommerce-custom-order-table/)
	- [High-Performance Order Storage Upgrade: FAQs](https://developer.woocommerce.com/2022/10/11/hpos-upgrade-faqs/)
- [How to get your store ready for High-Performance Order Storage? ( HPOS )](https://www.multidots.com/how-to-get-your-store-ready-for-hpos/)

## Contributors
- [[Muhammad Agung Sundoro]]