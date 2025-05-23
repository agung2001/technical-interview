# Raw Query
## Find product that has duplicate sku
```sql
SELECT meta_value, COUNT(*) AS sku_count
FROM wp_postmeta
WHERE meta_key = '_sku'
GROUP BY meta_value
HAVING sku_count > 1;
```

## Find product that related to the specific term_id
```sql
SELECT 
	p.*	
FROM wp_term_relationships tr 
INNER JOIN wp_term_taxonomy tt ON tr.term_taxonomy_id = tt.term_taxonomy_id
INNER JOIN wp_posts p ON tr.object_id = p.ID
WHERE tt.term_id = 1234 -- Change the term_id
```

## Manually Update Product Category Count
Update term taxonomy count
```sql
UPDATE wp_term_taxonomy tt 
SET count = (SELECT COUNT(tr.object_id) FROM wp_term_relationships tr WHERE tr.term_taxonomy_id = tt.term_taxonomy_id)  
WHERE tt.taxonomy = 'product_cat'
```
Update term meta `product_count_product_cat`
```sql
UPDATE wp_termmeta tt  
SET meta_value = (SELECT ttr.count FROM wp_term_taxonomy ttr WHERE tt.term_id = ttr.term_id)  
WHERE tt.meta_key = 'product_count_product_cat'
```

Also don't forget to run
```php
wp_cache_flush(); // to flush `woocommerce_get_product_subcategories_cache_key`
```

## Contributors
- [[Muhammad Agung Sundoro]]: 2024-12-23