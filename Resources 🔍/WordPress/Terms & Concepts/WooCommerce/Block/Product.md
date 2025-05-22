## Adding new Tab Product Editor
- [Comment](https://developer.woo.com/2023/11/17/getting-to-know-woo-extensibility-in-the-new-product-editor/#comment-12166)
```php
<?php

use Automattic\WooCommerce\Admin\BlockTemplates\BlockInterface;
use Automattic\WooCommerce\Admin\Features\ProductBlockEditor\ProductTemplates\GroupInterface;
use Automattic\WooCommerce\Admin\Features\ProductBlockEditor\ProductTemplates\ProductFormTemplateInterface;

add_action(
	'woocommerce_block_template_area_product-form_after_add_block_general',
	function ( BlockInterface $general_group ) {
		$template = $general_group->get_root_template();

		/*
		 * Why is this check necessary?
		 * - Allow VSCode to provide autocomplete for the specific product form template methods
		 */
		if ( ! $template instanceof ProductFormTemplateInterface ) {
			return;
		}

		$my_group = $template->add_group(
			array(
				'id'         => 'your-prefix-example-group',
				'attributes' => array(
					'title' => __( 'My Group', 'YOUR_TEXT_DOMAIN' ),
				),
			)
		);

		/*
		 * Why is this check necessary?
		 * - Because of current bug in the add_group() docblock (https://github.com/woocommerce/woocommerce/issues/41587)
		 */
		if ( ! $my_group instanceof GroupInterface ) {
			return;
		}

		$section_1 = $my_group->add_section(
			array(
				'id'         => 'your-prefix-example-section-1',
				'attributes' => array(
					'title' => __( 'My Section One', 'YOUR_TEXT_DOMAIN' ),
				),
			)
		);

		$section_1->add_block(
			array(
				'id'         => 'your-prefix-example-block-1',
				'blockName'  => 'woocommerce/product-text-field',
				'attributes' => array(
					'label'    => __( 'My Block One', 'YOUR_TEXT_DOMAIN' ),
					'property' => 'meta_data.your_prefix_example_field_1',
				),
			)
		);

		$section_2 = $my_group->add_section(
			array(
				'id'         => 'your-prefix-example-section-2',
				'attributes' => array(
					'title' => __( 'My Section Two', 'YOUR_TEXT_DOMAIN' ),
				),
			)
		);

		$section_2->add_block(
			array(
				'id'         => 'your-prefix-example-block-2',
				'blockName'  => 'woocommerce/product-checkbox-field',
				'attributes' => array(
					'label'    => __( 'My Block Two', 'YOUR_TEXT_DOMAIN' ),
					'property' => 'meta_data.your_prefix_example_field_2',
				),
			)
		);
	}
);
```

## Resource
- [WooCommerce Docs - ProductTemplates](https://github.com/woocommerce/woocommerce/blob/trunk/plugins/woocommerce/src/Admin/Features/ProductBlockEditor/ProductTemplates/README.md)

## News
- [Introducing a brand-new product creation experience powered by Blocks](https://developer.woocommerce.com/2023/06/28/introducing-a-brand-new-product-creation-experience-powered-by-blocks)
	- [Block-based Product Creation Experience](https://developer.woo.com/roadmap/block-based-product-creation-experience)
- [Getting to Know Woo: Extensibility in the New Product Editor](https://developer.woo.com/2023/11/17/getting-to-know-woo-extensibility-in-the-new-product-editor/)

## Contributors
- [[Muhammad Agung Sundoro]]